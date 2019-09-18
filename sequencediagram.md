https://github.com/bramp/js-sequence-diagrams/blob/master/README.md

participant scooter
participant bridgechain
participant app



```sequence



Title: Device / App Initialization (hack)

Note left of Desktop Wallet: generate wallets for scooter,app
Note left of scooter: store keys in memory
Note left of app: store keys in memory
Desktop Wallet->scooter: send tokens
Desktop Wallet->app: send tokens

```


```sequence


alice->bo: test
```