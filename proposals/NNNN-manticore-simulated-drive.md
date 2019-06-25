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

Add the ability to read a data file with a few required fields (time, speed, and gps location) and optional fields
like fuel gauge, acceleration pedal and others are supported by the HMI. This file can be played in real time or sped up. For
example drives provided there should also be a dashcam video provided. The video and other information on
the simulated drive will be placed on the right sidebar as a new tab selection.

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
