### Preparation for online-plugfest

#### Scenarios

- Test scenario 1: Smart house / Smart building
  - Scenario (draft)
    1. Passive IR sensor detect human (Fujitsu environment sensor)
    1. Turn on appliances
       - Turn on air conditioner (Panasonic air conditioner)
       - Turn on light (Philips hue light)
    1. Monitor power generation from solar panel (Oracle solar panel simulator)
       - Monitor power generation (Oracle solar panel simulator)
    1. When power generation below the lower limit, turn off unused appliances
       - Turn off other air conditioners (Fujitsu air conditioner, Oracle HVAC simulator)
       - Turn off other lights (Mozilla LED light)
    1. Check status
       - Monitor power consumption (Fujitsu smart meter)
  - Test phases
    - Phase 1: Simple communication test  
        - Fujitsu
          - Turn on/off air conditioner ... passed
          - Turn on/off led light ... passed
          - Read power cnsumption value from smart meter ... passed
          - Read PIR data from environment sensor ... passed
        - Panasonic
          - Turn on/off air conditioner ... passed
          - Turn on/off led light ... passed
        - Oracle
          - Read power power generation value from solar panel simulator ... not tested
          - Turn on/off HVAC simulator ... not tested
    - Phase 2: Run application (If prepared)
![scenario1][]
- Test scenario 2: Industrial integration
  - Scenario (draft)
    1. Monitor environment
       - Monitor temperature, humidity, etc. (Fujitsu environment sensor)
       - Display current temperature (Panasonic bulletin board)
    1. Detect turnover
       - Monitor Z axis acceralation (Fujitsu environment sensor)
    1. Turn on warning devices
       - Turn on beacon light and buzzer (Fujitsu beacon light, Fujitsu buzzer)
       - Change light color to red (Mozilla LED light)
    1. Control plant facilities
       - Turn off air conditioners (Panasonic air conditioner, Oracle HVAC simulator)
       - Turn off devices (Oracle blue pump simulator, Oracle fest plant simulator)
  - Test phases
    - Phase 1: Simple communication test  
        - Fujitsu
          - Turn on/off beacon light ... passed
          - Turn on/off buzzer ... passed
          - Turn on/off LED light ... passed
          - Change light color ... passed
          - Read sensor data from environment sensor ... passed
        - Panasonic
          - Turn on/off air conditioner ... passed
          - Turn on/off bulletin board ... passed
          - Set numer to bulletion board ... passed
        - Oracle
          - Turn on/off HVAC ... not tested
          - Turn on/off blue pump ... not tested
          - Open/Close valve on fest plant simulator ... not tested
          - Start/Stop pump on fest plant simulator ... not tested
    - Phase 2: Run application (If prepared)
![scenario2][]

[scenario1]:images/test_scenario_1.png
[scenario2]:images/test_scenario_2.png

#### Logistics
- vpn server
  - DHCP? / Fixed IP?
  - Can mDNS work over VPN?

#### Participants
Intel, Fujitsu, TUM, Siemens, Oracle, Hitachi

#### Date
Spet 10th, 9am-11am CDT, 4pm-6pm JST (+1 hour?)

#### Logistics

* WebEx and IRC

We will use the https://www.w3.org/WoT/IG/wiki/PlugFest_WebConf WebEx and IRC.

* Google Hangout (Matthias)
   - Used to video stream remote devices such as Festo Live or Panasonic Lab
   - https://hangouts.google.com/call/Gbgym9gd5j4OUEppg5VJAEEE (the one we used for the Online PlugFest on Sep 10)
   - https://hangouts.google.com/call/zMIBFnSSTxd4KpiLcP5DAAEI



