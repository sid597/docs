# REPL

The REPL is one of the core features of Clojure. REPL-driven programming can make you code faster, with less tests and bugs. This [video](https://vvvvalvalval.github.io/posts/what-makes-a-good-repl.html#what\_does\_a\_good\_repl\_give\_you?:\~:text=What%20does%20a%20good%20REPL%20give%20you%3F,-The) demonstrates this.

* Make sure you can run Athens locally before proceeding with this section.
* Refer to shadow-cljs [editor integration docs](https://shadow-cljs.github.io/docs/UsersGuide.html#\_editor\_integration) for more details.
* nREPL port is 8777, as defined in [shadow-cljs.edn](https://app.gitbook.com/s/-MVghT4Ocm\_YaZ2-l20i-2910905616/community/get-involved/shadow-cljs.edn).

### Cursive

[https://www.loom.com/share/a2cc5f36f8814704948a57e8277c04e9](https://www.loom.com/share/45d7c61703324089a425a9c91b14445b)

### CIDER

[Video tutorial](https://www.loom.com/share/a2cc5f36f8814704948a57e8277c04e9)

### Calva

```
Editor - Visual Studio Code
Calva plugin: v2.0.126 Built on: 2020-07-09
OS - Windows 10, MacOS Catalina v10.15.6
```

1. In VS Code, run `ctrl+shift+c` and `ctrl+shift+j` (`ctrl+alt+c ctrl+alt+j` in Windows 10) to jack into a repl session.
2. Pick shadow-cljs.
3. Select `:main` and `:renderer` profile for shadow-cljs to watch.
4. Select the `:renderer` build to connect to.
5. In another terminal tab, run `npx electron .`

### Vim Plugins

* [ ] TODO vim-iced
* [ ] TODO conjure
* [ ] \[X] TODO fireplace

#### Fireplace

[Fireplace](https://github.com/tpope/vim-fireplace) is a popular Clojure(script) development plugin for Vim (and Neovim) text editor. It's main dependency is the [cider-nrepl](https://github.com/clojure-emacs/cider-nrepl) which already included as a development dependency.

Assume you already executed the commands described above in different terminal sessions and have the Athens instance running. And of course assume you installed vim-fireplace plugin too.

```
lein dev # in one terminal, running nrepl server on port 8777
yarn run electron . # another terminal running the Athens app itself
```

Now open any Clojure file in Vim. This will load vim-fireplace plugin and necessary commands. First, we need to connect Clojure (not Clojurescript yet) runtime;

```
:FireplaceConnect 8777
```

Clojure part is done. Now to connect Clojurescript runtime with vim-fireplace;

```
:Piggieback :renderer
```

To test your development environment you can try to evaluate some Clojurescript and see the results on Athens running in electron;

```
:CljsEval (js/alert "hello!")
```

You supposed to see an alert on electron app saying "hello!" and your Vim instance would be blocked until you acknowledge the alert message.

If all goes well, now you can see documentation of symbols (binding: K), go to definition (binding: \[ C-d) and so fort. See `:help fireplace` for more information.

#### Conjure

[Conjure](https://github.com/Olical/conjure) is an interactive environment for evaluating code within your running program for Neovim. [Installing Conjure](https://github.com/Olical/conjure#installation)

Its main dependency is the [cider-nrepl](https://github.com/clojure-emacs/cider-nrepl). Create the following file at `~/.shadow-cljs/config.edn` to add the dependency:

```
{:dependencies
 [[cider/cider-nrepl "0.26.0"]]}
;; this version may be out of date, check whichever is available
```

See [shadow-cljs docs](https://shadow-cljs.github.io/docs/UsersGuide.html#user-config) for more info.

Now that we're set up, lets start the development environment;

```
lein dev # in one terminal, running nrepl server on port 8777
yarn run electron . # another terminal running the Athens app itself
```

Open any Clojurescript file in Neovim. Conjure will connect automatically to the leiningen nrepl server and you should see a temporary floating buffer in the top right corner of your editor showing a successful connection.

To get that buffer back and to keep it open in a horizontal split:

```
:ConjureLogSplit
```

To connect to the Clojurescript runtime;

```
:ConjureShadowSelect renderer
```

In the log buffer you should see;

```
; --------------------------------------------------------------------------------
; shadow-cljs (select): renderer
; (out) To quit, type: :cljs/quit
[:selected :renderer]
```

To test your development environment you can try to evaluate some Clojurescript and see the results on Athens running in electron;

```
:ConjureEval (js/alert "hello!")
```

You should see an alert in the electron app saying "hello!". All further evaluations will be blocked until you acknowledge the alert message.

Congratulations, you're connected!

To learn more about how to evaluate things with Conjure, please refer to `:help conjure`, `:help conjure-client-clojure-nrepl` and `:ConjureSchool` (an interactive tutorial). See also: \[Conjures quickstart guide to Clojurescript]\([https://github.com/Olical/conjure/wiki/Quick-start:-ClojureScript-(shadow-cljs](https://github.com/Olical/conjure/wiki/Quick-start:-ClojureScript-\(shadow-cljs))) and [Clojure](https://github.com/Olical/conjure/wiki/Quick-start:-Clojure)

