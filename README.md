# ECC608-httpsconnection-ioprotection

This issues "GET" request to https server and get a responce with IO protection for ECDH premaster secret transmission, which is provided by ATECC608 capability.

# Requirements

  Platformio with VS Code environment.
  install "Espressif 32" platform definition on Platformio  
  Prior to compile this project, you must copy "cert_chain.c", which is made by privious step [ECC608-Provision](https://github.com/kmwebnet/ECC608-Provision) to "src" folder.  

  you need to modify the definition and variables in main.c as follows:  
  ```
// your SSID and PASS
#define EXAMPLE_WIFI_SSID ""
#define EXAMPLE_WIFI_PASS ""

// Trusted CA certificate for verifying HTTPS server
const unsigned char rootcacert[]={
"-----BEGIN CERTIFICATE-----\n"
"-----END CERTIFICATE-----\n"
};

// URL , port number which you want to connect
const esp_mqtt_client_config_t mqtt_cfg = {
.uri = "mqtts://testcorp.com:8883",

  ```


# Environment reference
  
  Espressif ESP32-DevkitC
  this project initialize both of I2C 0,1 port, and the device on I2C port 0 is BME280 ambient sensor.
  pin assined as below:


      I2C 0 SDA GPIO_NUM_18
      I2C 0 SCL GPIO_NUM_19

      I2C 1 SDA GPIO_NUM_21
      I2C 1 SCL GPIO_NUM_22
          
  Microchip ATECC608(on I2C port 1)

# Usage

you need to change a serial port number which actually connected to ESP32 in platformio.ini.

# Result

If you run this project with success, you can find the results on serial console as follows:

```
I (19625) MQTT_CLIENT: Sending MQTT CONNECT message, type: 1, id: 0000
I (19635) ECC608: MQTT_EVENT_CONNECTED
I (19645) ECC608: sent subscribe successful, msg_id=48637
I (19645) ECC608: sent subscribe successful, msg_id=55581
I (19645) ECC608: sent unsubscribe successful, msg_id=14630
I (19655) ECC608: MQTT_EVENT_SUBSCRIBED, msg_id=48637
I (19665) ECC608: sent publish successful, msg_id=0
I (19665) ECC608: MQTT_EVENT_SUBSCRIBED, msg_id=55581
I (19675) ECC608: sent publish successful, msg_id=0
I (19675) ECC608: MQTT_EVENT_UNSUBSCRIBED, msg_id=14630
I (19685) MQTT_CLIENT: deliver_publish, message_length_read=19, message_length=19
I (19685) ECC608: MQTT_EVENT_DATA
TOPIC=/topic/qos0
DATA=data
I (19695) MQTT_CLIENT: deliver_publish, message_length_read=19, message_length=19
I (19705) ECC608: MQTT_EVENT_DATA
TOPIC=/topic/qos0
DATA=data
Free Heap Size 8bit = 128120
Free Heap Size 32bit = 190296
I (24175) ECC608: Stack remaining for task 'main' is 1904 bytes
I (24185) MQTT_CLIENT: deliver_publish, message_length_read=97, message_length=97
I (24185) ECC608: MQTT_EVENT_DATA
TOPIC=/topic/qos0
DATA={"Temparature": "26.485141" , "Pressure": "1004.483107" , "Humidity": "53.987691"}
I (25325) MQTT_CLIENT: deliver_publish, message_length_read=97, message_length=97
I (25325) ECC608: MQTT_EVENT_DATA
TOPIC=/topic/qos0
DATA={"Temparature": "26.947010" , "Pressure": "1005.009985" , "Humidity": "59.377412"}
```

# License

This software is released under the MIT License, see LICENSE.
