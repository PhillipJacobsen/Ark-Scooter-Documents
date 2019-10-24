Tier0: Proof of Concept Scooter Rental DApp
===
**Overview prepared for Developer Round-table Oct 24, 2019**


## Project Overview
Create an electric scooter rental solution utilizing a mobile app and an associated Ark custom bridgechain. All communication between the App and the IOT device will be on chain through the use of custom transactions.  
This project will be a great demonstation of a real world application utilizing Ark tech.  It will be an example for how to code custom Ark transaction plugins. It will demonstrate C++ SDK running on "small" embedded processor.

This project will not integrate the electronics inside of an actual scooter however this integration could easily be accomplished as a future project if desired. This could be a great marketing demo for Ark team.

This project will create a foundation and template for future projects.


## Team

- **@emsy - Community member**
-- Custom Transaction Plugins
-- Bridgechain Deployment
-- IOS/ Andriod Client App
- **@pj (Phillip) - Community member**
-- Embedded Hardware/Firmware Development
-- off chain data IOT dashboard
- **@sleepdeficit - Ark Team technical coordinator**


## Main Components
- Ark Bridgechain with custom transactions
- Mobile App
- IOT device integrated in Scooter
- IOT dashboard

### Block Diagram
![](https://i.imgur.com/oFjWFi4.jpg)


## Mobile App
The core user interface of the project will be a mobile app for both iOS and Android. This mobile app will manage the following:
- QR code scanner
- Send rental pickup transaction and payment to the IoT physical device (lock) to manage the security of the scooter.
- Display statistics once ride has been completed
- Developed with Appcelerator using JavaScript


## Custom ARK Bridgechain + Custom Transactions
All information related to the rental will be stored on the blockchain via custom transactions.

Bridgechain Name: Radians
Token: RAD
Delegates: 53
Blocktime: 8 seconds
Explorer: [radians.nl](https://radians.nl/)

Ark core plugins will be developed for the custom transactions and App communication. 
Developed using NodeJS + Express + SocketCluster.



## Rental Session Sequence 
**Basic transaction concept shown below. Currently being developed..**

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




## IOT device
Battery powered embedded hardware device that contains WiFi, GPS, display, and electronic switch to control lock.  
- Generates QR code
- unlocks scooter when rental pickup message is received and sends rental dropoff message when time elapses.
- Developed in Arduino environment using C++ SDK


### Embedded Electronics
![](https://i.imgur.com/8kIXYTd.jpg)

![](https://i.imgur.com/MN1TPzu.jpg)


## Off Chain IoT Dashboard
Realtime data(GPS, Speed, Battery) will be streamed offchain via MQTT to an opensource IOT analytics platform (Thingsboard). This offchain data may be signed using private keys.

 ![](https://i.imgur.com/WNWRkS1.jpg)











