# What do your want to do?

## Curious First time user

## Subscribe to signals in vehicle

## Playback a recording from another broker

# What is this?

## Realtime

## Record

## Replay

## Stack

HW and SW

# Getting started

## Installation

### RasperryPi

For convienince purposes we provide prebuilt [Raspberry Pi 4 images](https://www.beamylabs.com/releases/) with the [Seeed CAN-shield](https://www.seeedstudio.com/2-Channel-CAN-BUS-FD-Shield-for-Raspberry-Pi-p-4072.html) drivers. 



!> **Prerequisites**<br>
   Raspberry Pi + CAN-BUS HAT for Raspberry Pi<br>
   Raspberry Pi Imager for installation and it can be downloaded here https://www.raspberrypi.org/software/<br>
   SD card in an SD card reader connected to your computer

1. Download the latest image from https://www.beamylabs.com/releases/. At the time of writing this is *rpi-20220701_192701.img.gz*. 
2. In Raspberry Pi Imager, choose "Use custom" and then select the downloaded image and write the image to the SD card.
3. Put the SD card in the Pi
4. Connect the Pi with ethernet to a WiFi router with Internet access if avaialable( highly recommended)
5. Boot the Pi, this might take a few minutes the first time
6. Next its time to connect to the Pi with a web-browser but first we need to get the IP
   to the broker.

   **Connected to Internet through WiFi router**

   If possible, the easiest way is the get the IP from your router.

   If this is not possible, you need to connect to the brokers internal WiFi access point.
   From your phone or computer, connect using WiFi **beamy-\*** (password: beamylabs) and navigate to http://192.168.4.1:8080. Under "About" your can find the URL where the broker is accessible on your regular WiFi.

   ![alt text](images/webclient_accessible_on.png "License and upgrading")

   Change back to your regular WiFi and use http://ip_in_your_router:8080 instead. You know have Internet
   access from both your client and the broker which will make things easier as we move on.
 
   **Not connected to WiFi router**

   If you are not connected to Internet, you need to connect to the brokers internal WiFi access point.
   From your phone or computer, connect using WiFi **beamy-\*** (password: beamylabs)and navigate to http://192.168.4.1:8080. 
   In this state there is no Internet access on your desktop or your browser which means that things get
   a bit more complicated as we move on.


7. In web-client -> About it should now look something like this.

   ![alt text](images/Unlicenced_broker.png "License and upgrading")

8. Next step is to request a [License](#Acquire-your-License)


### Linux + Docker

!> You will need git, docker, docker-compose installed on your linux distribution


This part will explain how to install and run beamy-broker on linux with docker.

1. Clone the beamylabs-start git repository and go into that directory

   ```
   git clone https://github.com/beamylabs/beamylabs-start.git
   cd beamylabs-start
   ```

2. Start broker and web-client with docker-compose

   ``docker-componse up -d``

   This will start the beamy-broker together with the web-client on port 8080

3. Go to the "About" page in the web-client.

   If you run this on your local computer, use a browser and go to http://127.0.0.1:8080/#/about,
   otherwise replace 127.0.0.1 with the ip/hostname of the computer.

   You should se something like this

   ![alt text](images/Unlicenced_broker.png "License and upgrading")

   When you want to stop run ``docker-compose down``
   
4. Next step is to request a [License](#Acquire-your-License)

# Acquire your License

Running BeamyBroker requires a valid license. After installing BeamyBroker you can request a license through the web client (or through the license API).

![alt text](images/Unlicenced_broker.png "License and upgrading")

!> If you are not connected to Internet, pay extra attention to the steps in the guide since you 
   will need to switch back and forth between networks on your desktop.


1. Press "ACQUIRE NEW LICENSE" 

   !> Your email MUST be part of an organisation with a licence policy, otherwise a 30 day trial
      version is created for you

2. Enter your email to request a license

3. Wait for the returning e-mail and copy/paste the licence phrase and press "ADD LICENSE"

4. Under "About" it should now look something like this and you are now good to start use your broker.

     ![alt text](images/licenced_broker.png "License and upgrading")

5. To verify that your installation is successful you can navigate to "Traffic Monitor" and replay 
   a test drive that comes bundled. Expand the "Try out preconfigured and automatic playback" and press
   "START PLAYBACK".

    ![alt text](images/traffic_monitor_notraffic.png "License and upgrading")

   This will upload a broker configuration together with a recorded drive, then start the recording and subscribe to some of the signals.

   If everything is ok, you should see some graphs beeing displayed with "live" data.

   ![alt text](images/test_drive_graphs.png "License and upgrading")

   You know have a working and licenced broker. _What_do_next_ ?

   


# Your first configuration

!> Requires that you have equipment to connect to the car your want to subscribe to signals from and
   that this equipment is properly setup.<br>
   You also need a dbc file that matches the car model

Once the broker is done you can use the web-client to generate a configuration that the broker can
use.

There are two ways to configure the broker, one is to use the UI wizard and the other way is to upload a configuration directory containing the required files. Here we will use the wizard.

1. In the menu in web-client choose "Configuration" and you should see something like this.

      ![alt text](images/configuration.png "License and upgrading")

2. Under "Don´t have a configuration?" , press "Create configuration __here__" to start the wizard.
   
   Pick your dbc file and then you can just click through all steps without any changes. The last step "Reconfigure" will upload the configuration to the broker

3. Your broker is now ready to subscribe to signals in your car.
