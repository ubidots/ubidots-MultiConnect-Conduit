# MultiConnect Conduit

<img class="imgBody" src ="/images/conduit.png" style="display: block;" />

MultiConnect® Conduit™ is a programmable gateway that uses an open Linux development environment to enable machine-to-machine (M2M) connectivity using various wireless interfaces. It also provides an online application store as a platform for developers to provision and manage their gateway and associated sensors and devices.

## Requiremets

* [An MTAC-LORA-915](http://www.multitech.com/models/94557148LF).
* [MultiTech MultiConnect Conduit](http://www.multitech.com/brands/multiconnect-conduit).
* [A MultiConnect® mDot™ Micro Developer Kit](http://www.multitech.com/brands/micro-mdot-devkit)
* An Ethernet cable

## Setting up Hardware configuration

1. Install the LoRa mCard:
    * Disconnect power to the gateway device.
    * At the back of the housing, determine where you want to install the accessory card. You can install the card in either the AP1 or AP2 port. Remove the port cover and retain the screw.
    * Slide the card into the opening and push until you feel the card connector seat in the internal connector.
    * Use a small screwdriver to attach the card bracket to the housing with the screw from the port cover.
2. Attach the LoRa antenna to the LoRa mCard.
3. Install a Mini SIM card:
    * At the front of the Conduit housing, remove the screw that secures the nameplate to the Conduit and remove the nameplate.
    * Locate the SIM card holder in the upper right corner of the opening. If a SIM card is installed and needs to be removed, slide it out of the SIM card hold.
    * Gently push the new SIM card into SIM card holder face up with the cut corner to the right and the SIM contacts facing toward the Conduit’s interior.
    * If not installing a battery or micro SD card, reattach the MultiTech nameplate to the Conduit using the screw removed in before step.
4. Install a Micro SD card (optional):
    * At the front of the Conduit, remove the screw that secures the MultiTech nameplate.
    * Locate the SD card at the left side of the opening, on the underside of the PC board.
    * If an SD card is already installed, gently push the card to release it from its setting and remove it with your fingers.
    * With the new SD card contacts facing up and toward the interior of the Conduit, gently push the card into the slot to secure it.
5. Install a battery (optional):
    * At the front of the Conduit housing, remove the screw that secures the MultiTech nameplate to the housing.
    * The battery holder is located at the right side of the opening on the underside of the PC board. To remove an existing battery, use non-metal tweezers as necessary.
    * Orient the new battery so that the positive (+) pole is facing down. Use your fingers or non-metal tweezers to insert the battery into the holder.
    * Reattach the MultiTech nameplate to the housing using the screw removed in before step.
6. Use the Ethernet cable to connect the MultiConnect Conduit to your pc.
7. Connect the power cord to an outlet or power strip and to the power adapter.
8. Connect the power adapter to the barrel jack on the back panel of the device. The Power LED comes on immediately after power is applied. Wait for the Status LED to begin blinking.


## Setting up Ethernet configuration

1. Open an Internet browser. In the browser’s address field, type the default address for the device: http://192.168.2.1 when login page will appear type default user name (admin) and default password (admin).
    <img class="imgBody" src ="/images/conduitLogIn.png" style="max-width:100%; display: block;" />
2. Go to **Setup** and click on **Network Interfaces**.
    <img class="imgBody" src ="/images/conduitSetUp.png" style="max-width:100%; display: block;"/>
3. There press click on the pen of **eth0**.
    <img class="imgBody" src ="/images/conduitEth0.png" style="max-width:100%;display: block;"/>
4. Now configure Typre to **LAN** and  Mode to **DHCP Client**.
    <img class="imgBody" src ="/images/conduitLAN.png" style="max-width:100%;display: block;"/>
5. Go back to **Setup** and click on **Lora Network Server**.
    <img class="imgBody" src ="/images/conduitSetLora.png" style="max-width:100%;display: block;"/>
6. Setup the **Lora network name**, **Frequency Sub-Band** and **Passphrase**.
    <img class="imgBody" src ="/images/conduitSettingLora.png" style="max-width:100%;display: block;"/>
7. Click on Apps label and press Node-RED.
    <img class="imgBody" src ="/images/conduitInNode.png" style="max-width:100%;display: block;"/>

## Setting up Mobile configuration

1. Open an Internet browser. In the browser’s address field, type the default address for the device: http://192.168.2.1 when login page will appear type default user name (admin) and default password (admin).
    <img class="imgBody" src ="/images/conduitLogIn.png" style="max-width:100%;display: block;"/>
2. Go to **Cellular > Cellular Configuration** to display the Cellular Configuration window.
    <img class="imgBody" src ="/images/conduitCellConfig.png" style="max-width:100%;display: block;"/>
3. Check the Enabled box.
    <img class="imgBody" src ="/images/conduiCellCheck.png" style="max-width:100%;display: block;"/>
4. For GSM radios, enter the **APN** in the field located in the **Modem Configuration** section of the window.
    <img class="imgBody" src ="/images/conduitCellAPN.png" style="max-width:100%;display: block;"/>
5. Click Submit.

## Setting up Node-RED

>Text to import

```html
[{"id":"cb0c6b19.32c128","type":"lora in","name":"","datatype":"utf8","x":193,"y":227,"z":"864cde4d.3761a","wires":[["6b84ed6c.0bfdb4"]]},{"id":"97782f3b.a148d","type":"tcp out","host":"translate.ubidots.com","port":"9010","beserver":"client","base64":false,"end":true,"name":"","x":619,"y":256,"z":"864cde4d.3761a","wires":[]},{"id":"6b84ed6c.0bfdb4","type":"function","name":"","func":"var data = {};\nvar TOKEN = \"Your_Token_Here\";\nvar VARIABLE_NAME = \"Your_Variable_Name_Here\";\n\ndata.payload = \"mDot/1.0|POST|\"+TOKEN+\"|\"+msg.datr+\"=>\"+VARIABLE_NAME+\":\"+msg.payload+\"|end\";\n\nreturn data;","outputs":1,"noerr":0,"x":372,"y":167,"z":"864cde4d.3761a","wires":[["97782f3b.a148d"]]}]
```

To setting up the Node-RED you just need to follow next steps:

1. Click on the upper right corner button, select **Import** label and next **Clipboard** label.
    <img class="imgBody" src ="/images/nodeREDimport.png" />
2. Inside of the blank square paste our code of **Text to import**.
    <img class="imgBody" src ="/images/nodeREDsquare.png" />
3. Click on **Ok** and paste the block diagram.
    <img class="imgBody" src ="/images/nodeREDblock.png" />
4. Press double click on function label of new diagram and change **TOKEN** for your personal token and **VARIABLE_NAME** for the variable name that you want to send.
    <img class="imgBody" src ="/images/nodeREDfunction.png" />
