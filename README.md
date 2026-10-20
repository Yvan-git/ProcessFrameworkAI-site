# The Collabior Process Framework — the published artefact

This repository holds the **built** browser application for the Collabior
Process Framework, and nothing else. The source — the framework itself, the
toolchain that compiles it, and the tests that check it — lives in
[`Yvan-git/ProcessFrameworkAI`](https://github.com/Yvan-git/ProcessFrameworkAI),
which stays private.

The live site is published from
[`Yvan-git/Yvan-git.github.io`](https://github.com/Yvan-git/Yvan-git.github.io)
and served at <https://yvan-git.github.io/>.

Both repositories receive the same files in the same run of the
`publish-site` workflow in the source repository, so they cannot drift apart.

## Serving it from a web root

This repository is a complete static site. Clone it into a web root and it
works:

```bash
git clone https://github.com/Yvan-git/ProcessFrameworkAI-site.git public_html/framework.collabior.com
```

On Apache — which is what cPanel and most shared hosts run — this is the
whole deployment. The files are:

- `index.html`, `200.html` and `404.html` — the same single-page
  application shell. Apache serves `index.html` for `/`; the `.htaccess`
  rewrites unknown paths to `200.html`; `404.html` is there for hosts that
  serve it instead.
- `framework/` — the compiled framework as JSON: the map, the documents, the
  policies, the skills, the templates.
- `_app/` — the hashed JavaScript and CSS. Do not rename or re-compress
  these files; their names carry a content hash.

To update, `git pull` in the web root.

## The chat

The chat runs in the browser and talks to whatever endpoint the visitor
configures. There is no key in this repository and none is needed to read
the framework. To have the site answer the chat itself, run the server from
the source repository (`tools/web/server.mjs`) behind `/api/`, or point
`PUBLIC_CHAT_API` at a small service that holds the key.
