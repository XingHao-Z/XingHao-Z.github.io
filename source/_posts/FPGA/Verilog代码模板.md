---
title: Verilog代码模板
date: 2023-10-9 12:03:39
tags:
 - FPGA
 - UART
category:
 - FPGA
description: Verilog常用的重复的代码模板
---

# 分频

## 偶数分频

```verilog
module divider #(
    parameter DIV_NUM = 8       //分频系数
) (
    input               sys_clk,
    input               rst_n,
    output              clk_out
);
reg         clk_out_reg = 0;


parameter cnt_width	= $clog2(DIV_NUM)	    ;	// 求分频系数相应计数器的位数
parameter cnt_max	= (DIV_NUM >> 1) - 1	;	// 设置计数器的最大值，即 (N/2)-1

reg [cnt_width - 1 : 0]     cnt;

always @(posedge sys_clk or negedge rst_n) begin
    if(!rst_n)
        cnt <= 0;
    else if(cnt == cnt_max)
        cnt <= 0;
    else
        cnt <= cnt + 1'b1;
end

always @(posedge sys_clk or negedge rst_n) begin
    if(!rst_n)
        clk_out_reg <= 0;
    else if(cnt == cnt_max)
        clk_out_reg <= ~clk_out_reg;
    else
        clk_out_reg <= clk_out_reg;
end

assign clk_out = clk_out_reg;

endmodule
```

## 奇数分频

```verilog
module divider #(
    parameter DIV_NUM = 9       //分频系数
) (
    input               sys_clk,
    input               rst_n,
    output              clk_out
);

parameter cnt_width	= $clog2(DIV_NUM)	;	// 求分频系数相应计数器的位数
parameter cnt_max	= DIV_NUM - 1	    ;	// 设置计数器的最大值，即 N-1

reg [cnt_width - 1 : 0]     cnt;
reg                         clk1;
reg                         clk2;          

always @(posedge sys_clk or negedge rst_n) begin
    if(!rst_n)
        cnt <= 0;
    else if(cnt == cnt_max)
        cnt <= 0;
    else
        cnt <= cnt + 1'b1;
end


always @(posedge sys_clk or negedge rst_n) begin
    if(!rst_n)
        clk1 <= 0;
    else if(cnt == cnt_max>>1)
        clk1 <= 1'b1;
    else if(cnt == cnt_max)
        clk1 <= 1'b0;
end

always @(negedge sys_clk or negedge rst_n) begin
    if(!rst_n)
        clk2 <= 0;
    else if(cnt == cnt_max>>1)
        clk2 <= 1'b1;
    else if(cnt == cnt_max)
        clk2 <= 1'b0;
end

assign clk_out = clk1 | clk2;

endmodule
```



# UART

## UART_RX

