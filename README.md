# multisig

To install dependencies:

```bash
bun install
```

To run:

```bash
bun run ./src/index.ts
```

This project was created using `bun init` in bun v1.1.6. [Bun](https://bun.sh) is a fast all-in-one JavaScript runtime.


## Memo

### The most simple example: Send Sui from an account to another

```
$ lsui client transfer-sui --to 0x0fc530455ee4132b761ed82dab732990cb7af73e69cd6e719a2a5badeaed105b --sui-coin-object-id 0x4a3b0563e1cf18b0325182d91294af839ae4a623432f81dbaf610abb5364e020 --gas-budget 2000000000   --amount 5000000000
Transaction Digest: 7sT1TXg8D14K5XUoVfT4snW4oPJiHAq5o8eAUZBaeLh7
```

> object id can be obtained through curl command below:
```
$ curl --location --request POST 'http://127.0.0.1:9123/gas' --header 'Content-Type: application/json' --data-raw "{ \"FixedAmountRequest\": { \"recipient\": \"0xf7ae71f84fabc58662bd4209a8893f462c60f247095bb35b19ff659ad0081462\" } }" 

{"transferredGasObjects":[{"amount":20000000000,"id":"0x4a3b0563e1cf18b0325182d91294af839ae4a623432f81dbaf610abb5364e020","transferTxDigest":"2bFBFP2Y8RXJK1MS1wXKjrUFXr1LV82TrduRuBkLqZqA"},{"amount":20000000000,"id":"0xbc00d75e81dcd054143a6169f1f075029f3ece79211f27383e7c7d334aacd72c","transferTxDigest":"2bFBFP2Y8RXJK1MS1wXKjrUFXr1LV82TrduRuBkLqZqA"},{"amount":20000000000,"id":"0xd9a9367a2a9f51e7c21c24e99d2d6c80ee96f7111f2c0752b46d96f3bbc19787","transferTxDigest":"2bFBFP2Y8RXJK1MS1wXKjrUFXr1LV82TrduRuBkLqZqA"},{"amount":20000000000,"id":"0xe8565da104f150be7975a814fd93c0a54d555f1e2d6f92e9695f8f511e70df8e","transferTxDigest":"2bFBFP2Y8RXJK1MS1wXKjrUFXr1LV82TrduRuBkLqZqA"},{"amount":20000000000,"id":"0xecef1bc53af2d8d8dd1c9e2034b358b227bfff1f2654c3a666ecec00a92e2a46","transferTxDigest":"2bFBFP2Y8RXJK1MS1wXKjrUFXr1LV82TrduRuBkLqZqA"}],"error":null}

```
"id" is the object-id 

### Setting up environment.

1. Use suibase (https://suibase.io/how-to/localnet.html)
2. Launch localnet

### Creating a multisig address

1. Following https://docs.sui.io/concepts/cryptography/transaction-auth/multisig
> * In local suibase network, there are already initialized addresses. 
> * In order to access to suibase localnet, **lsui** command is used instead of sui command  

2. List available addresses
`` $ lsui keytool list  ``

3. Create a multisig address
```
$ lsui keytool multi-sig-address --pks AgIrMYwPbHFcj+kR4dbn0bkzU82fGQfw4QzJjhWGAUd4zQ== ALSfnL+vbyJ55c0rCuR08k8AoYxS7o4xAyaQ1Lmw977B AFeZlOAw+qZxhyjMyWnaQ+VQeYPGAq5NbQ+tw8p4v7uT --weights 1 2 3 --threshold 3 

╭─────────────────┬────────────────────────────────────────────────────────────────────────────────────────────────╮
│ multisigAddress │  0xcf41631862715223daae395c1a40677c8c4d93352ccedf48ae351684c9b5236b                            │
│ multisig        │ ╭────────────────────────────────────────────────────────────────────────────────────────────╮ │
│                 │ │ ╭─────────────────┬──────────────────────────────────────────────────────────────────────╮ │ │
│                 │ │ │ address         │  0xc7294a5cc946db818c4058c83c933ad6c28e73711bee21c7fa85553c90cb7244  │ │ │
│                 │ │ │ publicBase64Key │  AgIrMYwPbHFcj+kR4dbn0bkzU82fGQfw4QzJjhWGAUd4zQ==                    │ │ │
│                 │ │ │ weight          │  1                                                                   │ │ │
│                 │ │ ╰─────────────────┴──────────────────────────────────────────────────────────────────────╯ │ │
│                 │ │ ╭─────────────────┬──────────────────────────────────────────────────────────────────────╮ │ │
│                 │ │ │ address         │  0xf7ae71f84fabc58662bd4209a8893f462c60f247095bb35b19ff659ad0081462  │ │ │
│                 │ │ │ publicBase64Key │  ALSfnL+vbyJ55c0rCuR08k8AoYxS7o4xAyaQ1Lmw977B                        │ │ │
│                 │ │ │ weight          │  2                                                                   │ │ │
│                 │ │ ╰─────────────────┴──────────────────────────────────────────────────────────────────────╯ │ │
│                 │ │ ╭─────────────────┬──────────────────────────────────────────────────────────────────────╮ │ │
│                 │ │ │ address         │  0x8c66fda13388668dcb7bbe402c56e5819fa429f973070f094775711a4bb63b34  │ │ │
│                 │ │ │ publicBase64Key │  AFeZlOAw+qZxhyjMyWnaQ+VQeYPGAq5NbQ+tw8p4v7uT                        │ │ │
│                 │ │ │ weight          │  3                                                                   │ │ │
│                 │ │ ╰─────────────────┴──────────────────────────────────────────────────────────────────────╯ │ │
│                 │ ╰────────────────────────────────────────────────────────────────────────────────────────────╯ │
╰─────────────────┴────────────────────────────────────────────────────────────────────────────────────────────────╯
```

> Command line may reject slash "/" in public key. For example,  "AQKDgiRz9w/ZpZYS20WcFiDa6AwA+/DEWx5eq5AVvgbQ8A==".

4. Fund created multisig address
``` $ localnet faucet 0xcf41631862715223daae395c1a40677c8c4d93352ccedf48ae351684c9b5236b ``` 

5. Test sending object to the multisig address to obtain <OBJECT-ID>

``` $ curl --location --request POST 'http://127.0.0.1:9123/gas' --header 'Content-Type: application/json' --data-raw "{ \"FixedAmountRequest\": { \"recipient\": \"0xcf41631862715223daae395c1a40677c8c4d93352ccedf48ae351684c9b5236b\" } }"

{"transferredGasObjects":[{"amount":20000000000,"id":"0x898db79b2fac4563de50c6152316b110854ffcf1568189a51b81bbeee07d0d8b","transferTxDigest":"DjJ85r7PJ87NJVs7zipcaDo9eLpwGTHd5WSrmqZ72mKD"},{"amount":20000000000,"id":"0x9a44006ecdcd3102c5be1b206979f058ea7123ae036ec4163da080ee5d549795","transferTxDigest":"DjJ85r7PJ87NJVs7zipcaDo9eLpwGTHd5WSrmqZ72mKD"},{"amount":20000000000,"id":"0xb925ff018ec614eb58e605d135ca6ba7ca163e58d65609aca36d21e3dec942e8","transferTxDigest":"DjJ85r7PJ87NJVs7zipcaDo9eLpwGTHd5WSrmqZ72mKD"},{"amount":20000000000,"id":"0xc5efc911aabc488558cd90da7f2c3fb36cb644ba08f06fc7a307faa6f6378d39","transferTxDigest":"DjJ85r7PJ87NJVs7zipcaDo9eLpwGTHd5WSrmqZ72mKD"},{"amount":20000000000,"id":"0xcf6ccf4608c35e2717887b3f35496bfafe19d8a389e0730af054026311f13132","transferTxDigest":"DjJ85r7PJ87NJVs7zipcaDo9eLpwGTHd5WSrmqZ72mKD"}],"error":null}
```

6. Prepare transaction to be sent/signed
```
$ lsui client transfer --to 0x0fc530455ee4132b761ed82dab732990cb7af73e69cd6e719a2a5badeaed105b --object-id 0x898db79b2fac4563de50c6152316b110854ffcf1568189a51b81bbeee07d0d8b --gas-budget 20000000000 --serialize-unsigned-transaction

AAACACAPxTBFXuQTK3Ye2C2rcymQy3r3PmnNbnGaKlut6u0QWwEAiY23my+sRWPeUMYVIxaxEIVP/PFWgYmlG4G77uB9DYsIAAAAAAAAACCfNf1cRvD7zevGNFWv4ofyF1Jsx4JAulO7P2r3JhLb7gEBAQEBAAEAAM9BYxhicVIj2q45XBpAZ3yMTZM1LM7fSK41FoTJtSNrAQ+miSt4+oW/cWId2Zqz9w57uU0kZ7A8M0swURBcdXQoCAAAAAAAAAAgFjbfakIGbz59ACpBGnADSS3M0bt2b6c/+HgeCJfxzUfPQWMYYnFSI9quOVwaQGd8jE2TNSzO30iuNRaEybUja+gDAAAAAAAAAMgXqAQAAAAA
```

> TODO: what is transfer-sui command???
``` 
$ lsui client transfer-sui --to 0x0fc530455ee4132b761ed82dab732990cb7af73e69cd6e719a2a5badeaed105b --sui-coin-object-id 0x898db79b2fac4563de50c6152316b110854ffcf1568189a51b81bbeee07d0d8b   --gas-budget 20000000000   --amount 100 --serialize-unsigned-transaction

 AAACACAPxTBFXuQTK3Ye2C2rcymQy3r3PmnNbnGaKlut6u0QWwAIZAAAAAAAAAACAgABAQEAAQECAAABAADPQWMYYnFSI9quOVwaQGd8jE2TNSzO30iuNRaEybUjawGJjbebL6xFY95QxhUjFrEQhU/88VaBiaUbgbvu4H0NiwgAAAAAAAAAIJ81/VxG8PvN68Y0Va/ih/IXUmzHgkC6U7s/avcmEtvuz0FjGGJxUiParjlcGkBnfIxNkzUszt9IrjUWhMm1I2voAwAAAAAAAADIF6gEAAAAAA==
```

7. Signing transaction with keys
In this example, sign transaction with two keys (weight 1 and 2) then combine those signatures to send transaction

key 1 (weight 1)
```
$ lsui keytool sign --address 0xc7294a5cc946db818c4058c83c933ad6c28e73711bee21c7fa85553c90cb7244 --data AAACACAPxTBFXuQTK3Ye2C2rcymQy3r3PmnNbnGaKlut6u0QWwAIZAAAAAAAAAACAgABAQEAAQECAAABAADPQWMYYnFSI9quOVwaQGd8jE2TNSzO30iuNRaEybUjawGJjbebL6xFY95QxhUjFrEQhU/88VaBiaUbgbvu4H0NiwgAAAAAAAAAIJ81/VxG8PvN68Y0Va/ih/IXUmzHgkC6U7s/avcmEtvuz0FjGGJxUiParjlcGkBnfIxNkzUszt9IrjUWhMm1I2voAwAAAAAAAADIF6gEAAAAAA== 

╭──────────────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ suiAddress   │ 0xc7294a5cc946db818c4058c83c933ad6c28e73711bee21c7fa85553c90cb7244                                                                                               │
│ rawTxData    │ AAACACAPxTBFXuQTK3Ye2C2rcymQy3r3PmnNbnGaKlut6u0QWwAIZAAAAAAAAAACAgABAQEAAQECAAABAADPQWMYYnFSI9quOVwaQGd8jE2TNSzO30iuNRaEybUjawGJjbebL6xFY95QxhUjFrEQhU/88VaBiaUb │
│              │ gbvu4H0NiwgAAAAAAAAAIJ81/VxG8PvN68Y0Va/ih/IXUmzHgkC6U7s/avcmEtvuz0FjGGJxUiParjlcGkBnfIxNkzUszt9IrjUWhMm1I2voAwAAAAAAAADIF6gEAAAAAA==                             │
│ intent       │ ╭─────────┬─────╮                                                                                                                                                │
│              │ │ scope   │  0  │                                                                                                                                                │
│              │ │ version │  0  │                                                                                                                                                │
│              │ │ app_id  │  0  │                                                                                                                                                │
│              │ ╰─────────┴─────╯                                                                                                                                                │
│ rawIntentMsg │ AAAAAAACACAPxTBFXuQTK3Ye2C2rcymQy3r3PmnNbnGaKlut6u0QWwAIZAAAAAAAAAACAgABAQEAAQECAAABAADPQWMYYnFSI9quOVwaQGd8jE2TNSzO30iuNRaEybUjawGJjbebL6xFY95QxhUjFrEQhU/88VaB │
│              │ iaUbgbvu4H0NiwgAAAAAAAAAIJ81/VxG8PvN68Y0Va/ih/IXUmzHgkC6U7s/avcmEtvuz0FjGGJxUiParjlcGkBnfIxNkzUszt9IrjUWhMm1I2voAwAAAAAAAADIF6gEAAAAAA==                         │
│ digest       │ J+/5Gyker4IHGVzFnVL9y6E4u7u9exdH64BrGML0gmE=                                                                                                                     │
│ suiSignature │ AlqyUJoTAoT1R+8xgGC7oaF4wmweNT7S/Rm1JhwR4AAVSrPp6VgNgl+gL6jinyurjxwvsXAC6W1p+Dnz7QYn4P0CKzGMD2xxXI/pEeHW59G5M1PNnxkH8OEMyY4VhgFHeM0=                             │
╰──────────────┴──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

key 2 (weight 2)
```
$ lsui keytool sign --address 0xf7ae71f84fabc58662bd4209a8893f462c60f247095bb35b19ff659ad0081462 --data AAACACAPxTBFXuQTK3Ye2C2rcymQy3r3PmnNbnGaKlut6u0QWwAIZAAAAAAAAAACAgABAQEAAQECAAABAADPQWMYYnFSI9quOVwaQGd8jE2TNSzO30iuNRaEybUjawGJjbebL6xFY95Q
xhUjFrEQhU/88VaBiaUbgbvu4H0NiwgAAAAAAAAAIJ81/VxG8PvN68Y0Va/ih/IXUmzHgkC6U7s/avcmEtvuz0FjGGJxUiParjlcGkBnfIxNkzUszt9IrjUWhMm1I2voAwAAAAAAAADIF6gEAAAAAA== 

╭──────────────┬──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ suiAddress   │ 0xf7ae71f84fabc58662bd4209a8893f462c60f247095bb35b19ff659ad0081462                                                                                               │
│ rawTxData    │ AAACACAPxTBFXuQTK3Ye2C2rcymQy3r3PmnNbnGaKlut6u0QWwAIZAAAAAAAAAACAgABAQEAAQECAAABAADPQWMYYnFSI9quOVwaQGd8jE2TNSzO30iuNRaEybUjawGJjbebL6xFY95QxhUjFrEQhU/88VaBiaUb │
│              │ gbvu4H0NiwgAAAAAAAAAIJ81/VxG8PvN68Y0Va/ih/IXUmzHgkC6U7s/avcmEtvuz0FjGGJxUiParjlcGkBnfIxNkzUszt9IrjUWhMm1I2voAwAAAAAAAADIF6gEAAAAAA==                             │
│ intent       │ ╭─────────┬─────╮                                                                                                                                                │
│              │ │ scope   │  0  │                                                                                                                                                │
│              │ │ version │  0  │                                                                                                                                                │
│              │ │ app_id  │  0  │                                                                                                                                                │
│              │ ╰─────────┴─────╯                                                                                                                                                │
│ rawIntentMsg │ AAAAAAACACAPxTBFXuQTK3Ye2C2rcymQy3r3PmnNbnGaKlut6u0QWwAIZAAAAAAAAAACAgABAQEAAQECAAABAADPQWMYYnFSI9quOVwaQGd8jE2TNSzO30iuNRaEybUjawGJjbebL6xFY95QxhUjFrEQhU/88VaB │
│              │ iaUbgbvu4H0NiwgAAAAAAAAAIJ81/VxG8PvN68Y0Va/ih/IXUmzHgkC6U7s/avcmEtvuz0FjGGJxUiParjlcGkBnfIxNkzUszt9IrjUWhMm1I2voAwAAAAAAAADIF6gEAAAAAA==                         │
│ digest       │ J+/5Gyker4IHGVzFnVL9y6E4u7u9exdH64BrGML0gmE=                                                                                                                     │
│ suiSignature │ APOLMcAnoXHBntgLOjprjSltu3G7i9pO36Akde/YmNdlPWCNod44yw1nrMuVDv+O6MxC1OBn3sr3uSlrI/J9bAS0n5y/r28ieeXNKwrkdPJPAKGMUu6OMQMmkNS5sPe+wQ==                             │
╰──────────────┴──────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
```

8. Combine two signatures
```
$ lsui keytool multi-sig-combine-partial-sig --pks AgIrMYwPbHFcj+kR4dbn0bkzU82fGQfw4QzJjhWGAUd4zQ== ALSfnL+vbyJ55c0rCuR08k8AoYxS7o4xAyaQ1Lmw977B AFeZlOAw+qZxhyjMyWnaQ+VQeYPGAq5NbQ+tw8p4v7uT --weights 1 2 3 --threshold 3 --sigs AlqyUJoTAoT1R+8xg GC7oaF4wmweNT7S/Rm1JhwR4AAVSrPp6VgNgl+gL6jinyurjxwvsXAC6W1p+Dnz7QYn4P0CKzGMD2xxXI/pEeHW59G5M1PNnxkH8OEMyY4VhgFHeM0= APOLMcAnoXHBntgLOjprjSltu3G7i9pO36Akde/YmNdlPWCNod44yw1nrMuVDv+O6MxC1OBn3sr3uSlrI/J9bAS0n5y/r28ieeXNKwrkdPJPAKGMUu6OMQMmkNS5sPe+wQ== 

```

9. Send transaction 
```
$ lsui client execute-signed-tx --tx-bytes AAACACAPxTBFXuQTK3Ye2C2rcymQy3r3PmnNbnGaKlut6u0QWwAIZAAAAAAAAAACAgABAQEAAQECAAABAADPQWMYYnFSI9quOVwaQGd8jE2TNSzO30iuNRaEybUjawGJjbebL6xFY95QxhUjFrEQhU/88VaBiaUbgbvu4H0NiwgAAAAAAAAAIJ81/VxG8PvN68Y0Va/ih/IXUmzHgkC6U7s/avcmEtvuz0FjGGJxUiParjlcGkBnfIxNkzUszt9IrjUWhMm1I2voAwAAAAAAAADIF6gEAAAAAA== --signatures AwICWrJQmhMChPVH7zGAYLuhoXjCbB41PtL9GbUmHBHgABVKs+npWA2CX6AvqOKfK6uPHC+xcALpbWn4OfPtBifg/QDzizHAJ6FxwZ7YCzo6a40pbbtxu4vaTt+gJHXv2JjXZT1gjaHeOMsNZ6zLlQ7/jujMQtTgZ97K97kpayPyfWwEAwADAgIrMYwPbHFcj+kR4dbn0bkzU82fGQfw4QzJjhWGAUd4zQEAtJ+cv69vInnlzSsK5HTyTwChjFLujjEDJpDUubD3vsECAFeZlOAw+qZxhyjMyWnaQ+VQeYPGAq5NbQ+tw8p4v7uTAwMA

Transaction Digest: FFtreqtLFYA8HcquG7NeRJzG9r5WuvMUvUCcqa3WNzJY
╭─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Transaction Data                                                                                                                                                                                                                                                                                                                    │
├─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Sender: 0xcf41631862715223daae395c1a40677c8c4d93352ccedf48ae351684c9b5236b                                                                                                                                                                                                                                                          │
│ Gas Owner: 0xcf41631862715223daae395c1a40677c8c4d93352ccedf48ae351684c9b5236b                                                                                                                                                                                                                                                       │
│ Gas Budget: 20000000000 MIST                                                                                                                                                                                                                                                                                                        │
│ Gas Price: 1000 MIST                                                                                                                                                                                                                                                                                                                │
│ Gas Payment:                                                                                                                                                                                                                                                                                                                        │
│  ┌──                                                                                                                                                                                                                                                                                                                                │
│  │ ID: 0x898db79b2fac4563de50c6152316b110854ffcf1568189a51b81bbeee07d0d8b                                                                                                                                                                                                                                                           │
│  │ Version: 8                                                                                                                                                                                                                                                                                                                       │
│  │ Digest: BiVaDZSF673xn8TGiivU7wUQCsa1bNKk1HTBPhevwvtD                                                                                                                                                                                                                                                                             │
│  └──                                                                                                                                                                                                                                                                                                                                │
│                                                                                                                                                                                                                                                                                                                                     │
│ Transaction Kind: Programmable                                                                                                                                                                                                                                                                                                      │
│ ╭──────────────────────────────────────────────────────────────────────────────────────────────────────────╮                                                                                                                                                                                                                        │
│ │ Input Objects                                                                                            │                                                                                                                                                                                                                        │
│ ├──────────────────────────────────────────────────────────────────────────────────────────────────────────┤                                                                                                                                                                                                                        │
│ │ 0   Pure Arg: Type: address, Value: "0x0fc530455ee4132b761ed82dab732990cb7af73e69cd6e719a2a5badeaed105b" │                                                                                                                                                                                                                        │
│ │ 1   Pure Arg: Type: u64, Value: "100"                                                                    │                                                                                                                                                                                                                        │
│ ╰──────────────────────────────────────────────────────────────────────────────────────────────────────────╯                                                                                                                                                                                                                        │
│ ╭──────────────────────╮                                                                                                                                                                                                                                                                                                            │
│ │ Commands             │                                                                                                                                                                                                                                                                                                            │
│ ├──────────────────────┤                                                                                                                                                                                                                                                                                                            │
│ │ 0  SplitCoins:       │                                                                                                                                                                                                                                                                                                            │
│ │  ┌                   │                                                                                                                                                                                                                                                                                                            │
│ │  │ Coin: GasCoin     │                                                                                                                                                                                                                                                                                                            │
│ │  │ Amounts:          │                                                                                                                                                                                                                                                                                                            │
│ │  │   Input  1        │                                                                                                                                                                                                                                                                                                            │
│ │  └                   │                                                                                                                                                                                                                                                                                                            │
│ │                      │                                                                                                                                                                                                                                                                                                            │
│ │ 1  TransferObjects:  │                                                                                                                                                                                                                                                                                                            │
│ │  ┌                   │                                                                                                                                                                                                                                                                                                            │
│ │  │ Arguments:        │                                                                                                                                                                                                                                                                                                            │
│ │  │   Result 0        │                                                                                                                                                                                                                                                                                                            │
│ │  │ Address: Input  0 │                                                                                                                                                                                                                                                                                                            │
│ │  └                   │                                                                                                                                                                                                                                                                                                            │
│ ╰──────────────────────╯                                                                                                                                                                                                                                                                                                            │
│                                                                                                                                                                                                                                                                                                                                     │
│ Signatures:                                                                                                                                                                                                                                                                                                                         │
│    AwICWrJQmhMChPVH7zGAYLuhoXjCbB41PtL9GbUmHBHgABVKs+npWA2CX6AvqOKfK6uPHC+xcALpbWn4OfPtBifg/QDzizHAJ6FxwZ7YCzo6a40pbbtxu4vaTt+gJHXv2JjXZT1gjaHeOMsNZ6zLlQ7/jujMQtTgZ97K97kpayPyfWwEAwADAgIrMYwPbHFcj+kR4dbn0bkzU82fGQfw4QzJjhWGAUd4zQEAtJ+cv69vInnlzSsK5HTyTwChjFLujjEDJpDUubD3vsECAFeZlOAw+qZxhyjMyWnaQ+VQeYPGAq5NbQ+tw8p4v7uTAwMA │
│                                                                                                                                                                                                                                                                                                                                     │
╰─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────╯
╭───────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Transaction Effects                                                                               │
├───────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Digest: FFtreqtLFYA8HcquG7NeRJzG9r5WuvMUvUCcqa3WNzJY                                              │
│ Status: Failure { error: "InsufficientCoinBalance in command 0" }                                 │
│ Executed Epoch: 7                                                                                 │
│ Mutated Objects:                                                                                  │
│  ┌──                                                                                              │
│  │ ID: 0x898db79b2fac4563de50c6152316b110854ffcf1568189a51b81bbeee07d0d8b                         │
│  │ Owner: Account Address ( 0xcf41631862715223daae395c1a40677c8c4d93352ccedf48ae351684c9b5236b )  │
│  │ Version: 9                                                                                     │
│  │ Digest: F1SQfemCfs7LMUoHaaomKkvPpJrLhZptchsB7EYeCssp                                           │
│  └──                                                                                              │
│ Gas Object:                                                                                       │
│  ┌──                                                                                              │
│  │ ID: 0x898db79b2fac4563de50c6152316b110854ffcf1568189a51b81bbeee07d0d8b                         │
│  │ Owner: Account Address ( 0xcf41631862715223daae395c1a40677c8c4d93352ccedf48ae351684c9b5236b )  │
│  │ Version: 9                                                                                     │
│  │ Digest: F1SQfemCfs7LMUoHaaomKkvPpJrLhZptchsB7EYeCssp                                           │
│  └──                                                                                              │
│ Gas Cost Summary:                                                                                 │
│    Storage Cost: 988000 MIST                                                                      │
│    Computation Cost: 1000000 MIST                                                                 │
│    Storage Rebate: 978120 MIST                                                                    │
│    Non-refundable Storage Fee: 9880 MIST                                                          │
│                                                                                                   │
│ Transaction Dependencies:                                                                         │
│    DjJ85r7PJ87NJVs7zipcaDo9eLpwGTHd5WSrmqZ72mKD                                                   │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
╭─────────────────────────────╮
│ No transaction block events │
╰─────────────────────────────╯

╭──────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Object Changes                                                                                   │
├──────────────────────────────────────────────────────────────────────────────────────────────────┤
│ Mutated Objects:                                                                                 │
│  ┌──                                                                                             │
│  │ ObjectID: 0x898db79b2fac4563de50c6152316b110854ffcf1568189a51b81bbeee07d0d8b                  │
│  │ Sender: 0xcf41631862715223daae395c1a40677c8c4d93352ccedf48ae351684c9b5236b                    │
│  │ Owner: Account Address ( 0xcf41631862715223daae395c1a40677c8c4d93352ccedf48ae351684c9b5236b ) │
│  │ ObjectType: 0x2::coin::Coin<0x2::sui::SUI>                                                    │
│  │ Version: 9                                                                                    │
│  │ Digest: F1SQfemCfs7LMUoHaaomKkvPpJrLhZptchsB7EYeCssp                                          │
│  └──                                                                                             │
╰──────────────────────────────────────────────────────────────────────────────────────────────────╯
╭───────────────────────────────────────────────────────────────────────────────────────────────────╮
│ Balance Changes                                                                                   │
├───────────────────────────────────────────────────────────────────────────────────────────────────┤
│  ┌──                                                                                              │
│  │ Owner: Account Address ( 0xcf41631862715223daae395c1a40677c8c4d93352ccedf48ae351684c9b5236b )  │
│  │ CoinType: 0x2::sui::SUI                                                                        │
│  │ Amount: -1009880                                                                               │
│  └──                                                                                              │
╰───────────────────────────────────────────────────────────────────────────────────────────────────╯
```