## Scooter Device Registration
```sequence
Title: Scooter Device Registration

Scooter Owner->bridgechain: custom tx(Registration)
Note right of Scooter Owner: Registration TX \n To: multisig(1:2 device/owner)\n Amount: Deposit  \n Fee: Registration \n Asset: Scooter Device Public Key
bridgechain->scooter: emit registration


```



## Rental Session Sequence

```sequence
Title: Rental Session   
app->app: start app
scooter->scooter:Display QR code:Public Key,GPS,Rate
scooter->app: scan QR code
app->app: Select Rental Duration
app->app: Finalize Payment
app->bridgechain:custom tx:(Rental start) to scooter address

Note right of app: Rental Start TX \n To: Scooter Address\n Amount: Rental Amount  \n Fee: Rental \n Asset: hash(Start GPS), time

app->app: wait for tx confirmation
app->app: display message in app


scooter->scooter: search for Rental Start
bridgechain->scooter:custom tx:Rental Start
Note right of scooter:verify hash. Refund if invalid

scooter->scooter: Unlock scooter
scooter->scooter: Record start time, display ride timer

Note right of app:fun with scooter until timer expires
scooter->scooter:lock scooter
scooter->scooter:record GPS, display ride finished msg

scooter->bridgechain:custom tx:(Rental finish)
Note right of scooter: Rental Finish TX \n To: Renter Address \n Amount: 0  \n Fee: Rental \n Asset:start & end GPS,rate,duration \n start timestamp


app->app: search for Rental finish
bridgechain->app:custom tx: rental finish

app->app:Display ride stats(GPS,time,etc)

```

Notes: 

The rental finish transaction has the full details of the entire ride. If you wanted to analyze all of the ride data then you would only need to look at the rental finished messages.  


## Other details
- Scooter IOT will publish realtime GPS & battery level to MQTT broker
- Scooter IOT will also publish via MQTT its current operating mode(parked, in use, low battery, broken, etc).
- Thingsboard Dashboard will subscribe via MQTT to GPS, battery, and operating mode and display on realtime map. 
- Thingsboard Dashboard will subscribe via MQTT to bridgechain transaction events and display them in log
- There is no custom device registration TX so there is no device registry that needs to be created as a custom plugin. 



