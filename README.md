<div align="center">
  <a href="https://github.com/zimfw/zimfw">
    <img width="600" src="https://zimfw.github.io/images/zimfw-banner@2.jpg">
  </a>
</div>

What is Zim?
------------
Zim is a Zsh configuration framework with [blazing speed] and modular extensions.

Zim bundles useful [modules], a wide variety of [themes], and plenty of
customizability without compromising on speed.

What does Zim offer?
--------------------
Below is a brief showcase of Zim's features.

### Speed
<a href="https://github.com/zimfw/zimfw/wiki/Speed">
  <img src="https://zimfw.github.io/images/results.svg">
</a>

For more details, see [this wiki entry][blazing speed].

### Modules

Zim has many [modules available][modules]. Enable as many or as few as you'd like.

### Themes

To preview some of the available themes, check the [themes page][themes].

### Degit

Install modules without requiring `git` using our degit tool. It's faster and
lighter than `git`. See the [zmodule](#zmodule-usage) usage below.

Installation
------------
Installing Zim is easy:

* With curl:

      curl -fsSL https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh

* With wget:

      wget -nv -O - https://raw.githubusercontent.com/zimfw/install/master/install.zsh | zsh

Open a new terminal and you're done. Enjoy your Zsh IMproved! Take some time to
tweak your `~/.zshrc` file, and to also check the available [modules] and [themes]
you can add to your `~/.zimrc`.

<details>
<summary>Prefer to install manually?</summary>

### Manual installation

1. Set Zsh as the default shell:

       chsh -s $(which zsh)

2. Prepend the lines in the following templates to the respective dot files:

   * [~/.zshrc](https://raw.githubusercontent.com/zimfw/install/master/src/templates/zshrc)
   * [~/.zimrc](https://raw.githubusercontent.com/zimfw/install/master/src/templates/zimrc)

3. Restart your terminal to automatically install the `zimfw` command line utility,
   install the modules defined in `~/.zimrc`, and build the initialization scripts.
</details>

Usage
-----

Add `zmodule` calls to your `~/.zimrc` file to define the modules to be
initialized, then run `zimfw install` to install them.

### zmodule

Below are some usage examples:

  * A module from the [@zimfw] organization: `zmodule archive`
  * A module from another GitHub organization: `zmodule StackExchange/blackbox`
  * A module with a custom URL: `zmodule https://gitlab.com/Spriithy/basher.git`
  * A module at an absolute path, that is already installed:
    `zmodule /usr/local/share/zsh-autosuggestions`
  * A module with a custom fpath: `zmodule zsh-users/zsh-completions --fpath src`
  * A module with a custom initialization file:
    `zmodule spaceship-prompt/spaceship-prompt --source spaceship.zsh` or
    `zmodule spaceship-prompt/spaceship-prompt --name spaceship`
  * A module with two custom initialization files:
    `zmodule sindresorhus/pure --source async.zsh --source pure.zsh`
  * A module with a custom initialization command:
    `zmodule skywind3000/z.lua --cmd 'eval "$(lua {}/z.lua --init zsh enhanced once)"'`
  * A module with a big git repository: `zmodule romkatv/powerlevel10k --use degit`

<details id="zmodule-usage">
<summary>Want help with the complete <code>zmodule</code> usage?</summary>

<pre>Usage: <b>zmodule</b> &lt;url&gt; [<b>-n</b>|<b>--name</b> &lt;module_name&gt;] [options]

Add <b>zmodule</b> calls to your <b>~/.zimrc</b> file to define the modules to be initialized. The modules
are initialized in the same order they are defined.

  &lt;url&gt;                      Module absolute path or repository URL. The following URL formats
                             are equivalent: <b>foo</b>, <b>zimfw/foo</b>, <b>https://github.com/zimfw/foo.git</b>.
  <b>-n</b>|<b>--name</b> &lt;module_name&gt;    Set a custom module name. Default: the last component in &lt;url&gt;.
                             Use slashes inside the name to organize the module into subdirec-
                             tories.

Repository options:
  <b>-b</b>|<b>--branch</b> &lt;branch_name&gt;  Use specified branch when installing and updating the module.
                             Overrides the tag option. Default: the repository default branch.
  <b>-t</b>|<b>--tag</b> &lt;tag_name&gt;        Use specified tag when installing and updating the module. Over-
                             rides the branch option.
  <b>-u</b>|<b>--use</b> &lt;<b>git</b>|<b>degit</b>&gt;       Install and update the module using the defined tool. Default is
                             either defined by <b>zstyle &apos;:zim:zmodule&apos; use &apos;</b>&lt;<b>git</b>|<b>degit</b>&gt;<b>&apos;</b>, or <b>git</b>
                             if none is provided.
                             <b>git</b> requires git itself. Local changes are preserved on updates.
                             <b>degit</b> requires curl or wget, and currently only works with GitHub
                             URLs. Modules install faster and take less disk space. Local
                             changes are lost on updates. Git submodules are not supported.
  <b>-z</b>|<b>--frozen</b>                Don&apos;t install or update the module.

Initialization options:
  <b>-f</b>|<b>--fpath</b> &lt;path&gt;          Add specified path to fpath. The path is relative to the module
                             root directory. Default: <b>functions</b>, if the subdirectory exists.
  <b>-a</b>|<b>--autoload</b> &lt;func_name&gt;  Autoload specified function. Default: all valid names inside the
                             <b>functions</b> subdirectory, if any.
  <b>-s</b>|<b>--source</b> &lt;file_path&gt;    Source specified file. The file path is relative to the module
                             root directory. Default: <b>init.zsh</b>, if the <b>functions</b> subdirectory
                             also exists, or the file with largest size and with name matching
                             <b>{init.zsh,module_name.{zsh,plugin.zsh,zsh-theme,sh}}</b>, if any.
  <b>-c</b>|<b>--cmd</b> &lt;command&gt;         Execute specified command. Occurrences of the <b>{}</b> placeholder in
                             the command are substituted by the module root directory path.
                             I.e., <b>-s &apos;foo.zsh&apos;</b> and <b>-c &apos;source {}/foo.zsh&apos;</b> are equivalent.
  <b>-d</b>|<b>--disabled</b>              Don&apos;t initialize or uninstall the module.

  Setting any initialization option above will disable all the default values from the other
  initialization options, so only your provided values are used. I.e. these values are either
  all automatic, or all manual.
</pre>

</details>

### zimfw

The command line utility for Zim:

  * Added new modules to `~/.zimrc`? Run `zimfw install`.
  * Removed modules from `~/.zimrc`? Run `zimfw uninstall`.
  * Want to update your modules to their latest revisions? Run `zimfw update`.
  * Want to upgrade `zimfw` to its latest version? Run `zimfw upgrade`.
  * For more information about the `zimfw` utility, run `zimfw help`.

Settings
--------

Modules are installed using `git` by default. If you don't have `git`
installed, or if you want to take advantage of our degit tool for faster and
lighter module installations, you can set degit as the default tool with:

    zstyle ':zim:zmodule' use 'degit'

By default, `zimfw` will check if it has a new version available every 30 days.
This can be disabled with:

    zstyle ':zim' disable-version-check yes

Uninstalling
------------

The best way to remove Zim is to manually delete `~/.zim`, `~/.zimrc`, and
remove the initialization lines from your `~/.zshenv`, `~/.zshrc` and `~/.zlogin`.

[blazing speed]: https://github.com/zimfw/zimfw/wiki/Speed
[modules]: https://zimfw.sh/docs/modules/
[themes]: https://zimfw.sh/docs/themes/
[@zimfw]: https://github.com/zimfw
