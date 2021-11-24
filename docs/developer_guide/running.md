# Running Athens Locally

[Video version of this for Mac](https://www.loom.com/share/63618f2a2b2249e3923577fb88fabfdc).

These dependencies are needed to get Athens up and running. To install them, follow the instructions in the links.

1. [Java 11 and Leiningen](https://purelyfunctional.tv/guide/how-to-install-clojure/) (Leiningen installs Clojure)
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
lein dev
```

In another terminal, run:

```
yarn run electron .
```

Another window should open automatically. That's your Athens!

Now make sure you can run code in a REPL and that you know how to use re-frame-10x.

### Running in Docker

Docker doesn't work perfectly well anymore, because we are using Electron. Electron requires access to local resources such as `resources/index.html`.

If you run `yarn run electron .` from your local system, but are running Athens from within Docker, it won't work. Furthermore, if you run `yarn run electron .` from within your Docker system, the GUI won't popup on your local system. The workaround would be to sync the `resources/` files from Docker to a local folder.

The following command runs Athens in a docker container, but does not provide a workaround to actually run Electron.
```
docker build -t athens .
docker run -it -p 3000:3000 -p 8777:8777 -p 9630:9630 athens
```
Soon, we will have the web build of Athens working again, such that users can run the Athens backend and frontend from Docker, such that users can easily develop on the frontend while keeping all dependencies inside the container, and won't need Electron.
