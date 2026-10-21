# Dignite Docs

User documentation for Dignite products, published at [docs.dignite.com](https://docs.dignite.com).

The site is built with the [ABP Docs module](https://abp.io/docs/latest/modules/docs). It reads the files in this repository straight from GitHub, so a change merged into `main` shows up on the site without a deployment.

## This repository is public

Everything here can be read by anyone, and every file under a product's folder can be reached on the site by its path, whether or not the navigation links to it. Keep out of this repository:

- internal design notes and investigations (they stay in the product's own repository, such as `dev-docs/` in Campus),
- customer names, data or screenshots that show them,
- secrets of any kind: keys, passwords, connection strings, internal URLs.

The documentation of products whose source is private lives here for the same reason: the site reads this repository without a GitHub token, so it never has access to anything that is not already public.

## Products

| Folder | Product | Site |
|---|---|---|
| `campus/` | Dignite Campus, a school management system for Japanese language schools | `https://docs.dignite.com/{language}/campus/latest` |
| `campus-students/` | The Dignite Campus guide for the students of those schools, in the languages of the student app | `https://docs.dignite.com/{language}/campus-students/latest` |

Each folder is a separate project on the site, with its own languages, navigation and pages.

In `campus-students/`, the words in bold are the app's own button and screen names, copied from the student app's translations: change them when the app's change. Schools hand out `https://docs.dignite.com/campus-students` (an address without a language opens in the language of the reader's browser, or the default language, English, when the guide does not have it) or a language's own address; the school manual lists them in `campus/ja/app-linking.md`.

### Documented in their own repository

A product whose documentation follows its releases keeps it in its own repository (see [Versions](#versions)), and the site reads it from there, in the same format:

| Repository | Product | Site |
|---|---|---|
| [`dignite-projects/abp-modules`](https://github.com/dignite-projects/abp-modules/tree/main/docs) (`docs/`) | Dignite ABP Modules: BLOB Storing, FlexFields, Notifications and the MCP server, open-source modules for the ABP Framework | `https://docs.dignite.com/{language}/abp-modules/{version}` |
| [`dignite-projects/site`](https://github.com/dignite-projects/site/tree/main/docs) (`docs/`) | Dignite Site: an open-source, multi-tenant CMS for the ABP Framework, built and run from your own AI client over MCP | `https://docs.dignite.com/{language}/site/{version}` |

Their pages are written in those repositories, next to the code, and are versioned by their releases.

## Layout of a product folder

```
campus/
  docs-langs.json        languages of this product
  en/
    Index.md             the page a project opens with
    docs-nav.json        the navigation tree
    getting-started.md
    images/
      sign-in.png
  ja/
    ...
  zh-Hans/
    ...
```

`docs-langs.json` lists the languages, one of them marked as the default:

```json
{
  "Languages": [
    { "DisplayName": "English", "Code": "en", "IsDefault": true },
    { "DisplayName": "日本語", "Code": "ja", "IsDefault": false },
    { "DisplayName": "简体中文", "Code": "zh-Hans", "IsDefault": false }
  ]
}
```

`docs-nav.json`, one per language, is the tree on the left of every page. A node with `path` is a page; a node with only `items` is a group:

```json
{
  "items": [
    {
      "text": "Getting started",
      "items": [
        { "text": "Overview", "path": "Index.md" },
        { "text": "Signing in", "path": "getting-started.md" }
      ]
    }
  ]
}
```

## Writing pages

- Pages are Markdown (`.md`). The file name, without `.md`, becomes the end of the page's address, so use lowercase words joined by hyphens and do not rename a published page.
- Link to other pages and to images with relative paths, as they sit in the folder: `[Signing in](getting-started.md)`, `![Sign-in page](images/sign-in.png)`.
- Keep each language's pages at the same paths, so a visitor switching language lands on the same page.
- A new page appears on the site once it is in `docs-nav.json` and merged into `main`. The site checks GitHub for changes to a page it has already shown about every six hours.

## Versions

The site shows `main` as the latest version. The repository has no releases yet; a GitHub release here would version every product at once, so a product that needs versioned documentation will get its own repository.

## License

The documentation is licensed under [CC BY 4.0](LICENSE). The code samples in it are licensed under the [MIT License](LICENSE-CODE).
