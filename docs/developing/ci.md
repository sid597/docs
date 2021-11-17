# Continuous Integration

After each submitted PR to Athens, GitHub Actions runs the continuous integration workflow declared in `.github/workflows/build.yml`. This workflow runs scripts from [`script/`](https://app.gitbook.com/s/-MVghT4Ocm\_YaZ2-l20i-2910905616/community/get-involved/script) to test, lint, and build Athens. You can see these workflows in practice in the [Actions tab](https://github.com/athensresearch/athens/actions/).

However, it's a lot faster if you run these tests locally, so you don't have to submit a PR each time to make sure the workflow succeeds. You may need to install additional dependencies, though.

### Testing

No additional installation is needed. Just run this:

```
lein test
```

The output will look something like this:

```
$ lein test

Testing athens.block-test

Testing athens.parser-test

Testing athens.patterns-test

Ran 4 tests containing 16 assertions.
0 failures, 0 errors.
```

### Linting

We are linting Clojure code using [clj-kondo](https://github.com/borkdude/clj-kondo). Our clj-kondo configuration is in [`.clj-kondo/config.edn`](https://app.gitbook.com/s/-MVghT4Ocm\_YaZ2-l20i-2910905616/community/get-involved/.clj-kondo/config.edn).

For this linting to work, you will need to install `clj-kondo`. Instructions are in [`clj-kondo`’s installation guide](https://github.com/borkdude/clj-kondo/blob/master/doc/install.md).

To see the problems reported by clj-kondo, run `script/lint`. Example run:

```
$ script/lint
linting took 257ms, errors: 0, warnings: 0
```

Your editor may also be able to integrate with clj-kondo’s output. For example, if you use [Calva](https://marketplace.visualstudio.com/items?itemName=betterthantomorrow.calva) for VS Code, then clj-kondo’s messages are reported in the Problems panel.

### Clojure Styling

To format your code or check that your code is formatted correctly, you will need to use `cljstyle`. Instructions for installing it are [in `cljstyle`’s README](https://github.com/greglook/cljstyle/tree/master#installation).

To check if your Clojure code is formatted correctly, run `cljstyle check`. If there is no output and the return code is zero, you’re good. You can also run `script/style`, but currently it only works if you’re running Linux.

To reformat all your Clojure files in place, run `cljstyle fix`.

### Unused Variable Checking

To set this up, first make sure that a global `clojure` binary is installed. You won’t necessarily have a `clojure` binary installed just because you installed Leiningen.

Next, just run `script/carve`. The first time you run it it will download [Carve](https://github.com/borkdude/carve) as a dependency, which takes about a minute and outputs lots of messages. On subsequent runs `script/carve` won’t output anything unless an unused variable was found.

