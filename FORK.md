# Adnova fork

Upstream tags GitHub releases but has not published to npm since 24.0.1, and the
tags don't contain a built `dist/`. This fork commits the build so services can
depend on it straight from GitHub:

    "facebook-nodejs-business-sdk": "github:Adnova-AI/facebook-nodejs-business-sdk#v26.0.2-dist"

Only `dist/cjs.js` (the package `main`) and `dist/es.js` are committed.

## Rebuilding for a new upstream release

    git fetch upstream --tags
    git switch -c adnova-dist-vXX upstream/vXX.Y.Z   # or rebase this branch
    npm install --ignore-scripts
    npx gulp dist
    git add -f dist/cjs.js dist/es.js FORK.md
    git commit -m "Add built dist for vXX.Y.Z"
    git tag vXX.Y.Z-dist && git push origin HEAD vXX.Y.Z-dist
