
Ark Scooters
===
[Tier 0 Program](https://github.com/ArkEcosystem/tier-0-program/issues/12)


## Table of Contents

[TOC]

# Functional Requirements 
Create a Scooter rental solution utilizing a mobile app and an associated Ark custom bridgechain to manage locking, unlocking, deposits, locations, and management of ARK Scooter rentals.

## Components

### Mobile App
The core user interface of the project will be a mobile app for both iOS and Android. This mobile app will manage the following:
- Customer Onboarding
- Booking
- Real-time GPS tracking of available scooters using Google Maps
- QR code / ID scanner integration
- Lock and unlock an IoT physical device (lock) to manage the security of the scooters
- In-app payments in ARK (Ѧ)
- Show and track drop-off locations once a scooter has been rented
- Manage and track time and distance of rental (from pick-up to drop-off)
- Process deposit and fees on drop-off at a designated location
- Make the scooter available for rental after proper drop-off is completed

Optional Upgrades:
- Support multiple types of the rental by allowing the owner to take a picture of an object and upload it to the app with a category and price of their choosing
- Allow additional currencies and payment methods
- Allow a web interface for managing rentals
- Loyality Program
- Publish data according to General Bikeshare Feed Specification(GBFS)
- Rider Identification Verification
- Social media integration

### Custom ARK Bridgechain
All information related to the rental will be stored on the blockchain. This will be accomplished through several potentially new custom transaction types as follows:
- Device Registration Transaction (to register a new lock or device)
- Location Registration Transaction (pick-up/drop-off GPS coordinates)
- Rental Pick-up Transaction
- Rental Drop-off Transaction

### Provided by the ARK.io Team:
- The custom mobile app UI design
- Additional guidance and support as necessary

### Requirements for completion:
- Provide a completed mobile application that meets the above minimum criteria.
- Provide a functioning ARK based blockchain with the above custom transactions and functionality
- Demonstrate the application working as described
- Provide a Bill of Materials (BOM) for the required IoT hardware.


## Team Members
### Community Members
- @emsy
- @roks0n
- @Chris (ciband)
- @pj

### Ark Crew (Main Contacts and Tech Support)
- @sleepdeficit - IOT - Coordinator
- @Matthew DC - Project Specs 
- Oleg - UI

## Milestones
Implementation of custom transactions and deployment of bridgechain will occur near the latter stages of design.

#### Highlevel Timeline


---


# Technical Specification
- **@pj, @emsy**



## Main Blocks / Tasks

#### Bridge Chain Deployment & Node Management
- **@emsy**

#### Custom Transaction Design
- **@emsy, @pj**

#### Custom Transaction Implementation
- **@emsy, @roks0n ??**

#### Custom Core Module: MQTT plugin
- used for data analytics only. Likely needs minor tweaks
- **@roks0n**


#### Custom Core Module: Device and Location Registries
- **@emsy, @roks0n ??**

#### Custom Core Module: Logic Controller
- Note: I am not yet clear on location of all the logic (Core plugin, cloud server)
- **@emsy**

#### Cloud Server: Data Processing / Logic Controller
- Note: I am not yet clear on location of all the logic (Core plugin, cloud server)
- some data pre-processing / modules may be implemented via Node-Red
- NodeJS + Express + SocketCluster
- **@emsy, @pj**

#### MQTT Broker Management
- **@pj**

#### MQTT Protocol Design
- **@pj**

#### Analytics/Admin Cloud Platform (Thingsboard??)
- **@pj**

#### IOS/ Andriod Client App
- Appcelerator using JavaScript
- **@emsy with UI guidance from Oleg**

#### IOT device simulator / emulator
- Simulator of additional Scooters on Map. 
- **@pj, @roks0n**


#### Hardware Electronics
- **@pj**

#### Firmware
- **@pj, @Chris (ciband)**
- definitely will get @Chris (ciband)'s help with C++ SDK library enhancements if needed

#### Hardware Integration into Scooter
- **@pj**


#### System Test
-



## System Block Diagram
![](https://i.imgur.com/AHIrylh.jpg)

--- 

## dApp Block Diagram
![](https://i.imgur.com/VohsPuC.jpg)






## Bridgechain Requirements
- Core V2.6 Testnet
- 8 seconds blocktime with 53 forgers.
- Not sure if deployer will be updated to support V2.6 when we are ready for it so this might take a bit more work than the standard push button blockchain flow - I'm also not sure but I did setup a bridgechain without the deployer before and I documented it which might be helpfull (emsy)

## Data Stored on the Bridgechain
* Device Registration Transaction
    * Custom transaction used to register a new lock or device
    * This will be sent directly by lock/device
* Location Registration Transaction
    * Custom transaction used to register a specific pick-up / drop-off depot location.
    * **Not sure exactly how this would be triggered** - Who may determine these locations? The customer or us? Do we add / manage these locations via our Admin app? (emsy)
* Rental Pickup/Drop-off Transaction.
    * **I think this should be sent by logic controller/server.** - I think that the customer picks-up an available scooter(server sends this custom tx to bridgechain). Customer scoots along and requests a deposit after a while(may the customer decide this location by himself?). Server accepts deposit and instructs customer to make the payment. Customer pays with Ark and server locks the scooter and stores the drop-of transaction on the bridgechain. (emsy)

**I don't think that user App needs to know anything about the bridgechain. I think it just needs to proces payments by ARK** - I agree (emsy)

    

## Custom Transactions
Structure of the custom transactions goes here.

I added some links ad the bottom which might help on this topic (emsy)

## Logic platform
I am still thinking about how much of the logic should be implemented in the core plugin and how much in a cloud IOT service. Using a common/simple IOT tool such as Node Red for much of the logic would be a good approach for a POC. It is a very accesible tool to a wide range of people. It is a great tool for rapid prototyping. 


## Client Mobile Application

### Show and track the location of available scooters
1. Mobile App requests location data from server.
2. Server queries bridgechain for location data.
3. Server received data from bridgechain and emits this data through a socket back to the
Mobile App. The server also emits the same data to all other connected clients.
4. Clients update their views according to data.

### Lock and unlock an IoT physical device (lock) to manage the security of the scooters
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
Q: Is anyone familiar with smart locks? Is there a smart lock on the market with a display which is able to show QR codes?


### Process payments in ARK (Ѧ) to unlock the device
1. Every transaction will be requested via the server.
2. The server sends data to the Mobile App.
3. The Mobile App interprets the data and opens the Ark Mobile App.
4. User sends tokens.
5. Server waits for bridgechain event.
6. Server sends update to client.
7. Client update view according to data.

### Show and track drop-off locations once a scooter has been rented
1. Server determines drop-off location.
2. Server sends custom transaction to bridgechain with location data.
3. Server waits for bridgechain event.
4. Server sends update to client.
5. Client update view according to data.

Q: Are the drop-off locations fixed? Is the drop-off location the same as the rental start location?  
Q: Is the smart lock attached to the scooter? Or is the smart lock attached to a stand?

### Manage and track time and distance of rental (from pick-up to drop-off)
1. Mobile App requests track times.
2. Server determines track time (during rental: timestamp now - timestamp pick-up or total
rental time: timestamp drop-off - timestamp pick-up).
3. Server sends update to client.
4. Client update view according to data.  

Q: Distance tracking requires GPS data of the user which means the app needs to be open all time which is not a good combination riding a scooter. What if the user closes the app in the meantime? This might need some refinement.

### Process deposit and fees on drop-off at a designated location.
1. Scan QR of lock and initiate drop-off transaction.
2. Server instructs Mobile App to send custom transaction to the bridgechain.
3. Intent / URL scheme opens Ark Mobile App and fills the form with data.
4. User sends the transaction.
5. Server waits for bridgechain event.
6. Server sends update to client.
7. Client update view according to data.
8. Smart lock will start rental process, see below.

### Make the scooter available for rental after proper drop-off is completed
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

I believe that we could relatively easily generate a very similar dashboard as the demo below by simply subscribing to data published to the MQTT broker and using the standard Thingsboard Widgets.
![](https://i.imgur.com/W4Z3hKb.jpg)



## IOT Communication

The Scooter electronics will use MQTT protocol for all bidirectional communication with the cloud server. Data will be sent with JSON formatting. The server application will subscribe to the topics to retrieve data and publish to send commands.

### MQTT
MQTT is a lightweight publish/subscribe system that allows devices to publish information about a given topic to a server that functions as a message broker. The broker then pushes the information out to those clients that have previously subscribed to the topic. MQTT is very popular for hobby home automation projects however it is also popular in commercial applications. Facebook Messenger uses MQTT on mobile devices due to its low power consumption and fast transport with easy support for private or group chats.
- Mosquito MQTT Broker is open source and requires a low end VPS or Raspberry Pi
- Low cost cloud service is also available to minimize setup time [CloudMQTT](https://www.cloudmqtt.com/)
- Extensive library support for any language you would like to develop with.
- MQTT Clients to aid development
    - MQTT Box - good client for PC / chrome extension
    - MQTT Explorer - Awesome tool for exploring all the available topics on Broker
    - Many MQTT Android / iOS apps are available



## IOT Hardware / Firmware

### Scooter
- xiaomi m365 is a common scooter that rideshare companies rebranded for their launch in the last couple of years. The large rideshare companies are now starting to create modified electronics and upgraded scooters.
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

### Addtional Firmware Details
The firmware/hardware will not be optimized for low power extended battery operation.


# Interesting Links 

#### Ark
- [Tier 0 project details](https://github.com/ArkEcosystem/tier-0-program/issues/12)

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

[IOT Data Simulator](https://github.com/IBA-Group-IT/IoT-data-simulator)

###### tags: `ark.io` `Documentation` `IOT`
