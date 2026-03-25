# MQTT Dashboard examples for Zigbee2MQTT

# Introduction

Starting out with MQTT Dashboard is a little daunting mainly due to a lack of examples and details on how to configure MQTT Dashboard, below is what I found to work.

This documante assumes a MQTT server setup and working, you also have Zigbee2MQTT setup and working and you have MQTT Dashboard setup and working.

## Adding a soil moisture sensor

[Zigbee soil monitoring sensors](https://www.aliexpress.com/item/1005008987466283.html) seem to work well and provide temperature, humidity and soil moisture readings.

It's advisable to set the friendly name for your sensor in Zigbee2MQTT to something more memorable and unique such as 'SoilSensor1', you can do this by going to the devices page and clicking on the current friendly name and then clicking the edit icon next to the friendly name. By default this will be 0x followed by a hex string which can be used if you don't change it.

From the home screen click on the '+' button toward the bottom right on the screen.

Select 'Create Widget'.

Enter a label for your widget in the 'Name' text box, then pick a widget group.

### Adding a humidity reading

First touch on 'Text' in the 'Widget Properties' section.

Type a reading name for the sensor in the 'Name' text box. Under 'Type' select numeric.

Then set the 'Icon' to the picture of the rain drop with a percentage symbol, it's toward the bottom of all the icons, as this will be for humidity then click 'OK' at the bottom.

Then set a colour if you wish.

Make sure 'Broker' is set to the MQTT broker you added when setting up MQTT Dashboard.

For 'Subscription' you need to set this to 'zigbee2mqtt/' and the device's friendly name in Zigbee2MQTT, so in this case it would be zigbee2mqtt/SoilSensor1.

Tick the 'JsonPath parse data' check box, then in the 'JsonPath parse data (payload)' text box set it to '$.humidity'.

For 'Decimal places' set this to '0'

Click 'Done'

### Adding a moisture reading

Click on the '+' button under the 'Widget Properties' section.

As above enter a reading name and under 'Type' select numeric.

Set the 'Icon' to the same rain drop with the percentage symbol.

The rest of the details should be pre-filled from the humidity settings.

Again tick the 'JsonPath parse data' check box, then in the 'JsonPath parse data (payload)' text box set it to '$.soil_moisture'.

For 'Decimal places' set this to '0'

Click 'Done'

### Adding a temperature reading

Click on the '+' button under the 'Widget Properties' section.

As above enter a reading name and under 'Type' select numeric.

Set the 'Icon' to the thermometer symbol on the second row, I then set the colour to black as the icon defaults to red.

The rest of the details should be pre-filled from the humidity settings.

Again tick the 'JsonPath parse data' check box, then in the 'JsonPath parse data (payload)' text box set it to '$.temperature'.

For 'Decimal places' set this to '1'

Click 'Done'

### Adding a LQI reading (optional)

I found it useful to use the 4th and final box to show the LQI reported by the sensor as this will give visual feed back if the placement of the sensor is too far from your Zigbee co-ordinator or router.

Click on the '+' button under the 'Widget Properties' section.

As above enter a reading name and under 'Type' select numeric.

Set the 'Icon' to the signal symbol on the right side of the top row, the icon defaults to red so feel free to change the colour if that doesn't suit.

The rest of the details should be pre-filled from the humidity settings.

Again tick the 'JsonPath parse data' check box, then in the 'JsonPath parse data (payload)' text box set it to '$.temperature'.

For 'Decimal places' set this to '0'

Click 'Done'
