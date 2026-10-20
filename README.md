# The Collabior Process Framework — published site

This repository holds the **built** browser application for the Collabior
Process Framework. The source — the framework itself, the toolchain that
compiles it, and the tests that check it — lives in
[`Yvan-git/ProcessFrameworkAI`](https://github.com/Yvan-git/ProcessFrameworkAI),
which stays private.

The build is pushed here by the `publish-site` workflow in the source
repository, and published to GitHub Pages by the workflow in this repository.

## Live

- **Pages:** <https://yvan-git.github.io/ProcessFrameworkAI-site/>
- **Custom domain:** add a `CNAME` file containing `framework.collabior.com`
  to the root of this repository, and point the DNS at GitHub. The site is
  built for the root of its hostname, so it works unchanged at either address.

## Serving it somewhere else

This repository is a complete static site. Clone it into a web root and it
works:

```bash
git clone https://github.com/Yvan-git/ProcessFrameworkAI-site.git public_html/framework.collabior.com
```

- `index.html`, `200.html` and `404.html` are the same single-page
  application shell. Apache and nginx serve `index.html` for `/`; the
  `.htaccess` rewrites unknown paths to `200.html`; GitHub Pages serves
  `404.html` for a path that does not exist.
- `framework/` holds the compiled framework as JSON — the map, the documents,
  the policies, the skills, the templates.
- `_app/` holds the hashed JavaScript and CSS. Do not rename or re-compress
  these files; their names carry a content hash.

Note that the build published here is compiled for the `/ProcessFrameworkAI-site`
prefix, so it is meant to be served from that path. To serve it from the root
of a hostname instead, rebuild with `BASE_PATH=` (empty) — see the source
repository.

## The chat

The chat runs in the browser and talks to whatever endpoint the visitor
configures. There is no key in this repository and none is needed to read
the framework. To have the site answer the chat itself, run the server from
the source repository (`tools/web/server.mjs`) behind `/api/`.
