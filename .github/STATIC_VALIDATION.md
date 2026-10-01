# Static asset integrity and JavaScript syntax

Run from the repository root with Git and Node.js 22:

```sh
node .github/scripts/validate-static.cjs
```

CI checks the generated `index.html` script, link and image references,
`manifest.json` initial/game scripts, `resource/default.res.json` resource URLs,
and image files referenced by Egret font and sprite-sheet descriptors. Local
references must match the case-sensitive Git file list and exist on disk.
Relative and site-root paths are normalized; query strings and fragments are
removed. External URLs, data URLs, anchors and empty dynamic image placeholders
are ignored. Local references outside the asset root fail.

All tracked `.js` files and inline entrypoint scripts are parsed with Node's
JavaScript parser without execution. No packages or Egret SDK are installed.
This validates committed output; it is not a build, unit test, browser test, or
runtime compatibility check. The HTML/CSS extractors cover the simple generated
markup here. Dynamic URLs constructed by application JavaScript are outside
this check.
