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

## Single-sourcing/ partials
There are some instances where you want to write one document and display in two (or more) pages. For that use case, you want your content to be single-sourced. Examples: common steps, introductory section that needs to be repeated.

### How
Docusaurus has a feature where you can import markdown pages into one another. They call those files **partials**. 

While it's technically possible to import any page into any other page, we have some convetions.

- Any imported page use `_` as the filename prefix. 
- Use a folder called `shared` to put your partials. You have to decide in what level this folder should be created. If you think that this partial page could be used by other contexts, create the folder in the level that makes sense. For example, the product version makes sense to the whole project, so we could create it at `docs/shared`. Some niche kubernetes docs only makes sense in that context, then `docs/deploy/kubernetes/shared`. 

Examples on how to use it:

File `docs/shared/_markdown-partial-example.mdx`:

```javascript
<span>Hello {props.name}</span>

This is text some content from `_markdown-partial-example.mdx`.
```

The file that imports it must follow this syntax: 

File `docs/deploy/use-example.mdx`:

```javascript
import PartialExample from './_markdown-partial-example.mdx';

<PartialExample name="Redpanda Docs" />
```

The output of the file `docs/deploy/use-example.mdx` will be:

```
Hello Redpanda Docs
This is text some content from _markdown-partial-example.md.
```

More on that, on [Docusaurus documentation on partials](https://docusaurus.io/docs/markdown-features/react#importing-markdown)

### Limitations
Currently Docusaurus has a huge limitation in which the table of contents (the right side nav), does not contain the imported Markdown headings. [They have an open issue tracking it](https://github.com/facebook/docusaurus/issues/3915). There's no know workaround.

Relative links will only work where they were created. For example, if your partial file lives under `docs/folderA/shared/_partial` and you want to use in `docs/folderB/folderC/my-file` the relative link won't work, because the relative location is different, you have essentially another level. Workaround: Use fixed links, use links as variables.

### Examples

- [docs/get-started/shared/_rpk-version.mdx](https://github.com/redpanda-data/documentation/blob/dev/docs/get-started/shared/_rpk-version.mdx)
- [docs/manage/kubernetes/shared/_values-yaml.mdx](https://github.com/redpanda-data/documentation/blob/dev/docs/manage/kubernetes/shared/_values-yaml.mdx)