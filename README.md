# LoRa Node with AIoTs_GPS_state_tester

## **Introduction**

The AIoTs GPS & state tester is basic on Wio Terminal Chassis-LoRa-E5 and GNSS to develop. It compares with the traditional IoTs has more concise and intelligent. IoTs basically just receive data then do a command action, whatever data is correct, but AIoTs is able to filer the useless data strictly to get the accurate data by an algorithm which is the neural network.
In this project, I am using a built-in 3 axis sensor and the neural network to build up an intelligent recognition action system, it can according to your shake Wio Terminal then currently show you its state. Basically, I have trained in three states which are Stop(WT idle state), Turn(rolling-over WT device) and Wave(take WT to wave your hand). If you want to add more states, please go to [Edge Impulse](https://www.edgeimpulse.com/) training the action as you want.



  <div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/AIoTs_WioTerminal/AIoTs_pic.jpg"/></div>

 ## **Feature**

 - The LoRa device can display the DevEui, APPEui and Appkey on the first page.
 - Neural network algorithm correct data
 - High accurately detect Wio Terminal state
 - Display longitude, latitude and satellites number.
 - Display the device and TTN connection status.
  

## **Hardware** 

This demo you will need the device list as below:

- [**WioTerminal**](https://www.seeedstudio.com/Wio-Terminal-p-4509.html)

- [**Wio Terminal Chassis - LoRa-E5 and GNSS**](https://www.seeedstudio.com/Wio-Terminal-Chassis-LoRa-E5-and-GNSS-p-5053.html)

- [**Wio Terminal Chassis - Battery (Optional)**](https://www.seeedstudio.com/Wio-Terminal-Chassis-Battery-650mAh-p-4756.html)




## **Usage**

This project is based on the Arduino platform which means we’ll be using the Arduino IDE and various Arduino libraries. If this is your first time using the Wio terminal, here is a guide to quickly [**Get Started with Wio Terminal**](https://wiki.seeedstudio.com/Wio-Terminal-Getting-Started/).


Requite library:
- [**Seeed_Arduino_SFUD**](https://github.com/Seeed-Studio/Seeed_Arduino_SFUD)

### **Edge Impulse training**
If you want to add more action to recognized on Wio terminal, please go to the Edge Impulse to training a new library as you want action.
there is training instruction: 

Step 1. 
Open the [**Edge Impulse website**](https://studio.edgeimpulse.com/studio/select-project?autoredirect=1), and regiter a account. 

Step 2. 
Create a new project.
<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/AIoTs_WioTerminal/edge_PIC1.png"/></div>

Step 3.
Download the [**Edge Impulse firmware**](https://github.com/Seeed-Studio/Seeed_Arduino_edgeimpulse/releases/tag/1.4.0) for connect to webside.  

Double click the left button on Wio terminal, you will see a driver popup, then draw the firmware to the driver, the driver will disappear which mean the firmware has been uploaded. More detail on [**the Wio terminal get start**](https://wiki.seeedstudio.com/Wio-Terminal-Getting-Started/).

Step 4.
When you click "connect using WebUSB", the Wio Terminal will connect to the website, then there you can start to training the action as you want.
<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/AIoTs_WioTerminal/Edge_PIC2.png"/></div>

Step 5. 
When you finish all step, you need to select "Deployment" to general you trained library, then put on the third-party library. 



Note
If you need konw more about the Edge Impulse or something still unclear, please go to [**Wio Terminal Edge Impulse Getting Started**](https://wiki.seeedstudio.com/Wio-Terminal-TinyML-EI-1/).



### **TheThingsNetwork Console Configuration Setup**

In this project, The data will display on [**TheThingsNetwork**](https://www.thethingsnetwork.org) platform, the instuction as below:

Step 1: Load into [**TTN website**](https://www.thethingsnetwork.org) and create your account, then go to gateways start to set up your device.

<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/TTN_gataway1.png"/></div>

Step 2: Add the gateway device:
- Owner
- Gteway ID
- Gateway EUI
- Gateway name

<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/TTN_gateway2.png"/></div>

<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/TTN_gateway3.png"/></div>

<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/TTN_gateway4.png"/></div>

Step 3: Add Application:
- Owner
- Application ID
- Application name

<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/TTN_applications.png"/></div>

<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/application2.png"/></div>

Step 4：Add the LoRa node:
- Brand (Select Sense CAP)
- Model (Select LoRa-E5)
- Hardware Ver (Defult)
- Firmware Ver (Defult)
- Profile (The Region is according to your location)
- Frequency plan
- AppEUI
- DEVEUI
- AppKey
- End Device ID

<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/TTN_device1.png"/></div>

<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/TTN_device4.png"/></div>

Step 5: Add the code for decode the data:

<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/TTN_decode1.png"/></div>

```CPP
function Decoder(bytes, port) {
 
  var decoded = {};
  if (port === 8) {
    decoded.Stop   = bytes[1];
    decoded.Turn   = bytes[3];
    decoded.Wave   = bytes[5];
  }
 
  return decoded;
}

 
```

Step 5: Cheack the result on TheThingsNetwork

Go to the geteway, then click "Live data".

<div align=center><img width = 500 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/TTN_dataTEMP1.png"/></div>


Each LoRa device has a unique serial number, after you connect the LoRa device to the Wio terminal then there will display the deveui, appeui and appkey on the first page, you need to fill the LoRa ID and gateway ID in server.

<div align=center><img width = 600 src="https://files.seeedstudio.com/wiki/LoRa_WioTerminal/temp_ID.png"/></div>
