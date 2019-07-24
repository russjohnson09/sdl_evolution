#Manticore Simulated Drive

* Proposal: [SDL-NNNN](NNNN-manticore-simulated-drive.md)
* Author: [Russ Johnson](https://github.com/russjohnson09)
* Status: **Awaiting review**
* Impacted Platforms: [Manticore UI]

## Introduction

Adding the ability to run simulated drives in Manticore will give app developers a convenient and complete
way of testing their apps against real driving situations.

## Motivation

Currently Manticore provides a build of SDL core, a logging ui for this instance of core, a
generic hmi which provides an example display, and a mock vehicle hmi. The vehicle hmi 
can be adjusted in Manticore UI to affect things like vehicle speed, PRNDL status, 
gps location, fuel gauge and other information that
would normally be collected from the vehicle.

Being able to take the vehicle hmi and have users be able to press "start drive" and then
have this data updated for them as you would expect in a real life scenario could greatly improve the
developers experience in creating an sdl enabled app. There are also potential secondary benefits like
a convenient way to demo applications that rely on vehicle data.

## Proposed solution

Add the ability to read a data file with vehicle data and time. This file can be played in real time or sped up.
A few example drives will be included to select without requiring the user to create their own file.


## Data File
A csv file can be loaded as a test drive. The required fields are time and rpc. The ```VehicleInfo.OnVehicleData``` method will
be used to update the vehicle data and all params supported by this method can be included. Bellow is an example csv.

|                          |                                                                                                                                                                      |                           | 
|--------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------| 
| time                     | rpc                                                                                                                                                                  | step                      | 
| 2019-07-24T13:20:14.000Z | {"jsonrpc":"2.0","method":"VehicleInfo.OnVehicleData","params":{"prdnl":"PARK","speed":0,"gps":{"longitudeDegrees":42.5,"latitudeDegrees":-83.3,"altitude":7.7}}}    | Exiting Parking Lot       | 
| 2019-07-24T13:20:15.000Z | {"jsonrpc":"2.0","method":"VehicleInfo.OnVehicleData","params":{"prdnl":"FIRST","speed":2,"gps":{"longitudeDegrees":42.5,"latitudeDegrees":-83.3,"altitude":7.7}}}   | Turning Left On Main St.  | 
| 2019-07-24T13:20:16.000Z | {"jsonrpc":"2.0","method":"VehicleInfo.OnVehicleData","params":{"prdnl":"FIRST","speed":2,"gps":{"longitudeDegrees":42.5,"latitudeDegrees":-83.3,"altitude":7.7}}}   | Heading South On Main St. | 
| 2019-07-24T13:20:17.000Z | {"jsonrpc":"2.0","method":"VehicleInfo.OnVehicleData","params":{"prdnl":"FIRST","speed":2,"gps":{"longitudeDegrees":42.5,"latitudeDegrees":-83.3,"altitude":7.7}}}   |                           | 
| 2019-07-24T13:20:18.000Z | {"jsonrpc":"2.0","method":"VehicleInfo.OnVehicleData","params":{"prdnl":"SECOND","speed":10,"gps":{"longitudeDegrees":42.5,"latitudeDegrees":-83.3,"altitude":7.7}}} | Turning Right on Third    | 

The step column can be used to create named steps in the drive that will be displayed by the UI.

### Simulated Drive UI
The UI will include the vehicle data, a progress bar and a play/pause button.

#### Vehicle Data Display
The most recent gps, speed, and other vehicle info being read from the datafile will be displayed to the user
with fields like speed being displayed on the same line and fields like gps being collapsible.

####Steps
Steps will be included in the display if provided from the data file as a way for users to view the drive's progress
and as a way to start at specific parts of the drive.

## Potential downsides

It adds complexity to an already complicated setup, but this new feature will be contained within its own component and should
not impact existing emulation with Manticore UI.


## Impact on existing code

The code changes will most likely be additions only and will not have a major impact on existing code. It has the potential
to impact the Manticore UI's emulation sidebar especially when it comes to vehicle data.


## Alternatives considered

This could be done as a separate service that connects to Manticore UI, but having it a part of the existing
UI is much simpler. The proposed solution should be simple enough to integrate with the existing Manticore UI
and complete enough to allow for a fully simulated drive.

