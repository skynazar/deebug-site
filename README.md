# deebug.io

Source for the site at [deebug.io](https://deebug.io) — a single static page, no JS,
no external requests, inline CSS.

Hosted on **Firebase Hosting** (project `deebug-io`). Response headers, including
`Content-Security-Policy: default-src 'none'`, are set in `firebase.json`.

```sh
firebase deploy --only hosting --project deebug-io
```

This repo is a public mirror. It is not the deploy source — deploys run from a local
working copy, so a change here does not go live on its own.
