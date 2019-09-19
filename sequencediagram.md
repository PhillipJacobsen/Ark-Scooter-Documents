https://github.com/bramp/js-sequence-diagrams/blob/master/README.md



## Manually Generate Private Keys for app & scooter
App and Scooter will store hardcoded bridgechain private keys in memory. Every rider and scooter would need a unique build with its own hardcoded bridgechain wallet.

```sequence
Title: Device / App Wallet Init. (hack)

Note left of Desktop Wallet: generate wallets for scooter,app
Note left of scooter: keys hardcoded in flash
Note left of app: keys hardcoded in application
Desktop Wallet->scooter: send tokens
Desktop Wallet->app: send tokens

```

## Step 1 - Payment
Public Key of scooter is encoded in QRcode. App will need to include the public key of scooter in the rental start TX.
Rider selects # of minutes of play time and then prepays in ARK.

```sequence
Title: Step 1: Scan & Pay

scooter->scooter:Display QRcode(bridgechain public key)
app->app:Scan QRcode to get public key of scooter
app->app:Rider selects time.
app->Rider's Ark wallet:Payment info sent to Ark Wallet
Rider's Ark wallet->Company Wallet: send Ark payment
app->app:wait for Ark payment to be received in company wallet

```
## Step 2 -  Rental Session
App sends rental start tx. Scooter polls API(or maybe MQTT plugin) looking for rental start tx containing its own public key. Scooter is then unlocked until timer expires. Scooter locks and sends rental finish tx. App polls API(or maybe webhooks??) looking for rental finish tx containing its own public key. App displays rental summary.
```sequence
Title: Step 2: Rental Session

app->bridgechain:custom tx:rental start
app->app:Display ride starting message
bridgechain->scooter:custom tx:rental start
Note left of scooter: public key needs to match
scooter->scooter: store start time and GPS in memory
scooter->scooter:unlock scooter
scooter->scooter: IOT screen displays countdown timer,GPS
Note right of scooter:fun with scooter until timer expires
scooter->scooter:lock scooter
scooter->scooter:store end time and GPS in memory
scooter->scooter:IOT screen displays ride finished msg
scooter->bridgechain:custom tx:rental finish
bridgechain->app:custom tx: rental finish
Note right of app:public key needs to match
app->app:display ride stats(GPS start, GPS finish)

```


## Details of Custom TXs
### custom tx: rental start 
contains these items
- public key of scooter
- public key of app
- txid of Ark payment
- number of minutes of scooter time

### custom tx: rental finished
contains these items
- public key of scooter
- public key of app
- txid of ARK payment
- GPS start
- GPS finish
- number of minutes of scooter time

The rental finished transaction has the full details of the entire ride.
If you wanted to analyze all of the rides then I think you would only need to look at the rental finished messages.  


## Other details
- Scooter IOT will publish realtime GPS & battery level to MQTT broker
- Thingsboard Dashboard will display realtime map and stats
- App could subscribe to realtime GPS data if necessary. 
- There is no custom device register TX so there is no device registry that needs to be created as a custom plugin. In my mind a registry plugin to store the state information may be more work than the custom TX plugin



