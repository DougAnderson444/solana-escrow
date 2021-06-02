# solana-escrow

An implementation of an escrow on solana using [this guide](https://paulx.dev/2021/01/14/programming-on-solana-an-introduction)


# Build

In Linus or Windows WSL:

```sh
cargo build-bpf
```

...which compiles the program to a file with the `.so` file extension. You should see something like `/code/solana-escrow/target/deploy/solana_escrow.so` in your folder.

    To deploy this program:
    $ solana program deploy /code/solana-escrow/target/deploy/solana_escrow.so

```sh
# create and save a solana keypair locally
# or use your own wallet to get a keypair
solana-keygen new
```

Start local network

```sh
solana-test-validator
```

When calling solana config get, your "RPC URL" should now equal http://localhost:8899. If not, run 

```sh
solana config set --url http://localhost:8899
```

Run

```sh
# will show your balance which should NOT be 0
solana balance
```

## To deploy this program on Devnet:

sThrought the solana CLI:

Set the network to devnet:

```
solana config set --url devnet
```

Now everything will apply to the devnet, such as accounts and airdrops.

Make a new account on devnet

```
solana-keygen new
```

This will save the keypair to a id.json file in your `/home/user/.config/solana` folder

Check the balance

```
solana balance
```

If it's zero, airdrop some SOL:

```sh
solana airdrop 1 --url devnet
```

Now you've got funds to deploy a program:

```
solana deploy ./target/deploy/solana_escrow.so
```

([Docs](https://docs.solana.com/cli/usage#deploy-program) say `solana *program* deploy`, but `solana deploy` [worked](https://docs.solana.com/cli/usage#solana-deploy) for me on devnet...)

```sh
solana program deploy /code/programs/build/solana-escrow.so
```