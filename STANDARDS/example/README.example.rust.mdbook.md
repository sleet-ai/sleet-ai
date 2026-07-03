# project

one line description

---

### Dev and Build

```sh
# serve
mdbook serve
mdbook serve --open

# build
mdbook build

# test code samples
mdbook test

# cargo (preprocessors / plugins)
cargo check
cargo test
cargo fmt
cargo update
```

### Publish

```sh
# build and deploy to gh-pages
mdbook build
cp -r book/* docs/

# netlify
# commonprefix-project
netlify deploy
netlify deploy --prod
```

==================
<br/>
copyright 2026 by sleet.near