```verilog
//接收到一个字节的数据后，并行发送出去，同时发送标志信号
//uart_byte_out 和 byte_end_flag 常低
module UART_RX#(
    parameter clk_rate      = 50_000_000,       //系统时钟
    parameter buad_rate     = 9600,             //波特率
    parameter data_width    = 8,                //数据位
    parameter hold          = 5                 //输出保持的周期数
) (
    input                               clk,                    //时钟信号
    input                               rst_n,                    
    input                               uart_data_in,           //从低位到高位的bit流

    output          [data_width-1 : 0]  uart_byte_out,          //送出的数据为8bit
    output                              byte_end_flag           //表示数据是否准备好，高：准备好；
);



localparam  CNT_MAX     = clk_rate / buad_rate      ;   //每个bit对应的时钟数
localparam  CNT_HALF    = clk_rate / (buad_rate*2)  ;   //CNT_MAX的一半
localparam  CNT_WIDTH	= $clog2(CNT_MAX)           ;   //计数寄存器的位宽
reg     [CNT_WIDTH : 0]   clk_cnt = 0 ;

localparam  HOLD_CNT_WIDTH  = $clog2(hold)          ;
localparam  DATA_CNT_WIDTH  = $clog2(data_width)    ;
reg     [HOLD_CNT_WIDTH : 0]  hold_cnt = 0    ;
reg     [DATA_CNT_WIDTH : 0]  data_cnt = 0    ;


reg     [data_width-1 : 0]   data_reg = 0   ;       //暂存输出的寄存器

//状态机
localparam  IDLE        = 3'd0  ;       //空闲
localparam  START       = 3'd1  ;       //接收到起始位
localparam  DATA        = 3'd2  ;       //接收数据
localparam  STOP        = 3'd3  ;       //接收到停止位
localparam  HOLD        = 3'd4  ;       //发送数据和一个字节结束标志
reg [2:0] state, next_state;




//-----------------状态转移--------------------
always @(posedge clk or negedge rst_n) begin
    if(!rst_n)
        state <= IDLE;
    else
        state <= next_state;
end



//--------------------------下一状态---------------------------
always @(*) begin
    case(state)
        IDLE:           next_state = (uart_data_in ? IDLE : START);
        START:          next_state = (clk_cnt == CNT_HALF) ? (uart_data_in ? IDLE : DATA) : START;
        DATA:           next_state = (data_cnt == data_width) ? STOP : DATA;
        STOP:           next_state = (clk_cnt == CNT_MAX) ? (uart_data_in ? HOLD : IDLE) : STOP;
        HOLD:           next_state = (hold_cnt == hold - 1'b1) ? IDLE : HOLD;
        default:        next_state = IDLE;
    endcase
end


//--------------------------每个状态的处理-------------------------
always @(posedge clk or negedge rst_n) begin
    if(!rst_n) begin
        clk_cnt     <= 0;
    end
    else begin
        case(state)
            IDLE:   clk_cnt     <= 0;     

            START:  begin
                        if(clk_cnt == CNT_HALF)begin
                            clk_cnt     <= 0;
                        end
                        else begin
                            clk_cnt     <= clk_cnt + 1'b1;
                        end
                    end

            DATA,STOP:   begin                        
                        if(clk_cnt == CNT_MAX)begin
                            clk_cnt     <= 0;
                        end
                        else begin
                            clk_cnt     <= clk_cnt + 1'b1;
                        end
                    end
        endcase
                    
    end
end


always @(posedge clk or negedge rst_n) begin
    if(!rst_n) begin
        data_cnt    <= 0;
        data_reg    <= 0;
    end
    else begin
        case (state)
            IDLE: begin
                data_cnt    <= 0;
                data_reg    <= 0;
            end

            DATA: begin
                if(clk_cnt == CNT_MAX)begin
                    data_cnt            <= data_cnt + 1'b1;
                    data_reg[data_cnt]  <= uart_data_in;
                end
            end

            default: begin
                data_cnt    <= data_cnt;
                data_reg    <= data_reg;
            end
        endcase
    end
end

always @(posedge clk or negedge rst_n) begin
    if(!rst_n) begin
        hold_cnt    <= 0;
    end
    else if(state == HOLD)begin
        hold_cnt    <= hold_cnt + 1'b1;
    end
    else begin
        hold_cnt    <= 0;
    end
end


//--------------------------输出-------------------------------------
assign uart_byte_out = (state == HOLD) ? data_reg : 0;
assign byte_end_flag = (state == HOLD);


endmodule

```





# testbench

## UART接收1字节数据

```verilog
parameter clk_rate = 50_000_000;
parameter buad_rate = 9600;
parameter interval = clk_rate / buad_rate;

task receive_data;
    input[31:0] A;
    begin
        repeat(100)@(posedge clk);
        uart_data_in = 1'b0; 
        repeat(8)begin
            repeat(interval)@(posedge clk);
            uart_data_in = A[0];
            A = A>>1;
        end
        repeat(interval)@(posedge clk);
        uart_data_in = 1'b1;
        repeat(interval)@(posedge clk);
        repeat(interval*2)@(posedge clk);
    end
endtask
```



