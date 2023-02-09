# Install Clojure CLI

![Clojure CLI Logo](https://raw.githubusercontent.com/practicalli/graphic-design/live/logos/practicalli-clojure-cli-logo.png){align=right loading=lazy style="height:150px;width:150px"}

Install the Clojure CLI which provides the essential tools for Clojure development.

The Clojure CLI automatically downloads all library dependencies, including the Clojure Standard library.

As Clojure itself is packages as a library (`.jar` Java ARchive), any version of Clojure can easily be used with a project or the Clojure CLI tool.


=== "Linux"

    Practically recommends setting `XDG_CONFIG_HOME` to the `.config` directory, to avoid creating another dot directory in the root of the user account.  Add the following to `~/.bashrc` for the bash shell or `~/.zshenv` for Zsh.

    ```
    export XDG_CONFIG_HOME="$HOME/.config"
    ```

    Use the Linux script installer from [Clojure.org - Getting Started](https://clojure.org/guides/getting_started#_installation_on_linux)

    The instructions should be as follows, possibly with a newer version

    ```bash
    curl -O https://download.clojure.org/install/linux-install-1.11.1.1208.sh
    chmod +x linux-install-1.11.1.1208.sh
    sudo ./linux-install-1.11.1.1208.sh
    ```

    The installation creates `/usr/local/bin/clojure`, `/usr/local/bin/clj` wrapper and `/usr/local/lib/clojure` directory.


=== "Homebrew"

    Practically recommends setting `XDG_CONFIG_HOME` to the `.config` directory, to avoid creating another dot directory in the root of the user account.  Add the following to `~/.bashrc` for the bash shell or `~/.zshenv` for Zsh.
    ```
    export XDG_CONFIG_HOME="$HOME/.config"
    ```

    Use the Homebrew command with the [clojure/tools tap](https://github.com/clojure/homebrew-tools), as defined in the [Clojure.org Getting started guide](https://clojure.org/guides/getting_started#_installation_on_linux)

    ```bash
    brew install clojure/tools/clojure
    ```

    Use Homebrew to update an install of Clojure CLI to the latest release
    ```bash
    brew upgrade clojure/tools/clojure
    ```

    > [Homebrew on Linux or Windows with WSL](https://docs.brew.sh/Homebrew-on-Linux)

=== "Windows"

    For Windows 10 use [Windows Subsystem for Linux and Windows Terminal are recommended](https://conan.is/blogging/clojure-on-windows.html) if you have administrative privileges and are comfortable using a Unix system on the command line.

    Alternatively install [scoop.sh](https://scoop.sh/), a command line installer for windows.  [Powershell 5](https://aka.ms/wmf5download) or greater is required. Follow the [scoop-clojure getting started guide](https://github.com/littleli/scoop-clojure/wiki/Getting-started), summarized here:

    Open "Windows PowerShell" and enter the following commands to configure the shell:

    ```bash
    iwr -useb get.scoop.sh | iex
    Set-ExecutionPolicy RemoteSigned -Scope CurrentUser -Force
    ```
    Then in the same PowerShell window, install the Clojure related tools using the following commands:

    ```bash
    scoop bucket add extras
    scoop bucket add java
    scoop bucket add scoop-clojure https://github.com/littleli/scoop-clojure
    scoop install git 7zip pshazz temurin-lts-jdk clj-deps leiningen clj-kondo vscode coreutils windows-terminal
    ```


> Reference: [Clojure CLI Install - Clojure.org Getting Started](https://clojure.org/guides/install_clojure){target=_blank} - official guide


## Practicalli Clojure CLI Config

Add a wide range of community tools to extend the capabilities of Clojure CLI via the aliases contained within Practicalli Clojure CLI configuration.

Fork or clone [Practicalli Clojure CLI Config](https://github.com/practicalli/clojure-deps-edn){target=_blank} GitHub repository, first removing the `$XDG_CONFIG_HOME/clojure` or `$HOME/.clojure` directory if they exist.

??? HINT "Check Clojure CLI configuration location"
    Check the location of your Clojure configuration directory by running `clojure -Sdescribe` and checking the `:user-config` value.


=== "Free Desktop XDG CONFIG"
    If `XDG_CONFIG_HOME` environment variable is set, clone the repository to `$XDG_CONFIG_HOME/clojure`

    Via SSH
    ```shell
    git clone git@github.com:practicalli/clojure-deps-edn.git $XDG_CONFIG_HOME/clojure
    ```

    Via HTTPS:
    ```shell
    git clone https://github.com/practicalli/clojure-deps-edn.git $XDG_CONFIG_HOME/clojure
    ```

=== "Classic Config"
    Clojure CLI will look for its configuration in `$HOME/.clojure` directory if `$XDG_CONFIG_HOME` and `CLJ_CONFIG` environment variables not set.
    Via SSH
    ```shell
    git clone git@github.com:practicalli/clojure-deps-edn.git $HOME/.clojure
    ```

    Via HTTPS
    ```shell
    git clone https://github.com/practicalli/clojure-deps-edn.git $HOME/.clojure
    ```


## Check Configuration

`clojure -Sdescribe` shows the version of Clojure CLI installed and configuration locations used.

```bash
clojure -Sdescribe
```

The output of the command includes the version of Clojure CLI in the `:version` key

```bash
{:version "1.11.1.1208"
 :config-files ["/usr/local/lib/clojure/deps.edn" "/home/practicalli/.config/clojure/deps.edn" ]
 :config-user "/home/practicalli/.config/clojure/deps.edn"
 :config-project "deps.edn"
 :install-dir "/usr/local/lib/clojure"
 :config-dir "/home/practicalli/.config/clojure"
 :cache-dir "/home/practicalli/.cache/clojure"
 :force false
 :repro false
 :main-aliases ""
 :repl-aliases ""}
```

> `clojure -Sversion` will shows the version of Clojure CLI being when the `clojure` command is used to run a REPL or other Clojure command.


## Optional rlwrap readline

The `rlwrap` binary is a basic readline tool that provides a history of commands entered into a terminal UI when running a Clojure REPL with the `clj` wrapper script.

Pressing the ++arrow-up++ and ++arrow-down++ keys will scroll through the code previously entered in the REPL.

`rlwrap` is available with most Linux systems. Look for  install instructions by searching for rlwrap in a web browser or build from source from the [rlwrap GitHub repository](https://github.com/hanslub42/rlwrap).

!!! HINT "Use Rebel Readline for a rich terminal UI experience"
    [rebel readline](/clojure/clojure-cli/repl/) provides a auto-completion, documentation, signature help and multi-line editing all within a terminal UI, providing a much richer experience than the `clj` wrapper and `rlwrap`.

    Rebel Readline is part of the [Practicalli Clojure CLI config](#practicalli-clojure-cli-config).
