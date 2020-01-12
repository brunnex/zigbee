---
model: 73741  
vendor: Sylvania
title: Smart+ Full Color RT 5/6 Recessed Lighting Kit
category: light
functions:  on/off, brightness, color temperature, color xy
image: /assets/images/devices/73741.jpg
compatible: [z2m]
mlink: https://consumer.sylvania.com/our-products/smart/product-info/zigbee/sylvania-smart-zigbee-full-color-rt-56-recessed-lighting-kit/index.jsp
link: https://www.amazon.com/SYLVANIA-Recessed-Lighting-Changing-Dimmable/dp/B0196M601A
link2: 
link3: 
---
### Set default power on/off transition
Various Osram/Sylvania LED support setting a default transition when turning a light on and off.
```js
{
    "osram_set_transition": 0.1,            //time in seconds (integer or float)
}
```

### Remember current light state
Various Osram/Sylvania LED support remembering their current state in case of power loss, or if a light
is manually switched off then on. Lights will remember their respective attributes
(i.e. brightness, color, saturation, etc.).
NOTE: This must be executed everytime you make changes to a light's attributes for it to then 'remember' it.
```js
{
    "osram_remember_state": true,            // true, false (boolean)
}
```


### Device type specific configuration
*[How to use device type specific configuration](https://www.zigbee2mqtt.io/information/configuration)*


`transition`   
Controls the transition time (in seconds) of brightness,
color temperature (if applicable) and color (if applicable) changes. Defaults to `0` (no transition).
Note that this value is overridden if a `transition` value is present in the MQTT command payload.


#### Manual Home Assistant configuration
Although Home Assistant integration through [MQTT discovery](https://www.zigbee2mqtt.io/integration/home_assistant) is preferred,
manual integration is possible with the following configuration:


{% raw %}
```yaml
light:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    brightness: true
    color_temp: true
    xy: true
    schema: "json"
    command_topic: "zigbee2mqtt/<FRIENDLY_NAME>/set"

sensor:
  - platform: "mqtt"
    state_topic: "zigbee2mqtt/<FRIENDLY_NAME>"
    availability_topic: "zigbee2mqtt/bridge/state"
    unit_of_measurement: "-"
    value_template: "{{ value_json.linkquality }}"
```
{% endraw %}

