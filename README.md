# Elixir development with FreeBSD

Article reviewed in Apr 2021.

To ensure you're working using the latest version of your beloved tools use
[Kerl](https://github.com/kerl/kerl "Github for Kerl") and
[Kiex](https://github.com/taylor/kiex "Github for Kiex").
With this approach you'll be able to jump between versions easily.

```shell
$ sudo pkg install kerl
$ curl -sSL https://raw.githubusercontent.com/taylor/kiex/master/install | bash -s
```

## Installing Erlang

Before you begin to build Erlang with Kerl make sure wxWidgets are properly
installed if you want to be able to use features like `:observer.start()`.

```shell
$ sudo pkg install wx30-gtk3
$ sudo ln -s /usr/lib/bin/wxgtk30u-3.0-config /usr/local/bin/wx-config
$ wx-config --version
3.0.5
```

Kerl uses a concept of *releases* (available online [OTP source
tarballs](https://github.com/erlang/otp/tags)), *builds* (compiled
sources) and *installations* (installed builds). 

Enforced with this knowledge you are ready to check the latest release, build
it and install it.

```shell
$ kerl update releases     # get the list of Erlang releases to choose from
$ kerl build 23.3 23.3     # build relase "23.3" and name it "23.3"
$ kerl install 23.3 ~/.kerl/installations/23.3  # install built release
```

To make sure that installation was successful try to activate new environment,
check Erlang's version and deactivate the environment when you're done. 

```shell
$ source ~/.kerl/installations/23.3/activate
$ kerl active
The current active installation is:
/usr/home/codcod/.kerl/installations/23.3

$ erl -version
Erlang (SMP,ASYNC_THREADS,HIPE) (BEAM) emulator version 11.2

$ kerl_deactivate          # deactivate "virtual environment"
```

Useful commands.

```shell
$ kerl delete build 23.3   # remove built release
$ kerl list builds         # list versions built so far
$ kerl list installations  # list versions installed locally
$ kerl active              # show active version (installation)
```

## Installing Elixir

Kiex follows the same approach as Kerl. You check the latest releases, build
and install one in one go.

```shell
$ kiex list releases       # get the list od Elixir releases to choose from
$ kiex install 1.11.4      # install release "1.11.4"
$ kiex default 1.11.4      # make this release default
```

## After installation

Add to your `.zshrc`:

```shell
source "$HOME/.kerl/installations/23.3/activate"
source "$HOME/.kiex/scripts/kiex.bash"
source "$HOME/.kiex/elixirs/.elixir-1.11.4.env.bash"
```

Follow [this blog post](https://samuelmullen.com/articles/customizing_elixirs_iex)
to customize Elixir's REPL -- IEx.

## Resources

* [Kerl](https://github.com/kerl/kerl)
* [Kiex](https://github.com/taylor/kiex)
* [Prying.io](https://prying.io/technical/2018/09/18/using-kerl-and-kiex-for-version-management.html)
* [Samuel Mullen](https://samuelmullen.com/articles/customizing_elixirs_iex)

