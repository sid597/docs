# Continuous Integration

After each submitted PR to Athens, GitHub Actions runs the continuous integration workflow declared in `.github/workflows/build.yml`. This workflow runs scripts from `package.json` to test, lint, and build Athens. You can see these workflows in practice in the [Actions tab](https://github.com/athensresearch/athens/actions/).

However, it's a lot faster if you run these tests locally, so you don't have to submit a PR each time to make sure the workflow succeeds.


### Testing

No additional installation is needed. Just run this:

```
yarn client:test
yarn server:test
```

The first command runs tests for the client code, and the second runs tests for the server code.

```
$ yarn test

... lots of logging

Testing athens.patterns-test

Testing athens.walk-test
13:55:53.824 DEBUG [main] athens.walk - walk-string {:node/titles ("hey"), :page/refs ([:node/title "hey"])}
13:55:53.824 DEBUG [main] athens.walk - walk-string {:node/titles ("hola"), :page/refs ([:node/title "hola"])}
13:55:53.825 DEBUG [main] athens.walk - walk-string {:node/titles ("aloha"), :page/refs ([:node/title "aloha"])}
13:55:53.825 DEBUG [main] athens.walk - walk-string #:block{:refs ("uid123")}

Testing event-sync.core-test

Ran 70 tests containing 606 assertions.
0 failures, 0 errors.
✨  Done in 6.36s.
```


### Linting

We are linting Clojure code using [clj-kondo](https://github.com/borkdude/clj-kondo). 
Our clj-kondo configuration is in `.clj-kondo/config.edn`.

To see the problems reported by clj-kondo, run `yarn lint`. Example run:

```
$ yarn lint
yarn run v1.22.17
$ clojure -M:clj-kondo --lint src
linting took 1549ms, errors: 0, warnings: 0
✨  Done in 6.85s.
```

Your editor may also be able to integrate with clj-kondo’s output. For example, if you use [Calva](https://marketplace.visualstudio.com/items?itemName=betterthantomorrow.calva) for VS Code, then clj-kondo’s messages are reported in the Problems panel.


### Clojure Styling

To check if your Clojure code is formatted correctly, run `yarn style`. If there is no output and the return code is zero, you’re good. 

To reformat all your Clojure files in place, run `yarn style:fix`.


### Unused Variable Checking

Run `yarn carve` to get a report of unused variables. `yarn carve:interactive` will start an interactive prompt that lets you remove or ignore unused code.

