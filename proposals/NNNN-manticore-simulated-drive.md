#Manticore Simulated Drive

* Proposal: [SDL-NNNN](NNNN-manticore-simulated-drive.md)
* Author: [Russ Johnson](https://github.com/russjohnson09)
* Status: **Awaiting review**
* Impacted Platforms: [Manticore UI]

## Introduction

Adding the ability to run simulated drives in Manticore will give app developers a commentate and complete
way to test there apps against real driving situations

## Motivation

Currently Manticore UI provides a build of SDL core, a logging ui for this instance of core, a
generic hmi which provides an example display, and a mock vehicle hmi which is configurable in Manticore UI
to affect things like vehicle speed, PRNDL status, gps location, fuel gauge and other information that
would normally be collected from the vehicle.

Being able to take this last piece of the vehicle hmi and have users be able to press start drive and then
have this data updated for them as you would expect in a real life scenario could greatly improve the
developers experience in creating an sdl enabled app. There are also potential secondary benefits like
a convenient way to demo applications that really on vehicle data.

## Proposed solution

Add the ability to read a data file with as few fields as time, speed, and gps location and as many fields
as are supported by the HMI today.

## Potential downsides

Describe any potential downsides or known objections to the course of action presented in this proposal, then provide counter-arguments to these objections. You should anticipate possible objections that may come up in review and provide an initial response here. Explain why the positives of the proposal outweigh the downsides, or why the downside under discussion is not a large enough issue to prevent the proposal from being accepted.

## Impact on existing code

Describe the impact that this change will have on existing code. Will some SDL integrations stop compiling due to this change? Will applications still compile but produce different behavior than they used to? Is it possible to migrate existing SDL code to use a new feature or API automatically?

## Alternatives considered

Describe alternative approaches to addressing the same problem, and why you chose this approach instead.







#Questions
https://trello.com/c/Wc4rkohY/863-3-manticore-feature-request-simulated-drive-025

basically gps route with vehicle speed, PRNDL status, etc

"it would be cool for us to make an app that collects all of a vehicles' info during a drive and we can create simulations on manticore that trigger vehicle data events." - brett


It sounds to me like this request is to make an android or ios app that can read the gps and other vehicle 
RPCs. After this is should be able to playback this recording and emulate core?

When an actual drive takes place it is core that gives info to any subscribers of the gps, speed, and PRNDL status.

To simulate a drive either core would be told what the current status is from another system or core
would be stubbed out by manticore.


Trigger vehicle data events from manticore.
