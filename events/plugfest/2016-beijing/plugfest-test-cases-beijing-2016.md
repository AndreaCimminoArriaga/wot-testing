# WoT PlugFest Test Cases

Version Beijing 2016

## Setup

During the PlugFest, at least one *consuming Thing* (client) must be connected to one *exposing Thing* (server). This can be extended to a more complicated setup involving multiple clients, servers, and servients. All interacting Things must pairwise share at least one Protocol Binding. Furthermore, we expect one Thing Description Repository to be available for all connected Things.

## Discovery

| Identifier          | TC_WOT_DISC_01 |
|:--------------------|:---------------|
| Objective           | Discover Thing Manually
| References          | [3.2.6.2.1 Manual Discovery](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#manual-discovery)
| Pre-test conditions | Exposing Thing has Thing Description
| **Test sequence**   | 
| 1. Stimulus         | Operator configures TD of exposing Thing in Consuming Thing
| 2. Verify           | Consuming Thing displays or interacts with exposing Thing

| Identifier          | TC_WOT_DISC_02 |
|:--------------------|:---------------|
| Objective           | Register Thing with Repository
| References          | [3.2.6.2.2 Repository](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#repository)
| Pre-test conditions | Exposing Thing has Thing Description, TD Repository is reachable
| **Test sequence**   | 
| 1. Stimulus         | Exposing Thing or commissioning tool sends `Create` with the TD to Repository registration resource
| 2. Check            | Exposing Thing or commissioning tool sends <br/> - protocol operation bound to `Create` <br/> - valid TD in payload <br/> - to registration URI
| 3. Check            | Repository resonds with <br/> - positive response code <br/> - Location of the registration handle
| 4. Verify           | TD Repository look-up returns Exposing Thing

| Identifier          | TC_WOT_DISC_03 |
|:--------------------|:---------------|
| Objective           | Update TD in Repository
| References          | [3.2.6.2.2 Repository](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#repository)
| Pre-test conditions | Exposing Thing has changed Thing Description, TD Repository is reachable, exposing Thing is registered
| **Test sequence**   | 
| 1. Stimulus         | Exposing Thing or commissioning tool sends `Update` with the new TD to registration handle
| 2. Check            | Exposing Thing or commissioning tool sends <br/> - protocol operation bound to `Update` <br/> - valid TD in payload <br/> - to registration URI
| 3. Check            | Repository resonds with <br/> - positive response code <br/> - Location of the registration handle
| 4. Verify           | TD Repository look-up returns exposing Thing

| Identifier          | TC_WOT_DISC_04 |
|:--------------------|:---------------|
| Objective           | Discover Thing from Repository
| References          | [3.2.6.2.2 Repository](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#repository)
| Pre-test conditions | TD Repository is reachable, exposing Thing is registered, consuming Thing implements TD Repo look-up
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends look-up to Repository look-up resource
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Retrieve` <br/> - **experimental/optional** parameterized with filter for exposing Thing <br/> - to look-up URI
| 3. Check            | Repository resonds with <br/> - positive response code <br/> - Thing catalogue in payload <br/> - containing TD of exposing Thing
| 4. Verify           | Consuming Thing displays or interacts with exposing Thing

| Identifier          | TC_WOT_DISC_05 |
|:--------------------|:---------------|
| Objective           | Delete Thing from Repository
| References          | [3.2.6.2.2 Repository](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#repository)
| Pre-test conditions | TD Repository is reachable, exposing Thing is registered
| **Test sequence**   | 
| 1. Stimulus         | Exposing Thing sends `Delete` to handle resource
| 2. Check            | Exposing Thing sends <br/> - protocol operation bound to `Delete` <br/> - no payload <br/> - to handle URI
| 3. Check            | Repository resonds with <br/> - positive response code <br/> - no payload
| 4. Verify           | TD Repository look-up does not return exposing Thing


| Identifier          | TC_WOT_DISC_06 |
|:--------------------|:---------------|
| Objective           | Discover Thing Locally
| References          | [3.2.6.2.3 Local Discovery](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#local-discovery)
| Pre-test conditions | Exposing Thing has Thing Description, Both exposing and consuming Thing provide local discovery mechanism (e.g., mDNS or BLE Beacons)
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing initiates local look-up
| 2. Check            | Exposing Thing sends out TD
| 3. Verify           | Consuming Thing displays or interacts with exposing Thing

## Base

### Properties

| Identifier          | TC_WOT_BASE_01 |
|:--------------------|:---------------|
| Objective           | Read Boolean Property
| References          | [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data)
| Pre-test conditions | Exposing Thing provides boolean Property
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Retrieve` to Property
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Retrieve` <br/> - no payload <br/> - to Property URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - payload formatted according to TD
| 4. Verify           | Consuming Thing displays read value

| Identifier          | TC_WOT_BASE_02 |
|:--------------------|:---------------|
| Objective           | Write Boolean Property
| References          | [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data)
| Pre-test conditions | Exposing Thing provides boolean Property
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Update` to Property
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Update` <br/> - payload formatted according to TD <br/> - to Property URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - no payload
| 4. Verify           | `Retrieve` on Property returns new value

| Identifier          | TC_WOT_BASE_03 |
|:--------------------|:---------------|
| Objective           | Read Integer Property
| References          | [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data)
| Pre-test conditions | Exposing Thing provides integer Property
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Retrieve` to Property
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Retrieve` <br/> - no payload <br/> - to Property URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - payload formatted according to TD
| 4. Verify           | Consuming Thing displays read value

| Identifier          | TC_WOT_BASE_04 |
|:--------------------|:---------------|
| Objective           | Write Integer Property
| References          | [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data)
| Pre-test conditions | Exposing Thing provides integer Property
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Update` to Property
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Update` <br/> - payload formatted according to TD <br/> - to Property URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - no payload
| 4. Verify           | `Retrieve` on Property returns new value

| Identifier          | TC_WOT_BASE_05 |
|:--------------------|:---------------|
| Objective           | Read Number Property
| References          | [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data)
| Pre-test conditions | Exposing Thing provides number Property
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Retrieve` to Property
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Retrieve` <br/> - no payload <br/> - to Property URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - payload formatted according to TD
| 4. Verify           | Consuming Thing displays read value

| Identifier          | TC_WOT_BASE_06 |
|:--------------------|:---------------|
| Objective           | Write Number Property
| References          | [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data)
| Pre-test conditions | Exposing Thing provides number Property
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Update` to Property
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Update` <br/> - payload formatted according to TD <br/> - to Property URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - no payload
| 4. Verify           | `Retrieve` on Property returns new value

| Identifier          | TC_WOT_BASE_07 |
|:--------------------|:---------------|
| Objective           | Read String Property
| References          | [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data)
| Pre-test conditions | Exposing Thing provides string Property
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Retrieve` to Property
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Retrieve` <br/> - no payload <br/> - to Property URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - payload formatted according to TD
| 4. Verify           | Consuming Thing displays read value

| Identifier          | TC_WOT_BASE_08 |
|:--------------------|:---------------|
| Objective           | Write String Property
| References          | [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data)
| Pre-test conditions | Exposing Thing provides string Property
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Update` to Property
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Update` <br/> - payload formatted according to TD <br/> - to Property URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - no payload
| 4. Verify           | `Retrieve` on Property returns new value

| Identifier          | TC_WOT_BASE_09 |
|:--------------------|:---------------|
| Objective           | Read Structured Property
| References          | [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.2 Structured Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#structured-data)
| Pre-test conditions | Exposing Thing provides structured Property
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Retrieve` to Property
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Retrieve` <br/> - no payload <br/> - to Property URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - payload formatted according to TD
| 4. Verify           | Consuming Thing displays read value

| Identifier          | TC_WOT_BASE_10 |
|:--------------------|:---------------|
| Objective           | Write Structured Property
| References          | [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.2 Structured Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#structured-data)
| Pre-test conditions | Exposing Thing provides structured Property
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Update` to Property
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Update` <br/> - payload formatted according to TD <br/> - to Property URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - no payload
| 4. Verify           | `Retrieve` on Property returns new structured value

### Actions

| Identifier          | TC_WOT_BASE_21 |
|:--------------------|:---------------|
| Objective           | Invoke Simple Action
| References          | [3.2.3.2 Action](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#action)
| Pre-test conditions | Exposing Thing provides Action without parameters
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Create` to Action
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Create` <br/> - no payload <br/> - to Action URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - Location of Action handle
| 4. Verify           | Exposing Thing created new (sub-)resource and performs (or queued) Action

| Identifier          | TC_WOT_BASE_22 |
|:--------------------|:---------------|
| Objective           | Monitor Simple Action
| References          | [3.2.3.2 Action](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#action)
| Pre-test conditions | Consuming Thing has Handle from previously invoked Action
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Retrieve` to handle resource
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Retrieve` <br/> - no payload <br/> - to Action handle URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - non-empty payload
| 4. Verify           | Consuming Thing displays Action status

| Identifier          | TC_WOT_BASE_23 |
|:--------------------|:---------------|
| Objective           | Cancel Simple Action
| References          | [3.2.3.2 Action](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#action)
| Pre-test conditions | Consuming Thing has Handle from previously invoked Action
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Delete` to handle resource
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Delete` <br/> - no payload <br/> - to Action handle URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - no payload
| 4. Verify           | Exposing Thing stops action and removes handle resource

| Identifier          | TC_WOT_BASE_24 |
|:--------------------|:---------------|
| Objective           | Invoke Parameterized Action
| References          | [3.2.3.2 Action](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#action), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data), [3.2.4.2 Structured Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#structured-data)
| Pre-test conditions | Exposing Thing provides Action with parameters
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Create` to Action
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Create` <br/> - payload formatted according to TD <br/> - to Action URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - Location of Action handle
| 4. Verify           | Exposing Thing created new (sub-)resource and performs (or queued) Action

| Identifier          | TC_WOT_BASE_25 |
|:--------------------|:---------------|
| Objective           | Monitor Parameterized Action
| References          | [3.2.3.2 Action](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#action), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data), [3.2.4.2 Structured Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#structured-data)
| Pre-test conditions | Consuming Thing has Handle from previously invoked parameterized Action
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Retrieve` to handle resource
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Retrieve` <br/> - no payload <br/> - to Action handle URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - non-empty payload containing parameters from invocation
| 4. Verify           | Consuming Thing displays Action status

| Identifier          | TC_WOT_BASE_26 |
|:--------------------|:---------------|
| Objective           | Modify Parameterized Action
| References          | [3.2.3.2 Action](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#action), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data), [3.2.4.2 Structured Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#structured-data)
| Pre-test conditions | Consuming Thing has Handle from previously invoked parameterized Action
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Update` to handle resource
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Update` <br/> - payload formatted according to TD <br/> - to Action handle URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - no payload
| 4. Verify           | `Retrieve` on handle shows new parameters

| Identifier          | TC_WOT_BASE_27 |
|:--------------------|:---------------|
| Objective           | Cancel Parameterized Action
| References          | [3.2.3.2 Action](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#action)
| Pre-test conditions | Consuming Thing has Handle from previously invoked parameterized Action
| **Test sequence**   | 
| 1. Stimulus         | Consuming Thing sends `Delete` to handle resource
| 2. Check            | Consuming Thing sends <br/> - protocol operation bound to `Delete` <br/> - no payload <br/> - to Action handle URI
| 3. Check            | Exposing Thing sends <br/> - positive response code <br/> - no payload
| 4. Verify           | Exposing Thing stops action and removes handle resource

### Events

| Identifier          | TC_WOT_BASE_41 |
|:--------------------|:---------------|
| Objective           | Subscribe to Simple Event
| References          | [3.2.3.3 Event](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#event)
| Pre-test conditions | Exposing Thing provides Event without condition settings
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_BASE_42 |
|:--------------------|:---------------|
| Objective           | Unsubscribe from Simple Event
| References          | [3.2.3.3 Event](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#event)
| Pre-test conditions | Consuming Thing has subscription handle
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_BASE_43 |
|:--------------------|:---------------|
| Objective           | Subscribe to Conditional Event
| References          | [3.2.3.3 Event](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#event), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data), [3.2.4.2 Structured Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#structured-data)
| Pre-test conditions | Exposing Thing provides Event with condition settings
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_BASE_44 |
|:--------------------|:---------------|
| Objective           | Modify Event Conditions
| References          | [3.2.3.3 Event](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#event), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data), [3.2.4.2 Structured Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#structured-data)
| Pre-test conditions | Consuming Thing has subscription handle of conditional Event
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_BASE_45 |
|:--------------------|:---------------|
| Objective           | Unsubscribe from Conditional Event
| References          | [3.2.3.3 Event](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#event)
| Pre-test conditions | Consuming Thing has subscription handle of conditional Event
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

## Scripting API

| Identifier          | TC_WOT_SAPI_01 |
|:--------------------|:---------------|
| Objective           | Install a Script
| References          |
| Pre-test conditions | 
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_02 |
|:--------------------|:---------------|
| Objective           | Start a Script
| References          |
| Pre-test conditions | 
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_03 |
|:--------------------|:---------------|
| Objective           | Discover a Thing
| References          | [3.3.2.1.1 Factory discover()](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#discover)
| Pre-test conditions | 
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_04 |
|:--------------------|:---------------|
| Objective           | Consume a TD Object
| References          | [3.3.2.1.2 Factory consumeDescription()](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#consumeDescription), [3.2 Thing Description](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#thing-description)
| Pre-test conditions | TD of consumed Thing was parsed into object
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_05 |
|:--------------------|:---------------|
| Objective           | Consume a TD URI
| References          | [3.3.2.2.3 Factory createFromDescriptionUri()](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#createFromDescriptionUri), [3.2 Thing Description](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#thing-description)
| Pre-test conditions | TD of consumed Thing is available over a protocol supported by consuming Thing
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_06 |
|:--------------------|:---------------|
| Objective           | Display Thing Name
| References          | [3.3.3 Consumed Thing](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#consumed-thing), [3.2.2.2 Thing Metadata](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#thing-metadata)
| Pre-test conditions | Script has instance of consumed Thing
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_07 |
|:--------------------|:---------------|
| Objective           | Get Property
| References          | [3.3.3 Consumed Thing](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#consumed-thing), [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data), [3.2.4.2 Structured Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#structured-data)
| Pre-test conditions | Script has instance of consumed Thing
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_08 |
|:--------------------|:---------------|
| Objective           | Set Property
| References          | [3.3.3 Consumed Thing](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#consumed-thing), [3.2.3.1 Property](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#property), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data), [3.2.4.2 Structured Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#structured-data)
| Pre-test conditions | Script has instance of consumed Thing
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_09 |
|:--------------------|:---------------|
| Objective           | Invoke Simple Action
| References          | [3.3.3 Consumed Thing](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#consumed-thing), [3.2.3.2 Action](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#action)
| Pre-test conditions | Script has instance of consumed Thing
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_10 |
|:--------------------|:---------------|
| Objective           | Invoke Parameterized Action
| References          | [3.3.3 Consumed Thing](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#consumed-thing), [3.2.3.2 Action](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#action), [3.2.4.1 Simple Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#simple-data), [3.2.4.2 Structured Data](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#structured-data)
| Pre-test conditions | Script has instance of consumed Thing
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_05 |
|:--------------------|:---------------|
| Objective           | Cancel Action
| References          | [3.3.3 Consumed Thing](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#consumed-thing), [3.2.3.2 Action](https://w3c.github.io/wot/current-practices/wot-practices-beijing-2016.html#action)
| Pre-test conditions | Script has Promise of invoked Action
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_03 |
|:--------------------|:---------------|
| Objective           | Stop a Script
| References          |
| Pre-test conditions | 
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_SAPI_04 |
|:--------------------|:---------------|
| Objective           | Uninstall a Script
| References          |
| Pre-test conditions | 
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

## Experimental

Test Cases in this section are optional and test features from the [proposals](https://github.com/w3c/wot/tree/master/proposals).

### Explicit Bindings

| Identifier          | TC_WOT_EXP_01 |
|:--------------------|:---------------|
| Objective           | Perform Read Method
| References          |
| Pre-test conditions | 
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_EXP_02 |
|:--------------------|:---------------|
| Objective           | Perform Write Method
| References          |
| Pre-test conditions | 
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_EXP_03 |
|:--------------------|:---------------|
| Objective           | Perform Create Method
| References          |
| Pre-test conditions | 
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_EXP_04 |
|:--------------------|:---------------|
| Objective           | Perform Delete Method
| References          |
| Pre-test conditions | 
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 

| Identifier          | TC_WOT_EXP_05 |
|:--------------------|:---------------|
| Objective           | Perform Subscribe Method
| References          |
| Pre-test conditions | 
| **Test sequence**   | 
| 1. Stimulus         | 
| 2. Check            | 
| 3. Check            | 
| 4. Verify           | 
