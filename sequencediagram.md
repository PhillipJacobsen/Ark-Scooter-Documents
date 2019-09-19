https://github.com/bramp/js-sequence-diagrams/blob/master/README.md

participant scooter
participant bridgechain
participant app



```sequence



Title: Device / App Wallet Init. (hack)

Note left of Desktop Wallet: generate wallets for scooter,app
Note left of scooter: keys hardcoded in flash
Note left of app: keys hardcoded application
Desktop Wallet->scooter: send tokens
Desktop Wallet->app: send tokens

```


```sequence
Title: Step 1: Scan & Pay

scooter->scooter:Display QRcode(bridgechain public key)
app->app:Scan QRcode to get public key of scooter
app->app:Rider selects time.
app->Rider's Ark wallet:Payment intent sent to Ark Wallet
Rider's Ark wallet->Company Wallet: send Ark payment
app->app:wait for Ark payment to be received in company wallet

```

```sequence
Title: Step 2:Record start of transaction

app->bridgechain:custom tx:rental start
app->app:Display ride starting message
bridgechain->scooter:custom tx:rental start
Note left of scooter:look for tx with its own public key
scooter->scooter: record start time and GPS in memory
scooter->scooter:unlock scooter
scooter->scooter: IOT screen displays countdown timer, GPS coordinates
Note right of scooter:have fun with scooter until timer expires
scooter->scooter:lock scooter
scooter->scooter:IOT screen displays ride finished message
scooter->bridgechain:custom tx:rental finish
bridgechain->app:custom tx: rental finish
Note right of app:look for tx with it's own public key
app->app:display ride stats(GPS start, GPS finish)

```

---
## Details of Custom TXs
### custom tx: rental start 
contains these items
- txid of Ark payment
- public key of scooter
- amount of scooter time

### custom tx: rental finished
contains these items
- public key of app
- GPS of start
- GPS of finish
- txid of ark payment
- amount of scooter time

The rental finished transaction has the full details of the entire ride.
If you wanted to analyze all of the rides then I think you would only need to look at the rental finished messages.  


## Other details
- Scooter IOT will publish realtime GPS & battery level to MQTT broker
- Thingsboard Dashboard will display realtime map and stats
- App could subscribe to realtime GPS data if necessary. 

