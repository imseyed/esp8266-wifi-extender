# esp8266-wifi-extender

This project https://github.com/imseyed/esp8266-wifi-extender is forked from https://github.com/Pius171/esp8266-wifi-extender

Since I love ESP boards, especially the ESP8266, I was looking for a lightweight solution to extend my WiFi range and connect a network of various nodes.

I found Pius171's project to be a lightweight WiFi extender code that works well for IoT devices and can be used alongside other firmware components. However, as Pius171 himself mentioned, it was not compatible with newer versions of the ESP8266.

I have now upgraded it to support newer ESP8266 versions, and you can use it properly.

In this version, various protocols such as MQTT, SNMP, DNS, and HTTP have been tested, and all of them work flawlessly.

---
> Main project Quote:

Here are some features of my WiFi range extender:

- Scan for networks (refresh the page to scan)

- WiFi manger via web ui

- led indicator for debugging 

- Reset button to return to the factory setting



### flashing with esptool
**First install esptool**
`pip3 install esptool`

**Erase flash**
`esptool.py --port /dev/ttyUSB0 erase_flash`
if you are using windows change /dev/ttyUSB0 to the COM port your esp8266 is connected to.

**Upload bin file**
run this on the terminal
`esptool.py --port /dev/ttyUSB0 write_flash -fs 4MB -fm dout 0x0 [bin file location]`
Do not include the bracket in the terminal.

## Speed test
Before we go into the nitty-gritty of this article, take a look at the speed test. 
There is roughly an 80% speed drop 😥️😥️😥️. Yes that is a lot

Here is my router speed.

![router speed test](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8tkh632r5534393lcb0v.png)

Here is the extender speed

![router speed](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3ui89twkk342j6qfpv74.png)

I repeated this test twice which gave me roughly 80% speed drop. The good thing is that there is no speed drop when you add more extenders.

## Debugging with blinking rate

- Led blinking every second - config file does not exist and web portal is active.

- Led blinking every 200ms - connection is successful and repeater is ready to run.

- Led stays off - there is a problem with the repeater.

- Led stays on(no blinking) - trying to connect to router.

## Setting things up from the web interface
The default IP address for the device is 192.168.4.1, during the first run of the device the config file( a file containing the details of the router to connect to) does not exist, so it start the web server ( the led blinks every one second to indicate this), the default name for the device is _Pius_Electronics_extender0001_ connect to the WiFi network and type in the IP address in your browser you will be be greeted by the web page.

![Image](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7v1iiozqoatcbt7gniin.png)
 

Click on the scan button to scan for network select the network(router) you want to connect to input the password(router's password) and type in the name you want the extender to have in the text box labelled AP name,and click submit.The extender will have the same password as the router it is connected to. If the led starts blinking at a fast rate (200ms) this means the connection is successful, you can now connect to the extender and use it.

## Automesh
The extender does not automesh, but a workaround will be to connected consecutive extenders to each other i.e connect extender2 to extender1, extender3 to extender2, extender4 to extender3 and so on depending on how many extenders you need. If you have a better method you came make a pull request to my [GitHub repository](https://github.com/Pius171/esp8266-wifi-extender).

So if you are okay with a 80% speed drop, then you can try out this extender. Thank you so much for reading.
