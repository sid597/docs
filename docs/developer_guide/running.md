# Running Athens Locally

These dependencies are needed to get Athens up and running. To install them, follow the instructions in the links.

1. [Java 11 and Clojure](https://clojure.org/guides/getting_started#_clojure_installer_and_cli_tools)
2. [Node 12](https://nodejs.org/en/download/) and [Yarn](https://classic.yarnpkg.com/en/docs/install/#mac-stable)

_If you want to use Windows Subsystem for Linux (WSL),_ [_try this tutorial_](https://www.notion.so/Beginner-Clojure-Environment-Setup-Windows-36f70c16b9a7420da3cd797a3eb712fa#6a53854de58d4f07ba6319d868fba29c)_._

After you've got these dependencies, clone the Git repository to your hard drive:

```
git clone https://github.com/athensresearch/athens.git
```

Then `cd athens/` and run the following commands.

Pull JavaScript dependencies:

```
yarn
```

Pull Java dependencies and build, then start a local HTTP server for Athens:

```
yarn dev
```

In another terminal, run:

```
yarn client:electron
```

Another window should open automatically. That's your Athens!

Now make sure you can run code in a REPL and that you know how to use re-frame-10x.

