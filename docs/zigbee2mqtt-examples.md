# MQTT Dashboard examples for Zigbee2MQTT

# Introduction

Starting out with MQTT Dashboard is a little daunting mainly due to a lack of examples and details on how to configure MQTT Dashboard, below is what I found to work.

This documante assumes a MQTT server setup and working, you also have Zigbee2MQTT setup and working and you have MQTT Dashboard setup and working.

## Adding a soil moisture sensor

[Zigbee soil monitoring sensors](https://www.aliexpress.com/item/1005008987466283.html) seem to work well and provide temperature, humidity and soil moisture readings.

From the home screen click on the '+' button toward the bottom right on the screen.

Select 'Create Widget'.

Enter a label for your widget in the 'Name' text box, then pick a widget group and then touch on 'Text' in the 'Widget Properties' section.

Type a reading name for the sensor in the 'Name' text box. Under 'Type' select numeric. Then set the 'Icon' to the picture of the rain drop with a percentage symbol
