# MQTT Dashboard examples for Zigbee2MQTT

# Introduction

Starting out with MQTT Dashboard is a little daunting mainly due to a lack of examples and details on how to configure MQTT Dashboard, below is what I found to work.

This documante assumes a MQTT server setup and working, you also have Zigbee2MQTT setup and working and you have MQTT Dashboard setup and working.

## Adding a soil moisture sensor

[Zigbee soil monitoring sensors](https://www.aliexpress.com/item/1005008987466283.html) provide temperature, humidity and soil moisture readings.

It's advisable to set the friendly name for your sensor in Zigbee2MQTT to something more memorable and unique such as 'SoilSensor1', you can do this by going to the devices page and clicking on the current friendly name and then clicking the edit icon next to the friendly name. By default this will be 0x followed by a hex string which can be used if you don't change it.

From the home screen click on the '+' button toward the bottom right on the screen.

Select 'Create Widget'.

Enter a label for your widget in the 'Name' text box, for example 'GardenBed1', then pick a widget group such as 'Backyard'.

### Adding a humidity reading

Touch on 'Text' in the 'Widget Properties' section.

Type a name for the reading in the 'Name' text box, such as 'Humidity'.

For 'Type' select 'Numeric'.

Then set the 'Icon' to the picture of the rain drop with a percentage symbol, it's toward the bottom of all the icons, as this will be for humidity then click 'OK' at the bottom.

Then set a colour if you wish.

Make sure 'Broker' is set to the MQTT broker you added when setting up MQTT Dashboard.

For 'Subscription' you need to set this to 'zigbee2mqtt/' and the device's friendly name in Zigbee2MQTT, so in this case it would be 'zigbee2mqtt/SoilSensor1'.

Tick the 'JsonPath parse data' check box, then in the 'JsonPath parse data (payload)' text box set it to '$.humidity'.

For 'Decimal places' set this to '0'

Click 'Done'

### Adding a moisture reading

Click on the '+' button under the 'Widget Properties' section.

Enter a name for the reading, such as 'Moisture'.

For 'Type' select 'Numeric'.

Set the 'Icon' to the same rain drop with the percentage symbol.

The rest of the details should be pre-filled from the humidity settings.

Again tick the 'JsonPath parse data' check box, then in the 'JsonPath parse data (payload)' text box set it to '$.soil_moisture'.

For 'Decimal places' set this to '0'

Click 'Done'

### Adding a temperature reading

Click on the '+' button under the 'Widget Properties' section.

Enter a name for the reading, such as 'Temperature'.

For 'Type' select 'Numeric'.

Set the 'Icon' to the thermometer symbol on the second row, I then set the colour to black as the icon defaults to red.

The rest of the details should be pre-filled from the humidity settings.

Again tick the 'JsonPath parse data' check box, then in the 'JsonPath parse data (payload)' text box set it to '$.temperature'.

For 'Decimal places' set this to '1'

Click 'Done'

### Adding a LQI reading (optional)

I found it useful to use the 4th and final box to show the LQI reported by the sensor as this will give visual feed back if the placement of the sensor is too far from your Zigbee co-ordinator or router.

Click on the '+' button under the 'Widget Properties' section.

Enter a name for the reading, such as 'LQI'.

For 'Type' select 'Numeric'.

Set the 'Icon' to the signal symbol on the right side of the top row, the icon defaults to red so feel free to change the colour if that doesn't suit.

The rest of the details should be pre-filled from the humidity settings.

Again tick the 'JsonPath parse data' check box, then in the 'JsonPath parse data (payload)' text box set it to '$.linkquality'.

For 'Decimal places' set this to '0'

Click 'Done'

### Once all boxes have been set

Just click 'Done' and it will take you back to the home screen hopefully showing you the current readings.

## Adding a smart water timer

[Zigbee smart water timers](https://www.aliexpress.com/item/1005009335943136.html) allow you to automate turning water on and off.

As with the soil moisture sensor it's worth while setting a friendly name for the device to something friendlier like 'GardenTap'.

Unlike the soil moisture sensor, smart water timers can be made to turn water on and off and this is a little more complicated as you need to set details in the sending section as well.

From the home screen click on the '+' button toward the bottom right on the screen.

Select 'Create Widget'.

Enter a label for your widget in the 'Name' text box, for example 'GardenTap', then pick a widget group such as 'Backyard'.

### Adding a switch to turn water on and off remotely

Touch on 'Text' in the 'Widget Properties' section.

Type a name for the reading in the 'Name' text box, such as 'Tap' or 'LeftTap' if you have a smart timer with more than one outlet.

For 'Type' select 'Switch'.

For 'Status Icon "On"' there isn't a suitable tap or water icon available, so I picked the power plug icon which can be found on the second lasgt row.

For 'Status Icon "On"' I picked the power plug icon which is crossed out and it can be found on the second lasgt row next to the on icon.

For 'Subscription' in this case it would be 'zigbee2mqtt/GardenTap'.

Tick the 'JsonPath parse data' check box, then in the 'JsonPath parse data (payload)' text box set it to '$.state', if you have more than one outlet this might be '$.state_l1' instead.

In the sending section untick 'Send topic same as subscription topic' if checked.

Set the 'Send Topic' to 'zigbee2mqtt/GardenTap/set'

Zigbee2MQTT expects commands to be in JSON format, so set 'Prefix' to '{"state": "'. Then set 'Suffix' to be '"}'. This is so when MQTT Dashboard transmits an 'ON' command the message body is {"state": "ON"}.

If your smart water timer has more than one outlet you may need to use 'state_l1' instead of state in the above setting, and 'state_l2' for the 2nd outlet.

Note: For JSON to be valid you must use double quotes.

You can leave 'On' set to 'ON' and 'Off' set to 'OFF'.

Click 'Done'

You can either add another outlet or just click 'Done'.

Your should now see one or more switches on the home screen and touching on them should activate the solinoid in the device.

## Debugging

Using the `mosquitto_sub` program you can listen for MQTT packets, this can be useful for identifying the actual device names Zigbee2MQTT uses.

### Listen for all messages under the zigbee2mqtt topic

```
mosquitto_sub -v -u "<mqtt_username>" -P "<mqtt_password>" -h "<server_ip>" -p <server_port> -t "zigbee2mqtt/#"
```

### Listen for all messages from a single device

Zigbee2MQTT can be a bit noisy with status messages, so to only view messages from your device you do the following:

```
mosquitto_sub -v -u "<mqtt_username>" -P "<mqtt_password>" -h "<server_ip>" -p <server_port> -t "zigbee2mqtt/SoilSensor1/#"
```

