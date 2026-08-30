# AGENTS.md

## Project overview

This repository contains the source for a Hexo blog.

- Hexo: 8.1.2
- Theme: Butterfly 5.7.0, installed through npm
- Source branch: `hexo`
- Generated GitHub Pages branch: `master`
- Site config: `_config.yml`
- Butterfly overrides: `_config.butterfly.yml`
- Published posts: `source/_posts/`
- Drafts: `source/_drafts/`
- Generated output: `public/`

## Environment

- Use Node.js 20.19.0 or newer.
- Prefer a current Node.js 20 LTS release unless the user requests otherwise.
- Install dependencies with `npm ci`.
- Pandoc must be installed and available on `PATH`.
- Preserve UTF-8 encoding, Chinese filenames, punctuation, and directory names.
- Do not update dependencies or rewrite `package-lock.json` unless explicitly
  requested.

## Generated and dependency files

Never manually edit or commit:

- `node_modules/`
- `public/`
- `.deploy_git/`
- `db.json`
- log files

The Butterfly theme is installed as the `hexo-theme-butterfly` npm package.
Do not edit files under `node_modules/hexo-theme-butterfly/`.

Put site-specific Butterfly settings in `_config.butterfly.yml`.
Put custom static assets under `source/`, for example `source/img/`.
Do not store custom assets inside `node_modules` or the installed theme package.

## Content conventions

- Published posts belong under `source/_posts/`.
- Unfinished posts belong under `source/_drafts/`.
- Preserve existing subject directories such as `1-通信`, `2-软件`,
  and `3-Hexo的使用`.
- Keep valid YAML Front Matter between `---` markers.
- Follow the fields in `scaffolds/post.md`:
  `title`, `date`, `tags`, `categories`, `description`, and `mathjax`.
- Set `mathjax: true` only when an article requires mathematical rendering.
- Do not change article dates, categories, tags, technical conclusions, or
  wording unless explicitly requested.

## Post assets

`post_asset_folder` is enabled.

- Keep local article images in a directory whose basename matches the Markdown
  filename.
- When renaming or moving a post, move its matching asset directory.
- Update all affected image references.
- Before finishing, check that every referenced local asset exists.
- Do not rename Chinese paths only for normalization.

## Theme and configuration

- Prefer `_config.butterfly.yml` for site-specific theme customization.
- Do not copy or edit theme files under `node_modules`.
- If a layout or style override is required, first explain the maintainable
  override approach and obtain approval before vendoring or patching theme
  source.
- Do not upgrade Hexo, Butterfly, plugins, or the lockfile unless explicitly
  requested.
- When upgrading Butterfly, compare the existing override file with the new
  package's `_config.yml`; migrate settings selectively instead of replacing
  the entire file.
- Never add credentials, SSH keys, access tokens, or private service secrets.

## Validation

For content-only changes:

1. Validate Front Matter.
2. Confirm referenced local assets exist.
3. Preserve Chinese paths and links.
4. Inspect the affected page when rendering behavior may change.

For dependency, configuration, renderer, layout, or theme changes, run:

```powershell
npm run clean
npm run build
```

For visual changes, additionally run:

```powershell
npm run server
```

and inspect the affected pages at `http://localhost:4000/`.

There is no automated test or lint command. A successful clean Hexo build is
the minimum repository-wide validation.

## Deployment safety

Do not run any of the following unless the user explicitly requests
deployment:

```powershell
npm run deploy
npx hexo deploy
git push
```

Deployment publishes generated files to the `master` branch of:

```text
git@github.com:XingHao-Z/XingHao-Z.github.io.git
```

Before an explicitly requested deployment:

1. Run a clean build.
2. Report all warnings and failures.
3. Confirm the current source branch and destination branch.
4. Do not commit `public/` to the `hexo` branch.

## Scope discipline

- Preserve unrelated and pre-existing user changes.
- Never discard a dirty working tree.
- Avoid broad Markdown or YAML formatting rewrites.
- Report which posts, assets, configs, dependencies, and generated pages are
  affected.
- Ask before deleting unexpected or untracked files.
