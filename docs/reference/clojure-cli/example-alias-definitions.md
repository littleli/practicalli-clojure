# Clojure Tools - Common alias definitions


<!-- TODO: refactor clojure CLI example aliases  -->

## Task: Run a simple terminal REPL
`clojure` and `clj` (requires rlwrap) will run a REPL if given no other arguments.

Running either command from the root directory of a project will merge the `deps.edn` configuration with `~/.clojure/deps.edn`.


## Task: Run a REPL with additional dependencies and paths
`clojure -M:alias` will run a repl if the alias does not contain a main namespace defined in `:main-opts`, e.g. `:main-opts ["-m" "namespace.main"]`.  The deps and path values are included from the alias.

If the following alias is defined in the project `deps.edn` file

```clojure
:env/dev
{:extra-paths ["resources"]
 :extra-deps {com.h2database/h2 {:mvn/version "1.4.200"}}}
```
`clojure -M:env/dev` will add `resources` directory to the path and the h2 database library to the dependencies, then runs a REPL.

Including the `-r` option in the command line forces a REPL to run, even if a main namespace is provided via `:main-opts` or the command line.

```clojure
clojure -r -M:alias1:alias2
```
The dependencies and paths will be merged from the alias from left to right, with each successive alias over-riding the value of any matching keys in the dependencies.


## Task: Create a new project from template
The `clj-new` community tool can be used to create a Clojure / ClojureScript project, using a template to provide a project structure and example source code and tests.

Using the `:main-opts` approach, an alias for `clj-new` would be defined as follows

```clojure
  :project/new
  {:extra-deps {seancorfield/clj-new {:mvn/version "1.0.215"}}
   :main-opts  ["-m" "clj-new.create"]}
```

The `clj-new` tool can be run using the `-M` flag, passing the template and project names as arguments.

`clojure -M:project/new template-name project-domain/application-name`

To create a project as an application (to be run via the command line) for the practicalli domain with the application called banking-on-clojure

```bash
clojure -M:new app practicalli/banking-on-clojure
```

The latest version of the `clj-new` project also supports using the `-X` flag and default arguments.

Adding the `:exec-fn` to the `clj-new` alias, the `-X` flag can be used instead of the `-M`.  Arguments are supplied as key/value pairs

```clojure
  :project/new
  {:extra-deps {seancorfield/clj-new {:mvn/version "1.1.215"}}
   :exec-fn clj-new/create}
```
Use this alias with the `-X` flag

```bash
clojure -X:project/new :template template-name :name practicalli/banking-on-clojure
```

Default values can be added using the `:exec-args` key to the alias

```clojure
:project/new
{:extra-deps {seancorfield/clj-new {:mvn/version "1.1.215"}}
 :exec-fn clj-new.create
 :exec-args {:template lib :name practicalli/playground}}
```
`clojure -M:project/new :name practicalli/awesome-webapp` will create a new project using the `{:template lib :name practicalli/awesome-webapp}` argument.



## Task: Executing a specific function
Clojure can run a specific function, useful for one off tasks or timed batch processing (via cron or similar tool) as well as complete applications.

Arguments to the function are passed as a hash-map, defined in either an aliases `:exec-args` key or as key value pairs on the command line.  Command line key value pairs are merged with the `:exec-arg` hash-map, replacing the values from the command line if there are matching keys.

**Scenarios**

`clojure -X namespace/fn` runs the function specified on the command line, passing an empty hash-map as an argument

`clojure -X:alias fn` runs the function if the `:ns-default` is set to the namespace that contains the function, otherwise "Unqualified function can't be resolved: fn-name" error is returned.

`clojure -X:alias` runs the function specified by `:exec-fn` in the alias.  The function must include its namespace or have that namespace defined in `:ns-default`. If `:exec-args` is defined in the alias, its value is passed to the function, otherwise an empty hash-map is passed to the function as an argument.

