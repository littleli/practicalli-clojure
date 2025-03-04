# Editors for Clojure development

The best editor to use for learning Clojure is the editor already familiar with (or want to learn).

Use SublimeText & ClojureSublimed if unsure where to start as it will be the simplest tool to use.


## Clojure editor features

An ideal Clojure editor includes the these core features

* running / connecting to a REPL process
* evaluation results inline or in a repl window (fast feedback on what the code does)
* syntax highlighting (including highlight of matching parens)
* structural editing to ensure parens are balanced when writing and refactor code
* data inspector to visualise large and nested data, or connection to ([external data inpector tools](/clojure/data-inspector/))

![Clojure REPL driven development with Clojure aware editors](https://raw.githubusercontent.com/practicalli/graphic-design/live/clojure/clojure-repl-driven-development-clojure-aware-editor.png)


## Clojure aware editors

Emacs (Spacemacs, Doom, Prelude), Neovim (Conjure) and VSCode (Calva) are the most common open source Editors for Clojure and ClojureScript development.

SublimeText and IntelliJ are commercial editors (with limited free editions) which also provide Clojure support


=== "Emacs"
    Emacs is a very powerful editor with thousands of packages enabling a person to do almost any digital task concievable.  Emacs is highly extensible via the ELisp programming language used to write configuration and the numerous Emacs packages.

    Use one of the popular community configurations for Emacs or visit the CIDER documentation to learn how to add Clojure support to Emacs.

    Emacs 28 onward uses Native Compilation of Emacs packages, dramatically speeding up many common tasks and keeping Emacs a valuable option for development (and everything else).

    Emacs uses CIDER and Clojure LSP for a feature rich clojure development experience.

    === "Spacemacs"
        [Spacemacs](https://spacemacs.org/){target=_blank} is a community configuration bringing [Emacs](https://www.gnu.org/software/emacs/){target=_blank} features and [Vim sytle editing](https://practical.li/spacemacs/spacemacs-basics/evil/){target=_blank} together.  Spacemacs uses a mnemonic menu system that makes it easy to learn and provides detailed documentation for configuring and using Emacs.

        [Practicalli Spacemacs](https://practical.li/spacemacs){target=_blank} provides a guide to Clojure development, vim-style editing, documenting with org-mode, Git version control with Magit, Issues & Pull Requests with Forge and dozens of other features.

        [practicalli/spacemacs.d repository](https://github.com/practicalli/spacemacs.d){target=_blank} contains a customised configuration for Clojure development and supporting tools. [Browse the repository online](https://github.com/practicalli/spacemacs.d){target=_blank} or fork / clone the repository

        === "Free Desktop XDG Config"
            ```bash
            git clone https://github.com/practicalli/spacemacs.d.git $XDG_CONFIG_HOME/spacemacs`
            ```

        === "Classic Config"
            ```bash
            git clone https://github.com/practicalli/spacemacs.d.git $HOME/.spacemacs.d`
            ```

        The Practicalli configuration should replace the `~/.spacemacs` file if it exists

        [Spacemacs install guide - Practicalli Spacemacs](https://practicalli.github.io/spacemacs/install-spacemacs/){target=_blank .md-button}

        <p style="text-align:center">
        <iframe width="560" height="315" src="https://www.youtube.com/embed/NDrpclY54E0" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </p>

    === "Doom Emacs"
        [Doom Emacs](https://spacemacs.org/){target=_blank} is a community configuration for [Emacs](https://www.gnu.org/software/emacs/){target=_blank} that provides a minimalistic configuration that is readily customisable.  Doom Emacs is most suited to those comming from a Vim-style editing background or simply looking for a lightweight setup with options to extend the configuration.

        [Practicalli Doom Emacs Book](https://practical.li/doom-emacs/){.md-button}

        [practicalli/doom-emacs-config repository](https://github.com/practicalli/doom-emacs-config){target=_blank} contains a customised configuration for Clojure development and supporting tools. [Browse the repository online](https://github.com/practicalli/doom-emacs-config){target=_blank} or fork / clone the repository

        === "Free Desktop XDG Config"
            ```bash
            git clone https://github.com/practicalli/doom-emacs-config.git $XDG_CONFIG_HOME/doom`
            ```
            The Practicalli configuration should replace the `~/.config/doom/` directory created by the `doom install` command.

        === "Classic Config"
            ```bash
            git clone https://github.com/practicalli/doom-emacs-config.git $HOME/.doom.d`
            ```
            The Practicalli configuration should replace the `~/.doom.d/` directory created by the `doom install` command.


        ![Emacs Doom with Practicalli customisations](https://raw.githubusercontent.com/practicalli/graphic-design/live/doom-emacs/doom-emacs-practicalli-dark.png#only-dark)
        ![Emacs Doom with Practicalli customisations](https://raw.githubusercontent.com/practicalli/graphic-design/live/doom-emacs/doom-emacs-practicalli-light.png#only-light)


    === "Prelude Emacs"
         [Emacs Prelude](https://prelude.emacsredux.com/en/stable/) is an easy to use Emacs configuration for Emacs newcomers and lots of additional power for Emacs power users, from the author of [CIDER - the definitive Clojure IDE for Emacs](https://docs.cider.mx/).

         Prelude uses the traditional chorded key bindings to drive Emacs, e.g. ++ctrl+"c"++ ++ctrl+"c"++ to evaluate the current top-level form.

         [Prelude Install Guide](https://prelude.emacsredux.com/en/stable/installation/)

=== "Neovim"
    Neovim is a hyper-extensible text editor that evolved from Vim whist still fully compatible with Vim"s editing model and Vimscript extension language.  Neovim uses lua configuration and with the [aniseed package](https://github.com/Olical/aniseed) configuration and Neovim packages can be written in Fennel (a lisp dialect).

    Neovim is based on multi-model editing (e.g. normal, insert, visual editing states) providing a highly effective tool for writing code, configuration and documentation.

    The Neovim community provides a large number of packages to add features.

    [Conjure](https://github.com/Olical/conjure) is predominantly used for Clojure development and supports Clojure CLI, Leiningen and Babashka projects (as well as several other Lisp dialects and interesting languages)

    [![Neovim and Conjure](https://raw.githubusercontent.com/practicalli/graphic-design/live/banners/neovim-conjure-banner.png)](https://raw.githubusercontent.com/practicalli/graphic-design/live/banners/neovim-conjure-banner.png)

    === "Practicalli Neovim"
        [practicalli/neovim-config-redux](https://github.com/practicalli/neovim-config-redux) is written in Fennel as it is very close to Clojure.

        A Which-key menu can be used to drive Neovim, with a mnemonic set of key bindings to make adoptiong Neovim easier.

        [Conjure](https://github.com/Olical/conjure){target=_blank} provides interactive environment for evaluating Clojure code and providing inline results (or see results in an Heads Up Display or Log buffer).

        [Practicalli Neovim](https://practical.li/neovim/){target=_blank} covers installation and basic use of Neovim for Clojure development.

        [Practicalli Neovim](https://practical.li/neovim/){target=_blank .md-button}

        Older Neovim guides include:

        [Practicalli install guide for neovim and conjure](./editor-install-guides/neovim-conjure/){.md-button}
        [Practicalli user guide for neovim and conjure](./editor-user-guides/neovim-conjure/){.md-button}


        #### Quick try tutorial
        Try the Conjure interactive `:ConjureSchool` tutorial without the need to install, only a recent version of neovim
        ```bash
        curl -fL conjure.fun/school | sh
        ```
        ![Clojure editors - neovim and conjure tutorial](/images/clojure-editors-neovim-conjure-tutorial.png)

        `:q` to quit the tutorial.

        #### References

        [Getting started with Neovim and Conjure](https://oli.me.uk/getting-started-with-clojure-neovim-and-conjure-in-minutes/){target=_blank .md-button}
        [Neovim user guide](https://neovim.io/doc/user/){target=_blank .md-button}
        [Conjure install guide](https://github.com/Olical/conjure){target=_blank .md-button}
        [Conjuring Clojure in Vim](https://blog.djy.io/conjuring-clojure-in-vim/){target=_blank .md-button} - an introduction to using Conjure



    === "SpaceVim"
        [SpaceVim](https://spacevim.org/) is a fully featured vim experience that includes [a simple Clojure development environment](https://spacevim.org/layers/lang/clojure/) based around [vim-fireplace](https://github.com/tpope/vim-fireplace)

        Follow the [Quick Start Guide to instal SpaceVim](https://spacevim.org/quick-start-guide/)

        Add the Clojure layer to the SpaceVim custom configuration file
        ```shell title="~/.SpaceVim.d/init.toml"
        [[layers]]
          name = "lang#clojure"
        ```

        [SpaceVim quick guide](neovim-guide.md)
        [SpaceVim - Clojure Layer](https://spacevim.org/layers/lang/clojure/)
        [SpaceVim quickstart guide](https://spacevim.org/quick-start-guide/){target=_blank .md-button}
        [SpaceVim documentation](https://spacevim.org/documentation/){target=_blank .md-button}


    === "VimIced"
        Clojure Interactive Development Environment for Vim8/Neovim.

        [vim-iced documentation](https://liquidz.github.io/vim-iced/){target=_blank .md-button}

        [![Clojure Interactive Development Environment for Vim8 / Neovim](https://raw.githubusercontent.com/liquidz/vim-iced/master/doc/pages/assets/logo.svg)](https://github.com/liquidz/vim-iced){target=_blank .md-button}


=== "VSCode"
    [VS Code](https://code.visualstudio.com/) is a freely available editor build on open source and available for Linux, MacOS and Microsoft Windows.

    VS Code has a large marketplace of extensions, proiding additional tools for a complete development environment.

    Calva is the most commonly used extension for Clojure support and aims to provide similar features to Emacs Cider (and uses some of the same Clojure libraries).

    VSpaceCode provides a mnemonic menu (which-key) to drive VS Code by keyboard alone, vim editing and rich Git client (edamagit).  VSpaceCode extension also provides key bindings for common Calva commands.  Users experienced with Neovim and Emacs (Spacemacs / Doom) will find this extension makes VS Code easiter to use than vanilla VS Code or VS Code with an Neovim backend.

    Clover provides a more mininal environment using Socket REPL.


    === "Calva"
        The Calva extension adds Clojure support to Microsoft VS Code editor.

        [Calva - VS Code Marketplace](https://marketplace.visualstudio.com/VSCode){target=_blank .md-button}

        Calva is under active development and the [#calva channel on the Clojurians Slack community](clojurians.slack.com/messages/calva) can be supportive.

        [Calva Getting Started Guide](https://calva.io/getting-started/){target=_blank .md-button}
        [VSCode Calva extension](https://marketplace.visualstudio.com/items?itemName=betterthantomorrow.calva){target=_blank .md-button}
        [VSCode Getting Started Guide](https://code.visualstudio.com/docs/introvideos/basics)

        <p style="text-align:center">
          <iframe width="560" height="315" src="https://www.youtube.com/embed/a2vRDYXDAug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </p>

        ![VSCode Calva demo](https://github.com/BetterThanTomorrow/calva/raw/master/assets/howto/features.gif)


    === "VSpaceCode"

        [VSpaceCode](https://github.com/VSpaceCode/VSpaceCode) is a Spacemacs-like community configuration for Microsoft VS Code. Drive VS Code and Calva entirely from the keyboard, using easy to remember mnemonic keys for all commands and full vim-stile editing tools.

        Edamagit is a sophisticated text based Git client (like magit for Emacs) is also included in the VSpacemacs extension.

        [Practicalli VSpaceCode install guide](https://practical.li/vspacecode/install/){target=_blank .md-button}
        [Practicalli VSpaceCode user guide](vspacecode-guide/){target=_blank .md-button}

        ![VSpaceCode in action](https://raw.githubusercontent.com/VSpaceCode/vspacecode.github.io/master/static/img/demo.gif)

        <p style="text-align:center">
        <iframe width="560" height="315" src="https://www.youtube.com/embed/1VNNtaUfHs4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </p>


    === "Clover"
        [Clover](https://marketplace.visualstudio.com/items?itemName=mauricioszabo.clover){target=_blank} is a Socket REPL based development tool for Clojure with some ClojureScript support (not including Figwheel).

        [Clojure GitLab repository](https://gitlab.com/clj-editors/clover) includes useage details.



=== "SublimeText"
    [SublimeText 4](https://www.sublimetext.com/) is a lightweight and feature rich text editor, especially of interest that like a simple and uncluttered UI.  SublimeText is a commercial project although has free trial version available (check [conditions of use](https://www.sublimehq.com/store/text)).

    [Clojure-Sublimed](https://github.com/tonsky/Clojure-Sublimed) provides Clojure support for SublimeText 4, with support for Clojure & Edn syntax, code formatting and an nREPL client to connect to a Clojure REPL process.

    [SublimeText install](https://www.sublimetext.com/download){target=_blank .md-button}
    [Clojure-Sublimed install](https://github.com/tonsky/Clojure-Sublimed#installation){target=_blank .md-button}
    [SublimeText Documentation](https://www.sublimetext.com/docs/index.html){target=_blank .md-button}


=== "Atom"

    !!! WARNING "Atom not actively developed"
        Atom will be archived on December 15 2022 and no further updates from GitHub team, although it may continue in open source.

        Consider using VSCode with Clover or Calva plugins instead

    [Atom.io](https://atom.io/) is flexible and simple to use editor .  [Chlorine](https://github.com/mauricioszabo/atom-chlorine) is the recommended plugin for Atom.io. [ProtoREPL](https://atom.io/packages/proto-repl) is not actively maintained at present. The [Chlorine plugin for Atom](https://github.com/mauricioszabo/atom-chlorine) is especially recommended for ClojureScript shadow-cljs projects.

    [Chlorine install guide](https://github.com/mauricioszabo/atom-chlorine){target=_blank .md-button}

    ![Chlorine animated gif](https://raw.githubusercontent.com/mauricioszabo/atom-chlorine/master/docs/eval-code.gif)

    #### ProtoREPL

    ProtoREPL

    [Atom & ProtoREPL install guide](install-guides/atom-protorepl.html){ .md-button }

    ![Atom.io and ProtoREPL](/images/atom-protorepl-demo.gif)


    #### Proton - alternative menu and configuration approach
    Proton offers a simple mnemonic menu as an alternative to the multiple keys for shortcuts in Atom.io.  Proton also gives you a simple text configuration to manage all your packages quickly.  Unfortunately Proton is not complete replacement of all actions.

    [Atom & Proton install guide](install-guides/atom-proton.html){ .md-button }

    ![Atom.io proton-mode demo](/images/atom-proton-mode-demo.gif)


=== "Intellij"
    [Cursive](https://cursive-ide.com/) may be an appropriate choice for people from a Java background who are already familiar with IntelliJ.  Cursive will run static analysis of Clojure code when opening a Clojure project, as IntelliJ does with other languages.

    !!! HINT "Requires license for commercial development"
        There is a free license when development is not for commercial projects, however, a license must be purchased for each developer working on a commercial project.

    [IntelliJ & Cursive install guide](install-guides/intellij-cursive.html){ .md-button }

    ![Cursive IDE](https://cursive-ide.com/images/cursive-screenshot.png)
