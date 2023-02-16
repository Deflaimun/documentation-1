# Website

This website is built using [Docusaurus 2](https://docusaurus.io/), a modern static website generator.

## Local Development

```console
npm run start
```

This command starts a local development server and opens up a browser window. Most changes are reflected live without having to restart the server.

## Build

```console
yarn build
```

This command generates static content into the `build` directory and can be served using any static contents hosting service.

## Style Guide

Before you add or edit content, consult the Redpanda Style Guide (available on the [wiki](https://vectorizedio.atlassian.net/wiki/spaces/DOC/pages/92635182/Redpanda+Style+Guide) or in [Google Docs](https://drive.google.com/drive/folders/1dZqaWhAqe5-jHcOd0y6WRflMUxEPNK4Q?ths=true)) for product documentation guidelines.

## Best practices

### Single-sourcing with partials

Practice the DRY (Don't Repeat Yourself) principle by single-sourcing repeated content. Common examples of single-sourced content include prerequisites, contact info, and foundational steps of how-to guides.

Docusaurus supports single-sourcing with partials: markdown files that are importable in other files. The markdown content in a partial is rendered in a file that imports it. See [Docusaurus](https://docusaurus.io/docs/markdown-features/react#importing-markdown) for an example partial and an example import of a partial.

Partial filenames must be prefixed with an underscore (`_my_partial.mdx`). Docusaurus doesn't create doc pages for files prefixed with an underscore.

In Redpanda documentation, save partials in a `shared` folder, with `shared` at the root of the directory tree containing the files that import the partials. For example, in Redpanda documentation the `docs/deploy/kubernetes/shared` folder contains partials with k8s content that's imported by docs in `docs/deploy/kubernetes`.

> :warning: **Don't use headings in partials**. Currently Docusaurus has a limitation in which the table of contents in the right navigation pane doesn't display headings in partials. See its [Docusaurus open issue](https://github.com/facebook/docusaurus/issues/3915).

> :bulb: **Use absolute links in partials**. Relative links in partials will only work where they were created. For example, if your partial is saved in `docs/folderA/shared/_partial` and you want import it from `docs/folderB/folderC/my-file`, the relative link won't work, because the relative location is different.
 
Examples of partials in Redpanda documentation:

- [docs/get-started/shared/_rpk-version.mdx](https://github.com/redpanda-data/documentation/blob/dev/docs/get-started/shared/_rpk-version.mdx)
- [docs/manage/kubernetes/shared/_values-yaml.mdx](https://github.com/redpanda-data/documentation/blob/dev/docs/manage/kubernetes/shared/_values-yaml.mdx)