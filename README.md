# Protocol buffer definitions for the MeshScale project

Protocol buffers are used to create a standardised data structure that can be serialised to communicate over the wire/radio (network), Bluetooth (client), internally (firmware and app), ...

The messages are defined in .proto and .options files in the proto3 syntax. Source files are generated using the nanoPb generator


## Overview of the message structure

The message PbMessage is the top-level message that encapsulates all others. *One ring to rule them all...*
This one message is sent internally in the firmware, to the client (phone) and over the mesh.

Currently, the pbMessage can contain instructions (set config, execute command, ...) and events (received announce, user input, sensor activation, ...)

The instructions are then split up into: get, set and execute messages (request and response), e.g. "pbMessage - instruction - execReq - do_announce" or "pbMessage - instruction - getResp - interfaceConfig"

The event message is a single oneof with every proto module (=.proto and .options file combined) that have events defined. e.g. AnnounceEvents.


### Proto module numbering

The numbers in the proto module names is meant to show at what "layer" the message is. Numbers 2 and 4 are reserved for future use if needed.
- Layer 0: Only the top level pbMessage
- Layer 1: High level messages that are used in pbMessage (instruction/event)
- Layer 3: Messages that contain at least one of attributes-values/commands/events
- Layer 5: Helper proto modules that are used in Layer 3 modules. They only define data types and no attributes-values/commands/events

