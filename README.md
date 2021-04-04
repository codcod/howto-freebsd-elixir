# Elixir development in FreeBSD

Article reviewed in Apr 2021.

To ensure you're working using the latest version of your beloved tools use
[Kerl](https://github.com/kerl/kerl "Github for Kerl") and [Kiex](https://github.com/taylor/kiex "Github for Kiex").

```shell
$ sudo pkg install kerl
$ curl -sSL https://raw.githubusercontent.com/taylor/kiex/master/install | bash -s
```

Before you begin to build Erlang using Kerl make sure wxWidgets are properly installed if you want to be able to use features like `:observer.start()`.

```shell
$ sudo pkg install wx30-gtk3
$ sudo ln -s /usr/lib/bin/wxgtk30u-3.0-config /usr/local/bin/wx-config
$ wx-config --version
3.0.5
```
## Building Erlang

```shell
$ kerl update releases  # get the list of available Erlang releases to choose from
$ kerl build 23.3 23.3  # build relase "23.3" and name it "23.3"
$ kerl install 23.3 ~/.kerl/installations/23.3  # install release named "23.3" that had been just built
```

To make sure that installation was successful activate new installation, show it, check Erlang version and deactivate this virtual environment. 

```shell
$ source ~/.kerl/installations/23.3/activate
$ kerl active           # shows active version (installation)
The current active installation is:
/usr/home/codcod/.kerl/installations/23.3
$ erl -version          # make sure installation was successful
Erlang (SMP,ASYNC_THREADS,HIPE) (BEAM) emulator version 11.2
$ kerl_deactivate       # deactivate "virtual environment"
```

Useful commmands.

```shell
$ kerl delete build 23.3   # remove built release
$ kerl list builds         # list versions built so far
$ kerl list installations  # list versions installed locally
$ kerl active              # shows active version (installation)
```

