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

Docusaurus supports single-sourcing with markdown files that are importable in other files. While any page can be imported into any other page, its conventional that imported pages begin with an underscore `_`. Docusaurus calls those files **partials**. The markdown content in a partial is rendered in a file that imports it. See [Docusaurus partial docs](https://docusaurus.io/docs/markdown-features/react#importing-markdown) for more info.

In Redpanda documentation, save partials in a `shared` folder, at the root of the directory that shares the same context. If the partial doc can be used in more contexts, go up on level in the file tree. For example, the `docs/deploy/kubernetes/shared` folder contains partials with k8s content that's imported by docs in `docs/deploy/kubernetes`; general partials are stored at `docs/shared` and used throughout the project.

Example:

File `docs/deploy/shared/_markdown-partial-example.mdx`:

```javascript
<span>Hello {props.name}</span>
This is text some content from `_markdown-partial-example.mdx`.
```

The file that imports it must follow this syntax:

File `docs/deploy/use-example.mdx`:

```javascript
import PartialExample from './shared/_markdown-partial-example.mdx';
<PartialExample name="Redpanda Docs" />
```

The HTML output of the file `docs/deploy/use-example.mdx` will be:

```
Hello Redpanda Docs
This is text some content from _markdown-partial-example.md.
```

## Limitations :warning:

- **Headings**. Currently Docusaurus has a limitation in which the table of contents (the right navigation pane) doesn't import headings in partials. See its [Docusaurus open issue](https://github.com/facebook/docusaurus/issues/3915). There's no know workaround.

- **Relative links**. Relative links still follows the file tree where they were created. The partials feature doesn't change the link destination. For example, if your partial is saved in `docs/folderA/shared/_partial` and you want import it from `docs/folderB/folderC/my-file`, the relative link won't work, because the relative location is physically different. :bulb: Workaround: Use absolute links or use links as variables.
 
Examples of partials in Redpanda documentation:

- [docs/get-started/shared/_rpk-version.mdx](https://github.com/redpanda-data/documentation/blob/dev/docs/get-started/shared/_rpk-version.mdx)
- [docs/manage/kubernetes/shared/_values-yaml.mdx](https://github.com/redpanda-data/documentation/blob/dev/docs/manage/kubernetes/shared/_values-yaml.mdx)