`clojure -X:alias namespace/fn` will run the function specified on the command line, over-riding `:exec-fn` if it is defined in the alias.  `:exec-args` will be passed to the command line function if defined in the alias. Dependencies and paths will be used from the alias. Assumption: the command line namespace also overrides the `:ns-default` value if set.

`clojure -X:alias :key1 val1 :key2 val2` will execute the function defined in `:exec-fn` and pass it the key value pairs from the command line as a hash map.  If the alias has `:exec-args` defined, command line args are merged into the `:exec-fn` hash-map, replacing the default values in `:exec-args` where keys match.

Assuming there is an alias called `database/migrate` defined in the project `deps.edn`

```clojure
:database/migrate
{:exec-fn practicalli.banking-on-clojure.database/migrate
 :exec-args {:db-type "h2" :database "banking-on-clojure"}}
```

`clojure -X:database/migrate :database "specs-repository"` would merge the command line args with `:exec-args` to create the hash-map `{:db-type "h2" :database "specs-repository"}` which is passed to the `practicalli.banking-on-clojure.database/migrate` function as an argument.


## Task: Executing a range of functions

`:ns-default` in an alias defines the namespace that contains the functions that could be executed.

```clojure
{:aliases
  {:project/run
    {:ns-default practicalli/banking-on-clojure}}}
```
Specific functions from the namespace can be called via the command line

```bash
clojure -X:project/run migrate-db :db-type h2 :database banking-on-clojure
clojure -X:project/run server-start :port 8080
```


## Task: Dry Run or Prepare for CI / Containers
`clojure -P` will download the libraries defined in `:deps` in the project `deps.edn` and do nothing else.  Standard out shows downloading of dependencies not already cached locally, including name and versions and repository downloaded from.

![Clojure CLI tools - using -P flag to download project dependencies](/images/clojure-cli-tools-dependencies-p-flag.png)

> #### Hint::Qualified namespaces required
> If an unqualified library name is used, e.g. `compojure`, then a warning is sent to the standard out.  Change the name of the library to be fully qualified e.g. `weavejester/compojure`
>
>In a future version of the Clojure CLI tools unqualified namespaces will not be downloaded.

The `-P` flag can be used to modify an existing command to ensure no execution takes place, ensuring a prepare only (dry run) action.

`clojure -P -M:alias-name` downloads the dependencies for the specific aliases and multiple aliases can be chained together, e.g. `clojure -P -M:env/dev:test-runner/kaocha`

The `-P` flag uses everything from an alias not related to execution.

> The classic way to download deps was to run `clojure -A:aliases -Spath`, where `-Spath` prevented execution of repl or main.


## Run a Clojure application
`clojure -m full.namespace.to.dash-main` calls the `-main` function from the given namespace. Arguments to the function are simply added to the end of the command line and passed to the `-main` function in the given namespace.

> The `-m` flag in the CLI tools pre-release returns a warning that `-M` should be used.

Using `-M` and `-m` works, but seems redundant.  Using `-M` by itself runs the REPL.
```bash
clojure -M -m full.namespace.to.dash-main
```

`-M` seems useful when including an alias with extra configuration (eg. `:extra-deps`, `:extra-paths`, `:main-opts`).  As `:main-opts` is no different to the `-m` option, creating an alias just to avoid the warning seems excessive.



## Task: Executing a project - using Edn style args
Clojure CLI tools is encouraging a move to functions that take a hash-map for their arguments.  Passing arguments in as an edn data structure has more rigor than options and strings on the command line.

The simplest form is to define an alias to run the project, specifying just the function to execute using `:exec-fn`
```clojure
 :aliases
 {:project/run
   {:exec-fn practicalli.banking-on-clojure/server-start}
 } ;; End of Aliases
```
Then the project can be run using this alias.

```bash
clojure -X:project/run
```

Arguments can be passed to the function as key/value pairs on the command line.

```bash
clojure -X:project/run  :port 8080 :host "localhost"
```


`:exec-args` provides a way to define default arguments for the function, regardless of if it is defined in `;:exec-fn` or passed via the command line.

`:exec-args` defines a hash-map of arguments so the function must support taking a hash-map as an argument.

