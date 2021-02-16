MacOS Build Instructions and Notes
====================================
This guide will show you how to build Gamebets(qt) for MacOS

Notes
-----
* Tested on MacOS from version 10.13.6 High Sierra.
* All of the commands should be executed in a Terminal application. The
built-in one is located in `/Applications/Utilities/Terminal.app`.

Preparation
-----------
Install the macOS command line tools:

`xcode-select --install`

When the popup appears, click `Install`.

Then install [Homebrew](https://brew.sh).

Dependencies
----------------------

    brew install automake berkeley-db4 libtool boost@1.60 miniupnpc openssl pkg-config protobuf python qt libevent qrencode

See [dependencies.md](dependencies.md) for a complete overview.

If you want to build the disk image with `make deploy` (.dmg / optional), you need RSVG

    brew install librsvg

Berkeley DB
-----------
    It is recommended to use Berkeley DB 4.8. If you have to build it yourself,
    you can use [the installation script included in contrib/](/contrib/install_db4.sh)
    like so

    ```shell
    ./contrib/install_db4.sh .
    ```

    from the root of the repository.

    **Note**: You only need Berkeley DB if the wallet is enabled (see the section *Disable-Wallet mode* below).

Build Gamebets Core
    ------------------------

    1. Clone the Gamebets Core source code and cd into `Gamebets`

            git clone https://github.com/GamebetsCoin/Gamebets.git
            cd Gamebets

    2.  Build Gamebets Core:

        Configure and build the headless Gamebets Core binaries as well as the GUI (if Qt is found).

        You can disable the GUI build by passing `--without-gui` to configure.

            ./autogen.sh
            ./configure
            make

    3.  You can also create a .dmg that contains the .app bundle (optional):

            make deploy


    **Note**: Optional: Build and run the unit tests: make check

Disable-wallet mode
--------------------
When the intention is to run only a P2P node without a wallet, Bitcoin Core may be compiled in
disable-wallet mode with:

            ./configure --disable-wallet

In this case there is no dependency on Berkeley DB 4.8.

Mining is also possible in disable-wallet mode using the `getblocktemplate` RPC call.

Running
-------
Gamebets executables are now available at `./src/gamebetsd`
Gamebets-qt is now available at `.src/qt/Gamebets-qt`
Gamebets-qt.dmg is now available at `.src/Gamebets-qt.dmg`

Before running, it's recommended that you create an RPC configuration file.

Run `./gamebetsd` to get the filename where it should be put, or just try these
commands:

    echo -e "rpcuser=gamebetsrpc\nrpcpassword=$(xxd -l 16 -p /dev/urandom)" > "/Users/${USER}/Library/Application Support/Gamebets/gamebets.conf"
    chmod 600 "/Users/${USER}/Library/Application Support/Gamebets/gamebets.conf"

The first time you run gamebetsd, it will start downloading the blockchain. This process may take some time;

You can monitor the download process by looking at the debug.log file:

    tail -f $HOME/Library/Application\ Support/Gamebets/debug.log

Other commands:
-------

    ./gamebetsd -daemon     # Starts the gamebets daemon.
    ./gamebets-cli --help   # Outputs a list of command-line options.
    ./gamebets-cli help     # Outputs a list of RPC commands when the daemon is running
