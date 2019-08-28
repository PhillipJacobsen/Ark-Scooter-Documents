
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


## Team Members
### Community Members
- @emsy
- @roks0n
- @Chris (ciband)
- @pj

### Ark Crew (Main Contact and Tech Support)
- @sleepdeficit -IOT
- @Matthew DC - Project Specs
- Oleg - UI



# Technical Specification




###### tags: `ark.io` `Documentation` `IOT`
