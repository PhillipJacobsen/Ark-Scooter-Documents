
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
- Show and track the location of available scooters
- Lock and unlock an IoT physical device (lock) to manage the security of the scooters
- Process payments in ARK (Ѧ) to unlock the device
- Show and track drop-off locations once a scooter has been rented
- Manage and track time and distance of rental (from pick-up to drop-off)
- Process deposit and fees on drop-off at a designated location
- Make the scooter available for rental after proper drop-off is completed


Optional Upgrades:
- Support multiple types of the rental by allowing the owner to take a picture of an object and upload it to the app with a category and price of their choosing
- Allow additional currencies and payment methods
- Allow a web interface for managing rentals


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


---

## Team Members
### Community Members
- @emsy
- @roks0n
- @Chris (ciband)
- @pj

### Ark Crew (Main Contacts and Tech Support)
- @sleepdeficit - IOT
- @Matthew DC - Project Specs
- Oleg - UI

## Milestones





# Technical Specification

## Main Blocks 
Quick List(not in any particular order)
- Bridge Chain Node Management
- Custom Transaction Core Plugin(s)
- Custom Ark Logic Core Plugin
- Logic Platforms(cloud) - example: NodeRed, MQTT
- Analytics Platform(cloud) - example: thingsboard, NodeRed
- Admin App - might be included in Logic/Analytics platform
- Client App(s)(web, Android, IOS)
- IOT Hardware
- IOT Firmware
- IOT device simulator/emulator
- Test

## Optional Blocks
- publish data according to General Bikeshare Feed Specification(GBFS)


## Bridge Chain Requirements
- Core V2.6 Testnet
- Number of forging nodes?


## Logic platform
I am still thinking about how much of the logic should be implemented in the core plugin and how much in a cloud IOT service. Using a common/simple IOT tool such as Node Red for much of the logic would be a good approach for a POC. It is a very accesible tool to a wide range of people. It is a great tool for rapid prototyping. 

## Admin App
Requirements
- view status and configure Devices
- View stats
- 

## Interesting Links 
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


###### tags: `ark.io` `Documentation` `IOT`
