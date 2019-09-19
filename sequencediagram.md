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
Public Key of scooter is encoded in QR code. App will need to include the public key of scooter in the rental start TX.
Rider selects # of minutes of play time and then prepays in ARK.

```sequence
Title: Step 1: Scan & Pay

scooter->scooter:Display QRcode(bridgechain public key)
app->app:Scan QRcode to get public key of scooter
app->app:Rider selects time.
app->Rider's ARK wallet:Payment info sent to ARK Wallet
Rider's ARK wallet->Company ARK Wallet: send ARK payment
app->app:wait for payment to be received in company wallet

```
## Step 2 -  Rental Session
App sends rental start tx. Scooter polls API(or maybe MQTT plugin) looking for rental start tx containing its own public key. Scooter is then unlocked until timer expires. Scooter locks and sends rental finish tx. App polls API(or maybe webhooks??) looking for rental finish tx containing its own public key. App displays rental summary.
```sequence
Title: Step 2: Rental Session

app->bridgechain:custom tx:rental start
app->app:Display ride starting message
bridgechain->scooter:custom tx:rental start
Note left of scooter: public key needs to match
scooter->scooter: record start time and GPS
scooter->scooter:unlock scooter
scooter->scooter: IOT screen displays countdown timer
Note right of scooter:fun with scooter until timer expires
scooter->scooter:lock scooter
scooter->scooter:record end time and GPS
scooter->scooter:IOT screen displays ride finished msg
scooter->bridgechain:custom tx:rental finish
bridgechain->app:custom tx: rental finish
Note right of app:public key needs to match
app->app:Display ride stats(GPS,timestamps)

```


## Details of Custom TXs
### custom tx: rental start 
- public key of scooter
- public key of app
- txid of ARK payment
- number of minutes of scooter time
- reserved data

### custom tx: rental finished
- public key of scooter
- public key of app
- txid of ARK payment
- reserved data
- number of minutes of scooter time
- start rental GPS
- start rental timestamp
- finish rental GPS
- finish rental timestamp


The rental finished transaction has the full details of the entire ride.
If you wanted to analyze all of the ride data then I think you would only need to look at the rental finished messages.  


## Other details
- Scooter IOT will publish realtime GPS & battery level to MQTT broker
- Thingsboard Dashboard will subscribe via MQTT to GPS and battery info and display on realtime map 
- Thingsboard Dashboard will subscribe via MQTT to bridgechain transaction events and display them in log
- There is no custom device registration TX so there is no device registry that needs to be created as a custom plugin. 