> A function may take variable args, especially if it is supporting both hash-maps and strings as options.


```clojure
 :aliases
 {:project/run
   {:exec-fn fully.qualified/namespace
    :exec-args {:default "arguments" :can-be-over-ridden-by "command-line-args"} }
 } ;; End of Aliases
```

Adding `:exec-args` to the `:run-project`

```clojure
 :aliases
 {:project/run
   {:exec-fn practicalli.banking-on-clojure/server-start
    :exec-args {:port 8888 :host "localhost"}}
 } ;; End of Aliases
```



#### Example of running a Clojure project - hello-world
In this example I use the hello-world example from https://clojure.org/guides/deps_and_cli#_writing_a_program
A project `deps.edn` file was created containing the dependency for clojure.java-time and the source code from that page copied into `src/hello.clj`

`clojure -m` hello runs the project and returns the time from running the -main function.
However this gives a warning:
```bash
WARNING: When invoking clojure.main, use -M
```

`clojure -M` runs a REPL

`clojure -M -m hello` runs the project and returns the time.  But then I ask myself what is the purpose of -M

Creating an alias to run the project seems an interesting idea, as I could also set default arguments.

Adding an `:project-run` alias to the project `deps.edn` works when calling with clojure `-M:project-run`
```clojure
 :aliases
 {:project-run {:main-opts ["-m" "hello"]}}
```

Changing the `:project-run` alias to use `:exec-fn` and a fully qualified function (-main by default) should work when calling with `clojure -X:project-run`.
 :aliases
 {:run-project {:exec-fn hello]}}

However, the `hello-world` project has an unqualified function and cannot be resolved.

Moving the source code to `src/practicalli/hello.clj` and calling `clojure -X:run-project` gives an execution error, `(ArityException)` as the `-main` function does not take any arguments, `(defn -main [] ,,,)`.

Changing the `-main` function to `(defn -main [& args] ,,,)` fixes the arity exception and calling `clojure -X:run-project` works.



## Local Maven install
Install a jar into the local Maven cache, typically `~/.m2/repository/` directory, organised by groupId

```clojure
clojure -M:deps mvn-install :jar '"/path/to.jar"'
```
> edn strings must be in double quotes, and then single-quoted for the shell

`mvn-install` uses the `.pom` file contained in the jar (if it exists) to determine the _groupId_, _artifactId_, and _version coordinates_ to use when the jar is installed.

The `.pom` file can also be specified using the  `:pom` argument.

The install argmap takes the following options:

| key           | Required | Description                                            |
|---------------|----------|--------------------------------------------------------|
| `:jar`        | required | path to the jar file to install                        |
| `:pom`        | optional | path to .pom file (if .jar file does not contain .pom) |
| `:lib`        | optional | qualified symbol e.g `my.org/lib`                      |
| `:version`    | optional | Version number of library (string type)                |
| `:classifier` | optional | (string type)                                          |
| `:local-repo` | optional | path to local repo (default = ~/.m2/repository)        |


**mvn-install - define default configuration - using in templates for example**
Rather than pass details via the command line, use an alias to pass in default arguments.  This is especially useful when the project deps.edn is generated from a template.


> TODO: Is it possible to define `:exec-args` with the built-in `-X:deps mvn-install` command?

An alias can be defined in the project `deps.edn` file including default arguments via `:exec-args`

```clojure
{:aliases
 {:deploy/local-install
  {:exec-fn clojure.tools.deps.alpha.tools.install/install
  :exec-args {:jar "./project-name.jar" :pom "./project-name.pom"}
  }}}
```
Install the jar using the default arguments using the command:

```bash
clojure -X:deploy/local-install
```


**How it works**
`clojure.tools.deps.alpha.tools.install/install` is a function to install a jar into the local Maven cache, i.e. `~/.m2/repository`. An alias called `:deps` is built into Clojure CLI tools and includes the `tools.deps.alpha` library on the classpath,

`:exec-args` optionally includes a hash-map of key/values options that can also be passed on command line
