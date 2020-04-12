
Proof of Concept Ark Scooter Rental DApp
===
[Tier 0 Program](https://ark.io/projects/ark-scooters)

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
https://github.com/PhillipJacobsen/Ark-Scooter-Documents

**Scooter Firmware**  
https://github.com/PhillipJacobsen/Ark_Scooter

**iOS/Android DApp Source**  
https://github.com/e-m-s-y/scooter-app

**Radians Bridgechain**  
https://github.com/e-m-s-y/radians

**Custom Transaction Plugin**  
https://github.com/e-m-s-y/scooter-transactions

**Testing Utility for Sending Test Transactions**  
https://github.com/e-m-s-y/scooter-transactions

**Socket Event Forwarder Core Plugin**  
https://github.com/e-m-s-y/socket-event-forwarder

**MQTT Event Forwarder Core Plugin**  
https://github.com/deadlock-delegate/mqtt

**Node-Red Flow Backup**  
https://github.com/PhillipJacobsen/Ark_Scooter/tree/master/NodeRed

**ThingsBoard Dashboard Backup**  
https://github.com/deadlock-delegate/mqtt

**Ark-CPP-crypto v1.0.0**  
(fork of Standard Ark Crypto library with support for Radians Custom Transactions)  
https://github.com/sleepdefic1t/cpp-crypto/tree/chains/radians

**Ark-CPP-client v1.4.0-arduino**  
https://github.com/ArkEcosystem/cpp-client/pull/159

---

## System Block Diagram
![](https://i.imgur.com/TAmaPfE.jpg)


---

## Bridgechain Specifications
Bridge chain was launched prior to the completion of the updated V2.6 Deployer tools

Bridgechain Name: Radians  
Ark core V2.6xx Testnet  
Token: RAD  
Delegates: 53  
Blocktime: 8 seconds  
Explorer: [radians.nl](https://radians.nl/)  
Peer / Seed server: http://37.34.60.90:4040  
Epoch: 2019-10-25T09:05:40.856Z

---

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
scooter->scooter:Display QR code:Public Key,Pseudorandom,Rate
scooter->app: scan QR code
app->app: Select Rental Duration
app->app: Finalize Payment
app->bridgechain:custom tx:(Rental start) to scooter address

Note right of app: Rental Start TX \n To: Scooter Address\n Amount: Rental Amount  \n Fee: Rental \n Asset: hash(Pseudorandom)

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


## Custom Transaction Design

### Transaction Types
TYPE_GROUP: 4000  
SCOOTER_REGISTRATION_TYPE: 401  
RENTAL_START_TYPE: 500  
RENTAL_FINISH_TYPE: 600  


### Rental Start
**From:** App  
**To:** Scooter  
* type = RENTAL_START_TYPE  
* typeGroup = TYPE_GROUP  
* version = 2  
* fee = defaultStaticFee = 10000000  
* amount = number  
* vendorField = optional
* asset = {hash, gps: {[timestamp, lat, long]}, rate}  
    * hash = string(1->64 characters)  
    * timestamp = {epoch: integer}, {human: string}  
    * lat = GPS latitude; String(1->16 characters)  
    * long = GPS longitude; String(1->16 characters)  
    * rate = integer

**Note:**  
Hash, GPS coordinates, and rate are values that are generated by scooter and embedded in the QR code that the app scans.
Hash is a random number.  
Rate is the cost of the ride per minute measured in RAD/minute.  
The amount transferred determines the length of ride.  
Length of Ride(minutes) = Amount / Rate

---



### Rental Finish
**From:** Scooter  
**To:** App  

* type = RENTAL_FINISH_TYPE: 500  
* typeGroup = TYPE_GROUP  
* version = 2  
* fee = defaultStaticFee = 10000000  
* amount = number  
* vendorField = optional
* asset = {gps: {[timestamp, lat, long],[timestamp, lat, long] }, rentalStartTransactionId, rideDuration}  
    * timestamp = {epoch: integer}, {human: string}  
    * lat = GPS latitude; String(1->16 characters)  
    * long = GPS longitude; String(1->16 characters)  
    * rideDuration = RIDE_DURATION_IN_MINUTES


- To: App
- Amount: 0 (or refund amount)
- Fee: Rental
- Asset: 
  - original payment
  - rate (RAD/min)
  - start rental GPS (full precision)
  - start rental timestamp - emsy: we can use the timestamp of the rental start tx.
  - finish rental GPS (full precision)
  - finish rental timestamp
  - Rental Start tx id

The rental dropoff transaction has the full details of the entire ride.
If you wanted to analyze all of the ride data then you only need to look at the rental finish transaction.


---







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


### QR code Specification
The scooter will generate and display a QR code when it is available for rent. The code embedds the following parameters:
- Scooter Wallet Address (34 characters)
- SHA256 Hash of Unique/Random number
- Rental Rate
- GPS Latitude
- GPS longitude

Maximum number of characters required to be encoded is XX.


**NOTE:** GPS coordinates would need to be rounded as the value is not static even if the device is stationary. Rounding to the third decimal place is about 110m of precision. Accuracy of the readings is also a concern as you could get erroneous readings. QR code needs to be static.
Does the app actually require the GPS coordinates to be received at the start of the rental? Perhaps the coordinates could be removed.  

#### Example of String Encoded in QRcode
rad:TRXA2NUACckkYwWnS9JRkATQA453ukAcD1?hash=e4c18e33a25a1b8eec69c61fcc171e3503b21a80cada4d5bc78c037bd239c3b1&rate=61667&lat=53.535500&lon=-113.278236  

![](https://i.imgur.com/iA4B1S3.jpg =225x)

---
### Communication with Bridgechain and Analytics platform
The ESP32 will be assigned a unique Bridgechain address and store its private key in Flash memory. Secure storage methods will be an optional enhanced feature. The ESP32 will be able to send device registration transactions and optionally use its private key to sign / encrypt messages sent offchain. Transactions will use the public Bridgechain API.



---


## Client Mobile Application

### High level details on development environment used


### screenshots





---

## Off Chain IOT Analytics & Dashboard

- Analytics/Debug platform will be used to aid debugging and development of the hardware and the entire system. This tool will allow for realtime monitoring of the embedded hardware/firmware to verify correct operation during mobile testing.  
- The Event log will be used to vaudit all the transactions on the chain and correlate with resulting actions of the IOT device. 
- Operation of the rental platform does not depend on the analytics platform in any way.
- Scooter IOT will publish realtime GPS & battery level to MQTT broker
- Scooter IOT will also publish via MQTT its current operating mode(parked, in use, low battery, broken, etc).
- Thingsboard Dashboard will subscribe via MQTT to GPS, battery, and operating mode and display on realtime map. 
- Thingsboard Dashboard will subscribe via MQTT to bridgechain transaction events and display them in log


### MQTT Broker
A low cost cloud service offering a dedicated MQTT message broker called [CloudMQTT](https://www.cloudmqtt.com/) is used. The current subscription allows for 100 simultaneous connections.  

Alternatively an open source broker such as [Mosquito](https://mosquitto.org/) could be run on a VPS with other services. Mosquito broker could also likely run on the same server as a bridgechain relay node.



---
### Node-Red
- Open source browser-based programming tool for wiring together hardware devices, APIs and online services
- Runs on Raspberry Pi.
- IBM Cloud has free tier with 250MB storage

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
Thingsboard is a great tool for visualizing all of the data from the nodes and providing a very nice admin dashboard. This would Not be used for creating the Mobile user application.
- Device management, data collection, processing and visualization for your IoT solution
- Open Source. 
- Runs on Raspberry Pi
- Runs on Digital Ocean VPS
- Free license likely provides what we need. Paid license also available. Free license would be installed on VPS

#### Public Dashboard
http://165.22.237.171:8080/dashboard/f88894b0-d519-11e9-b281-0bd830c6c87f?publicId=f62146f0-cb7c-11e9-b281-0bd830c6c87f  

![](https://i.imgur.com/aGJLUlq.jpg)

<!---  this is the dashboard without annotation
![](https://i.imgur.com/tjSKfO7.jpg)
-->





## IOT Communication

The Scooter electronics uses MQTT protocol as the basis for sending all of the off chain data to the analytics dashboard.  The server application will subscribe to the topics to retrieve data and publish to send commands.

### MQTT Overview
MQTT is a lightweight publish/subscribe system that allows devices to publish information about a given topic to a server that functions as a message broker. The broker then pushes the information out to those clients that have previously subscribed to the topic. MQTT is very popular for hobby home automation projects however it is also popular in commercial applications. Facebook Messenger uses MQTT on mobile devices due to its low power consumption and fast transport with easy support for private or group chats.
There is extensive library support for development with many languages.
- MQTT Clients to aid development
    - MQTT Box - good client for PC / chrome extension
    - MQTT Explorer - Awesome tool for exploring all the available topics on Broker
    - Many MQTT Android / iOS apps are available
- library used by for MQTT event emitter core plugin: https://www.npmjs.com/package/mqtt

### MQTT Packet Structure
Supports MQTT Protocol V3.1.1
#### MQTT Topic Structure
Topics are a string that the broker uses to filter messages for each client. The topic consists of three or more levels. Each level is separated by a froward slash.  

The first 2 topic levels will be referred to as the root level of the device.  

Level1: Top Level Application Name  
Level2: Bridgechain Public Key. This is the base topic of the device.  
Level3: Function(status,set, get,) or Device Property(begins with $)  
Additional levels: Item Name  
  
Example Topics: 
scooters/03b3019278420fb9351fa716a6c80d400a370d088058cec6e4260246cca83fe862/status/gps
scooters/03b3019278420fb9351fa716a6c80d400a370d088058cec6e4260246cca83fe862/set/lock 
scooters/03b3019278420fb9351fa716a6c80d400a370d088058cec6e4260246cca83fe862/status/lock 

root level = scooters/03b3019278420fb9351fa716a6c80d400a370d088058cec6e4260246cca83fe862/

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







###### tags: `ark.io` `Documentation` `IOT`
