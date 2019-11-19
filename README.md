
Ark Scooters
===
[Tier 0 Program](https://github.com/ArkEcosystem/tier-0-program/issues/12)

## Table of Contents

[TOC]

# Functional Requirements 
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
<!--- Device Registration Transaction (to register a new lock or device)
- Location Registration Transaction (pick-up/drop-off GPS coordinates) -->
- Rental Pick-up / Drop-off Transaction  

<!---Administration functions to handle the registration of scooters and locations will not be implemented in the demo app. The transactions could be demonstrated by some script/tool(Not sure if the Ark Team has some utility for this) -->

### Provided by the ARK.io Team
- The custom mobile app UI design
- Additional guidance and support as necessary

### Requirements for completion
- Provide a mobile application that meets the above minimum criteria.
- Provide a functioning custom ARK Bridgchain blockchain with the above custom transactions and functionality
- Demonstrate the application working as described
- Provide a Bill of Materials (BOM) for the required IoT hardware.
- Project will not include final integration of electronics into scooter hardware. 

<!---### Optional Upgrades:
- Support multiple types of the rental by allowing the owner to take a picture of an object and upload it to the app with a category and price of their choosing
- Allow additional currencies and payment methods
- Allow a web interface for managing rentals
- Loyality Program
- Publish data according to General Bikeshare Feed Specification(GBFS)
- Rider Identification Verification
- Social media integration -->

## System Block Diagram
![](https://i.imgur.com/2Uha6kw.jpg)




---

<!---
### Manually generate private keys for app & scooter
App and Scooter will store hardcoded bridgechain private keys in memory. Every rider app and scooter would need a unique build with its own hardcoded bridgechain wallet.  
There is no automatic IOT device registration feature.

```sequence
Title: Device / App Wallet Init. (hack)

Note left of Desktop Wallet: generate wallets for scooter,app
Note left of scooter: keys hardcoded in flash
Note left of app: keys hardcoded in application
Desktop Wallet->scooter: send tokens
Desktop Wallet->app: send tokens

```
-->


## Message Sequence Diagrams
### Scooter Device Registration Sequence
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


## Details of Custom TXs
### custom tx: Rental Start 
- To: Scooter
- Amount: Rental payment. 
- Fee: Rental
- Asset: 
  - hash(pseudorandom data)
  - start rental GPS (full precision)

**Comments:**
- I don't think we need to expicitly include the rental time as an asset. Scooter can calculate rental duration by the amount received and its own rental rate
- Is there any other info that the app should include as an asset? emsy: I think GPS start coords should be in this transaction intstead of the `Rental Finish` transaction. 

---



### custom tx: Rental Finish
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
If you wanted to analyze all of the ride data then you would only need to look at the rental finish transaction. emsy: sounds good, this eliminates the need to execute multiple API calls. On the other end this does add duplicate data in the blockchain (timestamp rental start, GPS data rental start).


---


## Other details
- Analytics/Debug platform will be used to aid debugging and development of the hardware and the entire system. This tool will allow for realtime monitoring of the embedded hardware/firmware to verify correct operation during mobile testing.  
- The Event log will be used to vaudit all the transactions on the chain and correlate with resulting actions of the IOT device. 
- Operation of the rental platform does not depend on the analytics platform in any way.
- Scooter IOT will publish realtime GPS & battery level to MQTT broker
- Scooter IOT will also publish via MQTT its current operating mode(parked, in use, low battery, broken, etc).
- Thingsboard Dashboard will subscribe via MQTT to GPS, battery, and operating mode and display on realtime map. 
- Thingsboard Dashboard will subscribe via MQTT to bridgechain transaction events and display them in log
![](https://i.imgur.com/8mLIbhs.jpg)

## Team Members
### Community Members
- @emsy
- @pj


### Ark Crew (Main Contacts and Tech Support)
- @sleepdeficit - IOT - Coordinator
- @Matthew DC - Project Specs 
- Oleg - UI

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

## Main Project Tasks

#### Write Technical Specification
- **@pj, @emsy**

#### Bridge Chain Deployment & Node Management
- **@emsy** 

#### Custom Transaction Design
- **@emsy, @pj**

#### Custom Transaction Implementation
- **@emsy**


#### Custom Core Module: App Communication
- NodeJS + Express + SocketCluster 
- **@emsy**

#### IOT Protocol Design
- **@pj**

#### Analytics/Admin Cloud Platform/MQTT broker
- **@pj**

#### IOS/ Andriod Client App
- Appcelerator using JavaScript
- **@emsy with UI guidance from Oleg**

#### IOT device simulator / emulator
- Simulator of additional Scooters on Map. 
- This would be used to aid in development of the logic controller and app. It may just be some simple scripts to produce artificial MQTT data to emulate additional scooters. 
- For demo purposes it could also just be used to show additional devices on the map.
- **@pj**


#### Hardware Electronics
- **@pj**

#### Firmware
- **@pj**



---

# Technical Specification

---
### Technical specification is currently a scratchpad for brainstorming.
---



--- 

## dApp Block Diagram
![](https://i.imgur.com/VohsPuC.jpg)





## Bridgechain Requirements
- Core V2.6 Testnet
- 8 seconds blocktime with 53 forgers.
- We will likely be a bit ahead of the Push Button Deployer Tools and desktop/mobile wallets that support V2.6 core. We likely will need to use some early beta releases of the wallets.
- This will take more work than the standard push button blockchain flow. 
- @emsy has setup a bridgechain without the deployer before and has documented setup process. 

## Data Stored on the Bridgechain
* Device Registration Transaction
    * Custom transaction used to register a new lock or device
    * This will be sent directly by lock/device
* Location Registration Transaction
    * Custom transaction used to register a specific pick-up / drop-off depot location.
* Rental Pickup/Drop-off Transaction.
    * **I think this should be sent by logic controller/server.** - I think that the customer picks-up an available scooter(server sends this custom tx to bridgechain). Customer scoots along and requests a deposit after a while(may the customer decide this location by himself?). Server accepts deposit and instructs customer to make the payment. Customer pays with Ark and server locks the scooter and stores the drop-of transaction on the bridgechain. (emsy)


    

## Custom Transactions
Structure of the custom transactions goes here.


## Logic platform
I am still thinking about how much of the logic should be implemented in the core plugin and how much in a cloud IOT service. Using a common/simple IOT tool such as Node Red for much of the logic would be a good approach for a POC. It is a very accesible tool to a wide range of people. It is a great tool for rapid prototyping. 


## Client Mobile Application

#### Show and track the location of available scooters
1. Mobile App requests location data from server.
2. Server queries bridgechain for location data.
3. Server received data from bridgechain and emits this data through a socket back to the
Mobile App. The server also emits the same data to all other connected clients.
4. Clients update their views according to data.

#### Lock and unlock an IoT physical device (lock) to manage the security of the scooters
1. Mobile App scans QR code on the smart lock.
2. Mobile App reads data from QR and initiate lock or unlock transaction by sending a
request to the server.
3. Server accepts request (in case of unlock the server emits a reservation to all connected
clients) and passes data back to the Mobile App.
4. Mobile App creates intent / URL scheme and opens Ark Mobile app.
5. User sends the custom transaction.
6. Transaction gets forged and bridgechain plugin emits this event to the server.
7. Server emits update to all connected clients.
8. Clients update their views according to data.
9. Server locks / unlocks the smart lock.
10. Optional: in case of a timeout the server will cancel the reservation and update all clients.  

Q: Does the Ark Mobile app support custom transactions?  

(simon): Not currently. When the Tx spec is hammered out, we can get you help with this though.

Q: Is anyone familiar with smart locks? Is there a smart lock on the market with a display which is able to show QR codes?
(simon): Not that I'm aware of. We could probably just use a screen and a relay to cut power for an MVP.


#### Process payments in ARK (Ѧ) to unlock the device
1. Every transaction will be requested via the server.
2. The server sends data to the Mobile App.
3. The Mobile App interprets the data and opens the Ark Mobile App.
4. User sends tokens.
5. Server waits for bridgechain event.
6. Server sends update to client.
7. Client update view according to data.

#### Show and track drop-off locations once a scooter has been rented
1. Server determines drop-off location.
2. Server sends custom transaction to bridgechain with location data.
3. Server waits for bridgechain event.
4. Server sends update to client.
5. Client update view according to data.

Q: Are the drop-off locations fixed? Is the drop-off location the same as the rental start location?  
(simon): I'd say there should probably not be a designated drop-off location. 

Q: Is the smart lock attached to the scooter? Or is the smart lock attached to a stand?
(simon): I think for the MVP, maybe just a relay to cut power as mentioned above should work well enough.

#### Manage and track time and distance of rental (from pick-up to drop-off)
1. Mobile App requests track times.
2. Server determines track time (during rental: timestamp now - timestamp pick-up or total
rental time: timestamp drop-off - timestamp pick-up).
3. Server sends update to client.
4. Client update view according to data.  

Q: Distance tracking requires GPS data of the user which means the app needs to be open all time which is not a good combination riding a scooter. What if the user closes the app in the meantime? This might need some refinement.
(simon): We could probably just use a simple time-based calculation. X ARK == X minutes

#### Process deposit and fees on drop-off at a designated location.
1. Scan QR of lock and initiate drop-off transaction.
2. Server instructs Mobile App to send custom transaction to the bridgechain.
3. Intent / URL scheme opens Ark Mobile App and fills the form with data.
4. User sends the transaction.
5. Server waits for bridgechain event.
6. Server sends update to client.
7. Client update view according to data.
8. Smart lock will start rental process, see below.

#### Make the scooter available for rental after proper drop-off is completed
1. Smart lock sends location to server and requests availability for rental.
2. Server sends custom pick-up transaction to bridgechain with location data.
3. Server waits for bridgechain event.
4. Server sends update to all connected clients (scooter is now available for rental).
5. Clients update their views according to the data.





## Admin App (optional upgrade)
I think this could all be done with IOT platform tools.
Requirements
- View device status
- Configure Devices
- View usage stats
- Create/View various reports
- Generate Alerts

## IOT Platforms for Analytics, Device Monitoring, and some data processing

### Node-Red
- Open source browser-based programming tool for wiring together hardware devices, APIs and online services
- Runs on Raspberry Pi.
- IBM Cloud has free tier with 250MB storage

### Thingsboard
Thingsboard would be a great tool for visualizing all of the data from the nodes and providing a very nice admin dashboard. This would Not be used for creating the Mobile user application.
- Device management, data collection, processing and visualization for your IoT solution
- Open Source. 
- Runs on Raspberry Pi
- Runs on Digital Ocean VPS
- Free license likely provides what we need. Paid license also available. Free license would be installed on VPS

#### Admin Analytics Dashboard ####
![](https://i.imgur.com/8mLIbhs.jpg)




## IOT Communication

The Scooter electronics will use MQTT protocol for all bidirectional communication with the cloud server.  The server application will subscribe to the topics to retrieve data and publish to send commands.

### MQTT Overview
MQTT is a lightweight publish/subscribe system that allows devices to publish information about a given topic to a server that functions as a message broker. The broker then pushes the information out to those clients that have previously subscribed to the topic. MQTT is very popular for hobby home automation projects however it is also popular in commercial applications. Facebook Messenger uses MQTT on mobile devices due to its low power consumption and fast transport with easy support for private or group chats.
- Mosquito MQTT Broker is open source and requires a low end VPS or Raspberry Pi
- Low cost cloud service is also available to minimize setup time [CloudMQTT](https://www.cloudmqtt.com/)
- Extensive library support for any language you would like to develop with.
- MQTT Clients to aid development
    - MQTT Box - good client for PC / chrome extension
    - MQTT Explorer - Awesome tool for exploring all the available topics on Broker
    - Many MQTT Android / iOS apps are available
- library used by @roks0n: https://www.npmjs.com/package/mqtt

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

## IOT Hardware / Firmware

### QR code Specification
The scooter will generate and display a QR code when it is available for rent. The code embedds the following parameters:
- Scooter Address (34 characters)
- pseudorandom Hash (xx characters)
- Rental Rate (maxiumum 6 characters)

Maxiumum number of characters required to be encoded is XX.


**NOTE:** GPS coordinates would need to be rounded as the value is not static even if the device is stationary. Rounding to the third decimal place is about 110m of precision. Accuracy of the readings is also a concern as you could get erroneous readings. QR code needs to be static.
Does the app actually require the GPS coordinates to be received at the start of the rental? Perhaps the coordinates could be removed.  
The pseudorandom hash could be derived from full precision GPS coordinates + locally generated random value.

#### Example
rad:TRXA2NUACckkYwWnS9JRkATQA453ukAcD1?hash=4897212321343433&rate=370000000




---

### Scooter
- xiaomi m365 is a common scooter that rideshare companies rebranded for their
- launch in the last couple of years. The large rideshare companies are now starting to create modified electronics and upgraded scooters.
- There seems to be an easily accessible serial interface available for reading out data from the m365 scooter.

### Custom Electronics
The ESP32 processor is a 32bit highly integrated SoC with Wifi. Firmware will be developed using Arduino / PlatformIO environment and Ark C++ SDK.  
A GPS module with active external antenna will be used.  
The lock/unlock security mechanism will be a relay enabling the power to the stock scooter controller.  
Initially a cellphone wifi hotspot will provide the internet connection to the ESP32. A GSM module can be integrated as an optional feature.
A small 2.4" or 3.5" TFT could provided if it provides functionality to the user interface. It could be used to dynamically generate a QR code instead of a static printed code.  
The custom electronics may not be able to be integrated inside of the scooter due to space constraints. In this case a small enclosure will be used that can be attached to the base or handle of the scooter.

 ![](https://i.imgur.com/BSaLcJf.jpg)



### Communication with Bridgechain and Cloud Server
The ESP32 will be assigned a unique Bridgechain address and store its private key in Flash memory. Secure storage methods will be an optional enhanced feature. The ESP32 will be able to send device registration transactions and optionally use its private key to sign / encrypt messages sent offchain. Transactions will use the public Bridgechain API.

The ESP32 will not communicate with the Ark Mainnet.

MQTT protocol will be used for bidirectional communication with the cloud server. ESP32 will periodically publish sensor data(Location, Battery level).  ESP32 will subscribe to command topics and publish command acknowledgments.

### Additional Firmware Details
The firmware/hardware will not be optimized for low power extended battery operation.


# Interesting Links 

#### Ark
- [Tier 0 project details](https://github.com/ArkEcosystem/tier-0-program/issues/12)
- [Transaction Fixtures](https://github.com/sleepdefic1t/ledger/tree/feat/implement-v2/docs/fixtures)

#### Bike Share Data
- [General Bikeshare Feed Specification](https://github.com/NABSA/gbfs/blob/master/gbfs.md)
- [how cities can ask for data from micromobility providers](https://blog.remix.com/mds-gbfs-and-how-cities-can-ask-for-data-from-micromobility-providers-7957ca639f16)
- [How long do scooters last](https://qz.com/1561654/how-long-does-a-scooter-last-less-than-a-month-louisville-data-suggests/amp/)
- [better manage sharing bikes by tapping into blockchain](https://dailyfintech.com/2018/05/19/can-ofo-better-manages-their-sharing-bikes-by-tapping-into-blockchain/)

#### Bike Share Apps
- [Bitlock Bike Lock + Bike Share Platform](https://bitlock.co/bikeshare.html)
- [Joyride Bike/Scooter Share Platform](https://www.joyride.city/plans.html)
- [How to build a Scooter Sharing App](https://www.mobindustry.net/building-a-scooter-sharing-app-like-lime-nextbike-and-mobike/)

#### Scooter Hardware Reverse Engineering
- [decoding serial bus data on a Xiaomi M365 Scooter](https://gitlab.com/esp32m365/esp32_xiaomi_m365_display)
- [BLE controller replacement](https://github.com/camcamfresh/Xiaomi-M365-BLE-Controller-Replacement)

#### Custom transaction / application development
- [Introduction to development part 1](https://blog.ark.io/an-introduction-to-blockchain-application-development-part-1-7bb2082e5e44)
- [Introduction to development part 2](https://blog.ark.io/an-introduction-to-blockchain-application-development-part-2-2-909b4984bae)
- [Cryptocurrency Checkout](https://cryptocurrencycheckout.com/guides/individual_item)

[IOT Data Simulator](https://github.com/IBA-Group-IT/IoT-data-simulator)

###### tags: `ark.io` `Documentation` `IOT`
