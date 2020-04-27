
Proof of Concept Ark Scooter Rental DApp
===
[Tier 0 Program](https://ark.io/projects/ark-scooters)

https://hackmd.io/OuQMzbK6TaClVLTHu97fSg

## Table of Contents

[TOC]

# Project Overview
This project is a proof of concept of an electric scooter rental solution utilizing a mobile app and an associated Ark custom bridgechain to record the rental contract created. 
This project is a great illustration on how to code and interact with custom Ark transactions. It will demonstrate C++ SDK running on "small" embedded processor.

This project will not integrate the electronics inside of an actual scooter however this integration could easily be accomplished as a future project if desired. 

This POC is a great foundation and template for future projects.


# Team

- **@emsy - Community Member**  
-- Custom Transaction Plugins  
-- Bridgechain Deployment  
-- IOS/ Andriod Client App
- **@pj (Phillip) - Community Member**  
-- Embedded Hardware/Firmware Development  
-- Off Chain Data IOT Dashboard
- **@sleepdeficit - Ark Team Technical Coordinator**   
-- C++ library support for custom transactions   
- **@Matthew DC - Ark Team Project Specs**   
- Thanks to @console [deadlock] for developing MQTT core plugin


# Functional Requirements Defined Prior to Start of Project 
Create an electric scooter rental solution utilizing a mobile app and an associated Ark custom bridgechain to manage locking, unlocking, deposits, locations, and management of  Scooter rentals. All communication between the App and the IOT device will be on chain through the use of custom transactions.

## Components

### Mobile App
The core user interface of the project will be a mobile app for both iOS and Android. This mobile app will manage the following:
<!-- - Basic customer Onboarding -->
<!-- - Booking -->
<!-- - Real-time GPS tracking of available scooters using Google Maps -->
- QR code / ID scanner integration
- Send rental pickup transaction to the IoT physical device (lock) to manage the security of the scooter.
- In-app payments in the Bridgechain Token
- Display statistics once ride has been completed
<!-- - Show and track drop-off locations once a scooter has been rented -->
<!-- - Manage and track time and distance of rental (from pick-up to drop-off) -->
<!-- - Process deposit and fees on drop-off at a designated location -->
<!-- - Make the scooter available for rental after drop-off is completed -->

### IOT device
Battery powered embedded hardware device that contains WiFi, GPS, display, and electronic switch to control lock.  
- Generates QR code
- unlocks scooter when rental pickup message is received and sends rental dropoff message when time elapses.
- streams realtime GPS data to analytics server
 

### Custom ARK Bridgechain
All information related to the rental will be stored on the blockchain. This will be accomplished through several potentially new custom transaction types as follows:
- Device Registration Transaction (to register a new scooter)
- Rental Pick-up / Drop-off Transaction  

Administration functions to handle the registration of scooters and locations will not be implemented in the demo app. The transactions could be demonstrated by some script/tool

### Provided by the ARK.io Team
- The custom mobile app UI design
- Additional guidance and support as necessary

### Requirements for Completion
- Provide a mobile application that meets the above minimum criteria.
- Provide a functioning custom ARK Bridgchain blockchain with the above custom transactions and functionality
- Demonstrate the application working as described
- Provide a Bill of Materials (BOM) for the required IoT hardware.
- Project will not include final integration of electronics into scooter hardware. 


## Milestones
We both agreed to split the amount of funding, each contributor will have 12.5k to diversify over the assigned milestones. After completed approved by the Ark team the contributer is egible to request a payment.


#### IOT Hardware procurred, detailed hardware block diagram, IOT communication protocol defined, IOT analytics servers deployed, Firmware/Electronics v0.1 (pj) - 5250‬ ARK
- demonstration of basic opertaion of hardware peripherals (GPS, timer, TFT display, QR code generation)
- custom transaction interface not complete
#### Firmware/Electronics V0.2 (pj) - 3500‬ ARK
- final feature set to support App v0.2
#### Analytics Dashboard (pj) - 1250‬ ARK
---
#### Final Detailed Technical Specification + project preparation (emsy + pj) - 750 ARK(pj). 500 ARK(emsy)
#### Custom Transaction Structure & Flow Defined (emsy + pj) - 1000 ARK(pj). 1000 ARK(emsy)
#### Working Demo(final milestone) (Electronics not integrated into scooter) (pj + emsy) - 750 ARK(pj). 750 ARK(emsy)
- Video of working product. Performance could be verified by Simon.
---
#### V2.6 Ark Bridgechain Deployed (emsy) - 750 ARK
#### Custom Transactions Created (emsy) - 1500 ARK
#### Custom Core Plugins(app communication) Implemented (emsy) - 1500 ARK
#### App UI Mockup (emsy) - 500 ARK
#### App v0.1 (emsy) - 3000 ARK
- scan QR code containing scooter public key
- Process payments in BridgeChain Token to unlock the device

#### App v0.2 (emsy) - 3000 ARK
- Manage and track time of rental (from pick-up to drop-off)
- Display ride stats when rental is complete
- Make the scooter available for rental after drop-off is completed

## Project Costs
Applications could be optimized to operate on 1 or 2 VPS. Using separate services at the beginning will reduce implementation time.
- MQTT server - $19 USD/Month (pj)
- Node Red - Free Monthly Plan (pj)
- Thingsboard - $20 USD/Month (pj)
- Ark bridgechain 1 VPS with 2 CPU, 4GB RAM, 150GB SSD, 5TB pooled traffic +- $30 USD/Month (emsy)
    - Might need more RAM, this can be added at any time at a cost of +- 10$ / Month per 1GB.
- 1 sets of Prototype Electronics (pj): 
    - ESP32, TFT screen, GPS module, Antenna, Battery
    - ~$125->$175 USD per set


---


# Technical Specification


## Github Repositories 
**Project Documentation**  
https://hackmd.io/OuQMzbK6TaClVLTHu97fSg  
https://github.com/PhillipJacobsen/Ark-Scooter-Documents

**Scooter Firmware**  
https://github.com/PhillipJacobsen/Ark_Scooter

**iOS/Android DApp Source**  
https://github.com/e-m-s-y/scooter-app

**Radians Bridgechain**  
https://github.com/e-m-s-y/radians  
**Explorer:** https://radians.nl

**Custom Transaction Plugin**  
https://github.com/e-m-s-y/scooter-transactions

**Utility for Sending Test Transactions**  
https://github.com/e-m-s-y/scooter-transactions/blob/master/src/test.js

**Socket Event Forwarder Core Plugin**  
https://github.com/e-m-s-y/socket-event-forwarder

**MQTT Event Forwarder Core Plugin**  
https://github.com/deadlock-delegate/mqtt

**Node-Red Flow Backup**  
https://github.com/PhillipJacobsen/Ark_Scooter/tree/master/NodeRed

**ThingsBoard Dashboard Backup**  
https://github.com/PhillipJacobsen/Ark_Scooter/tree/master/ThingsBoard

**Public IoT Dashboard**  
http://165.22.237.171:8080/dashboard/f88894b0-d519-11e9-b281-0bd830c6c87f?publicId=f62146f0-cb7c-11e9-b281-0bd830c6c87f

**Ark-CPP-crypto v1.0.0**  
(fork of Standard Ark Crypto library with support for Radians Custom Transactions)  
https://github.com/sleepdefic1t/cpp-crypto/tree/chains/radians

**Ark-CPP-client v1.4.0-arduino**  
https://github.com/ArkEcosystem/cpp-client/pull/159

**arkcrypto-browserified**  
Enables you to use the @arkecosystem/crypto package in the browser  
https://github.com/e-m-s-y/arkcrypto-browserified

---

## System Block Diagram

The core functions of the rental process and the communication between the DApp and embedded hardware in the scooter are done through on chain custom bridgechain transactions.  

A secondary feature is the offchain communication between the bridgechain and embedded hardware with an IoT analytics dashboard.  

The rental DApp(iOS/Android) receives blockchain transactions via a custom Socket.io communication plugin running on a relay node. DApp sends blockchain transactions via RESTful API.

The scooter firmware sends and receives blockchain transactions via the RESTful API.

All data received by analytics dashboard is via MQTT messaging protocol.

The blockchain is a custom ARK.io bridgechain called Radians.

![](https://i.imgur.com/rTUXbkW.jpg)



---

## Bridgechain Specifications

Bridgechain Name: Radians  
Ark core V2.6.0-next.7 Testnet (as of April 14, 2020)  
https://radians.nl/api/node/configuration for more node details.  
Token: RAD  
Delegates: 53  
Blocktime: 8 seconds  
Explorer: [radians.nl](https://radians.nl/)  
Peer / Seed server: http://37.34.60.90:4040  
Epoch: 2019-10-25T09:05:40.856Z  

**VPS Specifications**  
- 2 CPU
- 4GB RAM
- 150GB SSD
- 5TB pooled traffic running on CentOS 7.7.1908

### Detailed Bridgechain Configuration
https://radians.nl/api/node/configuration
```
{
   "data":{
      "core":{
         "version":"2.6.0-next.7"
      },
      "nethash":"f39a61f04d6136a690a0b675ef6eedbd053665bd343b4e4f03311f12065fb875",
      "slip44":1,
      "wif":206,
      "token":"RAD",
      "symbol":"R",
      "explorer":"http://0.0.0.0:4200",
      "version":65,
      "ports":{
         "@arkecosystem/core-p2p":null,
         "@arkecosystem/core-api":4103
      },
      "constants":{
         "height":1850,
         "reward":200000000,
         "activeDelegates":53,
         "blocktime":8,
         "block":{
            "version":0,
            "maxTransactions":150,
            "maxPayload":6291456
         },
         "epoch":"2019-10-25T09:05:40.856Z",
         "fees":{
            "staticFees":{
               "transfer":10000000,
               "secondSignature":500000000,
               "delegateRegistration":2500000000,
               "vote":100000000,
               "multiSignature":500000000,
               "ipfs":500000000,
               "multiPayment":100000000,
               "delegateResignation":2500000000,
               "htlcLock":10000000,
               "htlcClaim":0,
               "htlcRefund":0
            }
         },
         "vendorFieldLength":512,
         "multiPaymentLimit":256,
         "aip11":true,
         "htlcEnabled":true
      },
      "transactionPool":{
         "dynamicFees":{
            "enabled":true,
            "minFeePool":3000,
            "minFeeBroadcast":3000,
            "addonBytes":{
               "transfer":100,
               "secondSignature":250,
               "delegateRegistration":400000,
               "vote":100,
               "multiSignature":500,
               "ipfs":250,
               "multiPayment":500,
               "delegateResignation":400000,
               "htlcLock":100,
               "htlcClaim":0,
               "htlcRefund":0
            }
         }
      }
   }
}
```

---

## Adding Radians Bridgechain to Ark Desktop
The following instructions can be used to add Radians chain to the standard Ark desktop wallet. The following instructions were tested on Windows 10 and version 2.9.1 of the wallet.
1. Download and install Ark.io desktop wallet from one of the following locations.
    * https://ark.io/wallet 
    * https://github.com/ArkEcosystem/desktop-wallet/releases
2. Run ARK Desktop Wallet
3. Go to Network(the cloud icon on the bottom left)->Manage networks 
4. Add a new network and fill in the following info:
    * Name: Radians
    * Description: Radians Testnet
    * Seed Server: http://37.34.60.90:4040
5. Press Fetch
    * The network should be found.
    * Press Save and you should get message saying "validating network"
6. Go to Profile(bottom icon on the left) -> Add profile
7. Fill in Profile Name (whatever you want to call it)
    * Press next
8. Select Radians custom network and press next
9. Select appearance options and then press done

Note: I find that it does not automatically find the peer.  
How to connect to custom peer:
1. Network->Connect custom peer and fill in these details
    * Protocol + IP / Hostname: http://37.34.60.90
    * Port: 4040
2. Press Connect

You should now be able to create or import a Radians wallet.


## Scooter - DApp Communication Sequence Diagrams

### Manually generate private keys for app & scooter
DApp and Scooter private keys are manually generated in desktop wallet.  

Scooter stores hardcoded bridgechain private keys in memory. Current firmware requires every scooter to use a unique build with its own hardcoded bridgechain wallet.  

DApp allows rider to type in private keys.

```sequence
Title: Scooter / DApp Wallet Init.

Note left of Desktop Wallet: generate wallets for scooter,DApp
Note left of scooter: keys hardcoded in flash
Note left of DApp: keys typed into DApp
Desktop Wallet->scooter: send tokens
Desktop Wallet->DApp: send tokens

```


### Scooter Device Registration Sequence
There is no automatic IOT device registration feature. Devices are registered using custom Javascript utility

```sequence
Title: Scooter Device Registration

Scooter Owner->bridgechain: custom tx(Registration)
Note right of Scooter Owner: Registration TX \n To: multisig(1:2 device/owner)\n Amount: Deposit  \n Fee: Registration \n Asset: Scooter Device Public Key, other....
Note right of bridgechain:  emit registration complete 

```

### Rental Session Sequence

```sequence
Title: Rental Session   
app->app: start app
scooter->scooter:Display QR code:Public Key,random hash,Rate, GPS coordinates
scooter->app: scan QR code
app->app: Select Rental Duration
app->app: Finalize Payment
app->bridgechain:custom tx:(Rental start) to scooter address

Note right of app: Rental Start TX \n To: Scooter Address\n Amount: Rental Amount  \n Fee: Rental \n Asset: hash(random SHA256), GPS

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
---

## Rental Session Screenshots
The following screenshots of the app, scooter, and analytics dashboard illustrates the sequence of a rental transaction.

### Step 1: Scooter Bootup  
**Scooter displays boot screen while waiting for waiting for WiFi connection**  
![](https://i.imgur.com/Uv2taZn.jpg =200x)  

**Scooter A status is broken while it waits for GPS sync**
![](https://i.imgur.com/qfOYwE8.png)


### Step 2 Scooter Ready for Rental   
**Once all of the networks are connected then QR code is displayed**  
![](https://i.imgur.com/c9PhRlZ.jpg =200x)


### Step 3 App Bootup  
**Press the '+' on the top right to open camera for QR code scanning**  
![](https://i.imgur.com/bWRdbfK.png =200x)

### Step 4 App Ready for QR Scanning  
**You can scan QR code via camera or via file for testing**  
![](https://i.imgur.com/y5SrxYy.png =200x)

### Step 5 App Scanning QR code  
**You would need to zoom in more to scan QR code**  
![](https://i.imgur.com/j4Fs3fF.jpg =200x)

### Step 6 App Configure Ride Length  
**Use slider to configure the length of the ride**  
![](https://i.imgur.com/fN8whde.png =200x)

### Step 7 App Sends Rental Start  
**Rental Start Transaction is sent along with payment to Scooter**  
![](https://i.imgur.com/3wytmbB.png =200x)

### Step 8 Scooter Rental in Progress  
**Once Rental Start transaction is received the scooter unlocks and starts ride timer.**  
Speed and rental countdown timer are displayed.  
Rental Finish transaction is sent once timer expires.  
![](https://i.imgur.com/C8IiTgU.jpg =200x)  

**Scooter A status is now Rented.**  
GPS, Battery, Speed are updated in realtime via MQTT  
Radians Scooter.Rental.Start panel shows the latest transaction event received via blockchain
![](https://i.imgur.com/41xEkH0.png)


### Step 9 App Rental in Progress  

![](https://i.imgur.com/M46OIDw.png =200x)

### Step 10 App Received Rental Finish  
**App receives Rental Finish transaction from scooter when ride timer elapses.**  
![](https://i.imgur.com/855lBDf.png =200x)  

**Scooter A status is now available.**  
Radians Scooter.Rental.Finish panel shows the latest transaction event received via blockchain  
![](https://i.imgur.com/Sh36GnX.png)


---
## Rental Session Video Screenshots

### Rental Session using App and Test Utility to Emulate Scooter
https://www.youtube.com/watch?v=Jxn2BhQjYgY




### Analytics Dashboard During Rental Session
https://youtu.be/QSazY9Nj_Pc

---

## Custom Transaction and Wallet Attributes Design

### Transaction Types
TYPE_GROUP: 4000  
SCOOTER_REGISTRATION_TYPE: 401  
RENTAL_START_TYPE: 500  
RENTAL_FINISH_TYPE: 600  

### Scooter Registration

***Note: data types and length needed to be updated***

**From:** Scooter  
* type = SCOOTER_REGISTRATION_TYPE  
* typeGroup = TYPE_GROUP  
* fee = Register = xxxxx  

**Scooter Register Example:**
https://radians.nl/api/v2/transactions/444b5172476a7f86b38392eaeffcd1bf35123cdd83b44c96aaa597e24c05006e
```
{
   "data":{
      "id":"444b5172476a7f86b38392eaeffcd1bf35123cdd83b44c96aaa597e24c05006e",
      "blockId":"7142238589308015273",
      "version":2,
      "type":401,
      "typeGroup":4000,
      "amount":"0",
      "fee":"3000000000",
      "sender":"TRXA2NUACckkYwWnS9JRkATQA453ukAcD1",
      "senderPublicKey":"03e063f436ccfa3dfa9e9e6ee5e08a65a82a5ce2b2daf58a9be235753a971411e2",
      "recipient":"TRXA2NUACckkYwWnS9JRkATQA453ukAcD1",
      "signature":"2ad52e6d3c927c66b7f0760f05311d48cb22ec124315745d4c842170c869e31c73f16fe53f1ad3d8c5eb2a61076a776d0a759c4029cbb31c1aa9dedb97028898",
      "asset":{
         "scooterId":"1234567890"
      },
      "confirmations":846380,
      "timestamp":{
         "epoch":9109608,
         "unix":1581103948,
         "human":"2020-02-07T19:32:28.856Z"
      },
      "nonce":"41"
   }
}
```


### Rental Start
***Note: data types and length needed to be updated***

**From:** App  
**To:** Scooter  
* type = RENTAL_START_TYPE  
* typeGroup = TYPE_GROUP  
* version = 2  
* fee = Rental = xxxxx  
* amount = number  
* vendorField = optional
* asset = {sessionID, gps: {[timestamp, lat, long]}, rate}  
    * sessionID = SHA256  
    * timestamp = {epoch: integer}, {human: string}  
    * lat = GPS latitude; String(1->16 characters)  
    * long = GPS longitude; String(1->16 characters)  
    * rate = integer

**Note:**  
SessionID, GPS coordinates, and rate are values that are generated by scooter and embedded in the QR code that the app scans.  
Hash is SHA256 of random number.  
Rate is the cost of the ride measured in RAD/seconds.  
The amount transferred determines the length of ride.  
Length of Ride(seconds) = Amount / Rate

**Rental Start Example:**
https://radians.nl/api/v2/transactions/c9dbbede340926fab174e56fd3cea75b3b99a1cc9eb594f18e7250fbd11392e7

```
{
   "data":{
      "id":"c9dbbede340926fab174e56fd3cea75b3b99a1cc9eb594f18e7250fbd11392e7",
      "blockId":"2072591193193033951",
      "version":2,
      "type":500,
      "typeGroup":4000,
      "amount":"3700020",
      "fee":"10000000",
      "sender":"TLdYHTKRSD3rG66zsytqpAgJDX75qbcvgT",
      "senderPublicKey":"02cbe4667ab08693cbb3c248b96635f84b5412a99b49237f059a724f2cfe2b733f",
      "recipient":"TRXA2NUACckkYwWnS9JRkATQA453ukAcD1",
      "signature":"84315ff2c7382a0986c326daac84fe076e4a963a31d87ef710904f37c28d4657e9c3a3696d3b2ae33c557f13b727a188c440f23387040cd2657c1b01b8ab9c7b",
      "asset":{
         "gps":{
            "timestamp":1585720792,
            "latitude":"53.534603",
            "longitude":"-113.329002",
            "human":"2020-04-01T05:59:52.000Z"
         },
         "sessionId":"bc9583e4c8094c7a84fc6dc0ec916d7e1a8fdac3dcaf2dcbec8073babaa00165",
         "rate":"61667",
         "gpsCount":1
      },
      "confirmations":269412,
      "timestamp":{
         "epoch":13726456,
         "unix":1585720796,
         "human":"2020-04-01T05:59:56.856Z"
      },
      "nonce":"104"
   }
}
```


---



### Rental Finish
https://radians.nl/api/v2/wallets/TGGUtM6KPdWn7LSpNcWj1y5ngGa8xJqxHf/scooter-transactions

***Note: data types and length needed to be updated***

**From:** Scooter  
**To:** App  

* type = RENTAL_FINISH_TYPE: 500  
* typeGroup = TYPE_GROUP  
* version = 2  
* fee = Rental = xxxxxxx  
* amount = number  
* vendorField = optional
* asset = {SessionID, gps: {[start timestamp, lat, long],[finish timestamp, lat, long] }, rideDuration}  
    * sessionID = SHA256
    * timestamp = {epoch: integer}, {human: string}  
    * lat = GPS latitude; String(1->16 characters)  
    * long = GPS longitude; String(1->16 characters)  
    * rideDuration = RIDE_DURATION_IN_SECONDS

**Rental Finish Example:**
https://radians.nl/api/v2/transactions/6ad85654597fe9fab5f61930f0eccfb02cbb892fbfc78b91d723797d82408c6d
```
{
   "data":{
      "id":"6ad85654597fe9fab5f61930f0eccfb02cbb892fbfc78b91d723797d82408c6d",
      "blockId":"18274364918586419922",
      "version":2,
      "type":600,
      "typeGroup":4000,
      "amount":"1",
      "fee":"10000000",
      "sender":"TRXA2NUACckkYwWnS9JRkATQA453ukAcD1",
      "senderPublicKey":"03e063f436ccfa3dfa9e9e6ee5e08a65a82a5ce2b2daf58a9be235753a971411e2",
      "recipient":"TLdYHTKRSD3rG66zsytqpAgJDX75qbcvgT",
      "signature":"30440220295d8140f99bf8a9b3a2c576f94f6e93ce44060f38d3c927e1301166525eb15602201a4be28023b3c3d50fc639f699c13340acb984aab01824667c861e3463b500a2",
      "asset":{
         "gps":[
            {
               "timestamp":1585720806,
               "latitude":"53.534560",
               "longitude":"-113.329120",
               "human":"2020-04-01T06:00:06.000Z"
            },
            {
               "timestamp":1585720866,
               "latitude":"53.534724",
               "longitude":"-113.328960",
               "human":"2020-04-01T06:01:06.000Z"
            }
         ],
         "sessionId":"bc9583e4c8094c7a84fc6dc0ec916d7e1a8fdac3dcaf2dcbec8073babaa00165",
         "containsRefund":false,
         "gpsCount":2,
         "rideDuration":60
      },
      "confirmations":269413,
      "timestamp":{
         "epoch":13726528,
         "unix":1585720868,
         "human":"2020-04-01T06:01:08.856Z"
      },
      "nonce":"131"
   }
}
```


---

### Custom Wallet Attributes
Two custom wallet attributes were created to implement a semaphore mechanism to control shared access of the scooter. The attributes are also used to control which custom transactions are available based on wallet type. Example: Rental Start transactions can only be sent by DApp and Rental Finish transactions can only be sent by scooters.


```
module.exports = {  
    IS_REGISTERED_AS_SCOOTER: "isRegisteredAsScooter",  
	IS_RENTED: "isRented"  
};
```

When a scooter wallet sends the custom ***Register Scooter*** transaction the ***IS_REGISTERED_AS_SCOOTER*** attribute is set to TRUE.  
If you try to register the scooter a second time, the transaction will be rejected by the node and not added to the transaction pool.  

When the DApp wallet sends a custom ***Rental Start*** transaction two wallet attributes are checked. The node will reject the transaction if the receiving wallet is not registered as a scooter. The node will reject the transaction if the receiving wallet attribute ***IS_RENTED*** is true. If the attribute is false then the transaction will be accepted and attribute will be set true.  

**NOTE: Need to confirm that the following is implemented:**  ***Rental Finish*** transaction will be rejected by the node if the wallet is not registered as a scooter. ***Rental Start*** transaction will be rejected by the node if sent by wallet registered as scooter.





---

## Embedded Electronics

The highlighted section in the following diagram shows the implemented components of the embedded electronics. The dotted line section shows how the current project could be integrated into an existing of the shelf electrical scooter for a completely functional demonstration.

![](https://i.imgur.com/8kIXYTd.jpg)

![](https://i.imgur.com/MN1TPzu.jpg =500x)



**Embedded Processor**  
The ESP32 Feather module is a 32bit highly integrated System on Chip(SoC) processor. The module integrates a 240MHz dual-core Tensilica LX6 microcontroller with 520KB SRAM, 4MB Flash, 802.11b/g/n HT40 Wi-Fi, and power supply.

Several peripheral devices are interfaced to the ESP32 module to provide the necessary I/O. 

**Peripheral devices:**
- A GPS module is used to provide location data for the scooter. The module includes an onboard antenna however an external antenna was used for significant gain especially when testing indoors  
- A small 2.4" TFT display is used for the user interface. It generates dynamic QRcodes as well as displaying ride statistics.
- A wifi hotspot provides the internet connection for communicating to Ark bridgechain and analytics dashboard. A GSM module could be integrated as a future upgrade.
- The lock/unlock security mechanism is a relay to control lock or power system of physical scooter



### Bill of Materials 

| Component                     | Adafruit Part # | Digi-Key Part #|
| ---------------------------- | -------------- | -------------- |
| HUZZAH32 ESP32 FEATHER       | 3619           | 1528-2515-ND   |
| ULTIMATE GPS FEATHERWING     | 3133           | 1528-1695-ND   |
| FEATHERWING 2.4" 320X240 LCD | 3315           | 1528-1802-ND   |
| FEATHERWING DOUBLER          | 2890           | 1528-1535-ND   |
| RF ANT - SMA (optional)      | 960            | 1528-1170-ND   |
| SMA to uFL Adapter (optional)| 851            | 1528-2053-ND   |
| Lithium Ion Battery - JST-PH | 2011           |                |

#### Future/Optional (Integration into physical scooter)
- xiaomi m365 is a common scooter that rideshare companies rebranded for their service launch in 2018/2019
- The large rideshare companies are now starting to create modified electronics and upgraded scooters.
- There seems to be an easily accessible serial interface available for reading out data from the m365 scooter.


---

## Embedded Firmware
Firmware is developed using Arduino / PlatformIO environment and Ark C++ SDK.  

### Arduino Development Environment Setup
The following are detailed steps on setting up Arduino programming environment.  
The following process is testing on Windows 10 environment but should be similar on other operating systems.
1. Download and install Arduino  
    * https://www.arduino.cc/en/Main/Software
2. Run Arduino
3. Install ESP32 processor board hardware library
    1. File->Preferences  
    2. Enter https://dl.espressif.com/dl/package_esp32_index.json into the “Additional Board Manager URLs” field and select ok
    3. Open the Boards Manager. Tools->Board->Boards Manager
    4. Search for ESP32 and install "ESP32 by Espressif Systems" version 1.0.4.  Some times this can take a while to download
    5. ESP32 support should now be installed  

### Install Firmware Library Dependencies
The following are steps to install dependencies for the Scooter fimware project. 

Install the following libraries via the Arduino library manager.  
Tools->Manage Libraries.  
You can then search and add each of the following libraries and versions indicated.

* EspMQTTClient by Patrick Lapointe Ver 1.8.0
* PubSubClient by Nick O'Leary Ver 2.7.0 
* Adafruit GPS by Adafruit Ver 1.4.1
* Adafruit GFX by Adafruit Ver 1.7.5
* Adafruit Touchscreen by Adafruit 1.0.5
* Adafruit ILI9341 by Adafruit Ver 1.5.4
* Adafruit STMPE610 by Adafruit Ver 1.1.1
* QRCode by Richard Moore Ver 0.0.1
* ArduinoJson by Benoit Blanchon Ver 6.13.0
* BIP66 by Ark Ecosystem Ver 0.3.2
* bcl by Project Nayuki Ver 0.0.5
* micro-ecc by Kenneth MacKay Ver 1.0.0
* Ark-Cpp-Client by Ark Ecosystem V 1.4.0-arduino

### Installing Ark SDK Crypto C++ Library with support for custom Radians bridgechain transactions
The standard Ark-Cpp-Crypto (Ver 1.0.0) by Ark.io was forked to include custom Radians transaction support.(thanks to @sleepdeficit for support)  

1. Download the chains\Radians branch(not the main branch) from:
    * https://github.com\sleepdefic1t\cpp-crypto\tree\chains\radians
2. Move cpp-crypto folder to \Arduino\libraries
3. rename cpp-crypto to Ark-Cpp-Crypto  

A bash script needs to be executed to format the library for use with Arduino development. Windows10 does not have native support for this. I use "git for windows" which has gitbash included.  
https://gitforwindows.org/  
After installation of gitbash right click in \Ark-Cpp-Crypto\extras\ folder and select "GIT Bash Here".

4. gitbash shell window should open. Run "sh ARDUINO_IDE.sh"
    * script should start and ask for confirmation to continue. Press y
    * script should complete with message "You can now use Cpp-Crypto with the Arduino IDE".




### Library Modification
In the Arduino\libraries folder open \PubSubClient\src\PubSubClient.h  
Change this line: #define MQTT_MAX_PACKET_SIZE 128 
to:   #define MQTT_MAX_PACKET_SIZE 512


### Configure WiFi credentials in Firmware
open firmware file secrets.h
Configure the WiFi credentials with your network details.  
```
  #define WIFI_SSID         "*****"
  #define WIFI_PASS         "*****"
```

### Configure Wallet Credentials in Firmware
The project code includes Radians blockchain private keys embedded in source code. This is of course a terrible idea for a real project but convenient for development.  The included wallet has already been registered on the Radians chain via custom Register Scooter transaction.

Another address can be configured by editing the following lines in secrets.h  
```
const char* ArkAddress = "TRXA2NUACckkYwWnS9JRkATQA453ukAcD1";  
static const auto PASSPHRASE = "afford thumb forward wall salad diet title patch holiday metal cement wisdom";  
```

**Instructions for sending Register Scooter transaction:**  
Scooter wallet must be registered before being able to send or received Rental Transactions.
https://hackmd.io/OuQMzbK6TaClVLTHu97fSg?view#Custom-Transaction-Test-Tool


### Compiling Scooter Firmware
1. Download Scooter firmware: 
https://github.com/PhillipJacobsen/Ark_Scooter
2. Open Ark_Scooter.ino in Arduino
3. TBD: Change compiler error/warning settings(not needed in windows)
    * Todo need to check this for compilation on MacOS 
    * need to check default error/warning settings after installing Arduino
5. Select the processor board 
    * Tools->Board->Adafruit ESP32 Feather
6. Compile Firmware
    * Sketch->Verify/Compile

### Download Firmware
1. Connect the ESP32 Feather module to PC via USB cable.  Serial -> usb device drivers should have been installed during the installation of the Arduino software.  
2. Select COM port
    * Tools->port
3. Compile and upload
    * Sketch->Upload

---

### QR code Specification
The scooter will generate and display a QR code when it is available for rent. The code embedds the following parameters:
- Scooter Wallet Address: (34 characters)
- SessionID: SHA256 Hash of Unique/Random number. 256 bits
- Rental Rate: Cost per second of ride time
- GPS Latitude: Current location of scooter
- GPS longitude: Current location of scooter

#### SessionID
The sessionID is a random identifier that is unique to a Rental transaction. The QR code, Rental Start, and Rental Finish transactions all embed this unique identifier.  
1. Scooter generates random 32 bit integer. SHA256 hash fuction is performed generating 256 bit result. This is used as the SessionID.  
2. App scans QR code which includes the SessionID. Apps sends Rental Start transaction with SessionID embedded.
3. Scooter receives Rental Start and verifies received SessionID matches the value encoded in the QRcode
4. Scooter sends Rental Finish and embedds SessionID
5. App receives Rental Finish and confirms SessionID matches what it sent in Rental Start


**NOTE:** GPS coordinates would need to be rounded as the value is not static even if the device is stationary. Rounding to the third decimal place is about 110m of precision. Accuracy of the readings is also a concern as you could get erroneous readings. QR code needs to be static.
Does the app actually require the GPS coordinates to be received at the start of the rental? Perhaps the coordinates could be removed.  

#### Example of String Encoded in QRcode
rad:TRXA2NUACckkYwWnS9JRkATQA453ukAcD1?hash=e4c18e33a25a1b8eec69c61fcc171e3503b21a80cada4d5bc78c037bd239c3b1&rate=61667&lat=53.535500&lon=-113.278236  

![](https://i.imgur.com/iA4B1S3.jpg =225x)

---

### Status Panel on Scooter Display
The bottom portion of the scooter display provides status of all the network connections and system parameters.

#### Top Row of Status Panel
"Speed(kmh) via GPS"  "Time(via NTP server)" "WiFi Signal Strength"

#### Middle Row of Status Panel
"WiFi Connection" "MQTT Broker Connection" "Battery Voltage"

#### Bottom Row of Status Panel
"GPS Signal Lock" "Ark Node Connection" "# of GPS satellites"


### Communication with Radians Bridgechain
The ESP32 is assigned a unique Bridgechain address and stores its private key in Flash memory. This is certainly a terrible idea for real production product but is fine for prototyping. Secure storage methods will be an optional enhanced feature.  


The ESP32 will be able to send device registration transactions and optionally use its private key to sign / encrypt messages sent offchain. Transactions will use the public Bridgechain API.

### Communication with Analytics platform



### Detailed Firmware Description
TBD

---


## DApp - Rider Mobile Application

### Development Environment
Cross-platform tool called Appcelerator (https://appcelerator.com) was used to develop the app. This tool allows you to develop mobile apps in JavaScript and compile them to native code(Java for Android or Objective C for iOS). The Appcelerator SDK used is Ti 8.3.0.  

Webpack(https://webpack.js.org/) was used in order to get the @arkecosystem/crypto (https://www.npmjs.com/package/@arkecosystem/crypto/v/2.6.0-next.7) package working in the app.  

PhpStorm IDE was used.

---

## Custom Transaction Test Tool

**A custom javascript utility was created to send custom transactions.**  
This is a nice simple utility for development.  
This tool is currently the only method for sending Register Scooter transaction.

**Steps to run on Windows 10**
1. Download and install Node.js and NPM 
    * https://nodejs.org/en/download/
2. Reboot Computer
3. Verify installation and version in windows command prompt
    * `node –v`
    * `npm -v`
4. Download custom Transactions project
    * https://github.com/e-m-s-y/scooter-transactions
4. Open Windows command prompt or Windows PowerShell and navigate to local /scooter-transactions folder
5. run in command prompt 
    * `npm install`
7. Edit test.js script with wallet credentials for the scooter and rider app
    * /scooter-transactions/src/test.js 

### Easy way to retrieve current nonce of wallet
Edit the following with the desired wallet address.
https://radians.nl/api/v2/wallets/TRXA2NUACckkYwWnS9JRkATQA453ukAcD1

### How to Send test transactions
execute the following commands in command prompt. If the nonce is not valid the transaction will fail and produce error message.

**Send Standard transaction**  
`npm run t -- --nonce 22`

**Send Register Scooter transaction**  
scooter must be registered before using Rental Start/Finish  
`npm run sr -- --nonce 22`

**Send Rental Start transaction**  
`npm run rs -- --nonce 22`

**Send Rental Finish transaction**  
`npm run rf -- --nonce 22`






---

## Off Chain IoT Analytics & Dashboard

### Purpose of IoT Dashboard
The Iot dashboard is an opportunity to connect some well know traditional IoT tools with blockchain technology. The rental transaction process does not depend on this platform. In addition to providing a realtime status of the hardware and the blockchain network it also aided in the debugging and development of the embedded hardware and firmware.

### Features of IoT Dashboard
- Blockchain transaction events via MQTT are used to view and audit all the transactions on the chain and correlate with resulting actions of the IOT device. 
- Scooter publishes via MQTT realtime GPS, Speed, Battery level, and wallet value. Location of scooters are shown on map and data is plotted on graphs.
- Scooter will also publish via MQTT its current operating mode(broken, available, rented, charging, etc).

### Cloud Services
Three cloud services were used for the IOT dashboard demonstration however all of these services could be combined and optimzed to run on a single VPS. It is also possible that these services could be run on the same VPS as an Ark relay node.  
- CloudMQTT
- Node-Red
- Thingsboard 

Thingsboard is the IoT platform that is used to display the web-based Dashboard. This tool offers a nice visual display however the communication interfaces are not as intuitive and flexible as other platforms. For a "real" product you could design IoT protocols to conform directly to Thingsboard's requirements. In the spirit of rapid prototyping I opted to used Node-Red as an intermediate platform to perform some data filtering and packet formating to interconnect all of the data sources and sinks. 

---

### MQTT Broker
A low cost cloud service offering a dedicated MQTT message broker called [CloudMQTT](https://www.cloudmqtt.com/) is used. The current subscription allows for 100 simultaneous connections.  

Alternatively an open source broker such as [Mosquito](https://mosquitto.org/) could be run on a VPS with other services. Mosquito broker could also likely run on the same server as a bridgechain relay node.  

---

### Node-Red
Open source browser-based programming tool for wiring together hardware devices, APIs and online services. It allows for rapid prototyping of services.
This service can be run on a VPS with other services.  IBM offers a free teir with 250MB of storage which was acceptable for the tasks required.

#### Radians Blockchain Event Handler
Thingsboard is not able to handle complex JSON messages with more than 1 level of hierarchy.  Node-Red is used to do some refomatting of the Blockchain messages emitted by the MQTT Core plugin.  
The various events types are split into separate packets and then routed to the corresponding display panel in Thingsboard.

Sceen
![](https://i.imgur.com/jfVFznt.jpg)


#### Realtime Scooter Data Routing
- Node-Red is used to route MQTT messages originating from the Scooter to Thingsboard.  
Currently the messages are just routed without any modifications to the data.  
The data received from the scooter is signed using it's private key. We are currently not verifying this data however we could add this feature using Node-Red.

#### Scooter Device Simulator
- Node-Red is used to create some simple scripts that simulate data for 3 scooters.  This is for demo purposes only so there is data displayed on the Thingsboard dashboard even if a real life scooter device is not power on.  

![](https://i.imgur.com/qNZwGEI.jpg)


---

### Thingsboard
Thingsboard is a great tool for visualizing all of the data from the nodes and providing a very nice admin dashboard. It is an open source platform. Free licence was used. Paid licence is available with additional features and support.  Both free and paid licences required the service to be self hosted. Hosted service does not appear to be available.

**VPS Specifications**  
- Digital Ocean
- 2 CPU
- 4GB RAM
- 80GB SSD
- Ubuntu 18.04.3 (LTS) x64


#### Public Thingsboard Dashboard
http://165.22.237.171:8080/dashboard/f88894b0-d519-11e9-b281-0bd830c6c87f?publicId=f62146f0-cb7c-11e9-b281-0bd830c6c87f  

![](https://i.imgur.com/aGJLUlq.jpg)

<!---  this is the dashboard without annotation
![](https://i.imgur.com/tjSKfO7.jpg)
-->





## IoT Off Chain Communication

The Scooter electronics uses MQTT protocol as the basis for sending all of the off chain data to the analytics dashboard.  The server application will subscribe to the topics to retrieve data and publish to send commands.

### MQTT Overview
MQTT is a lightweight publish/subscribe system that allows devices to publish information about a given topic to a server that functions as a message broker. The broker then pushes the information out to those clients that have previously subscribed to the topic. MQTT is very popular for hobby home automation projects however it is also popular in commercial applications. Facebook Messenger uses MQTT on mobile devices due to its low power consumption and fast transport with easy support for private or group chats.
There is extensive library support for development with many languages.
- MQTT Clients to aid development
    - MQTT Box - good client for PC / chrome extension
    - MQTT Explorer - Awesome tool for exploring all the available topics on Broker
    - Many MQTT Android / iOS apps are available
- library used by MQTT event emitter core plugin: https://www.npmjs.com/package/mqtt

### MQTT Packet Structure
Supports MQTT Protocol V3.1.1

### MQTT Topic Structure
Topics are a string that the broker uses to filter messages for each client. Topic structures are determined entirely by each application and there is no standard structure.  

For the scooter project the topic structure is very simple and consists of three levels. Each level is separated by a forward slash. .

Level1: Top Level Application Name  
Level2: Bridgechain Wallet Address  
Level3: Data Name  

All data is sent in a single topic encoded as a JSON message. The third level topic is just called 'data'.  

The first two topic levels will be referred to as the root level of the device.  
root level = scooters/TRXA2NUACckkYwWnS9JRkATQA453ukAcD1/

**The full topic path is:  scooters/TRXA2NUACckkYwWnS9JRkATQA453ukAcD1/data**  


### MQTT JSON Packet Structure
```
{
   "status":"Available",
   "fix":1,
   "lat":53.53858513,
   "lon":-113.27569070,
   "speed":0.04,
   "sat":11,
   "bal":94968174556,
   "bat":78,
   "sig":"3045022100d8636ab909be41dc3d3512433265bb21586fdcaf54f702d91617d542b7018a3602201ce7ad0be20064eca08b1e51d6c283c6d1fb0855619156b5a092c66a55b44d84"
}

```
* status: Available, Broken, Rented, Charging
* fix: 1 = GPS satelite lock, 0 = no lock
* lat: GPS latitude
* lon: GPS longitude
* speed: km/hour 
* bal: wallet ballance
* sig: packet signature signed with prviate keys

---
## Message Signing using Private Keys
For the proof of concept the MQTT data packets are signed using the the Radians wallet private keys. The packets are currently not being verified by the broker or by the Thingsboard dashboard.

Message signatures were verified using the desktop wallet.  
Example:   

Message: "status":"Available","fix":1,"lat":53.53858513,"lon":-113.27569070,"speed":0.04,"sat":11,"bal":94968174556,"bat":78

Signature: 3045022100d8636ab909be41dc3d3512433265bb21586fdcaf54f702d91617d542b7018a3602201ce7ad0be20064eca08b1e51d6c283c6d1fb0855619156b5a092c66a55b44d84



 ---

## MQTT Topic structures not currently being used in Scooter project
The first 2 topic levels will be referred to as the root level of the device.  

Level1: Top Level Application Name  
Level2: Bridgechain Wallet Address. This is the base topic of the device.  
Level3: Function(status,set, get,) or Device Property(begins with $)  
Additional levels: Item Name  
  
Example Topics: 
scooters/TRXA2NUACckkYwWnS9JRkATQA453ukAcD1/status/gps
scooters/TRXA2NUACckkYwWnS9JRkATQA453ukAcD1/set/lock 
scooters/TRXA2NUACckkYwWnS9JRkATQA453ukAcD1/status/lock 

root level = scooters/TRXA2NUACckkYwWnS9JRkATQA453ukAcD1/


#### Scooter MQTT Topics

##### Device Properties
These are special level3 topics starting with $.
- $state -> device connection state
- $name -> friendly device name
- $fw/version -> Version of firmware
- $fw/checksum -> checksum of firmware

##### Status Topics
Scooter devices will publish to these topics

##### Cmd Topics
Scooter devices will Subscribe to these topics. This is used by the server logic to control actions on the scooter. The device will update the state of the corresponding status topic after command has been executed. The server logic should monitor the status toouc to kniw when command has been completed.


#### MQTT Message Payload Structure
- The message format for status function topics is either a simple value or a JSON encoded object.  
- The message fromat for set function topics is a simple value(boolean, integer, floating point number, or string)

#### Broadcast Channel
This is a special topic that the server can use to broadcast messages to all devices.  
scooters/$broadcast



---




###### tags: `ark.io` `Documentation` `IoT`
