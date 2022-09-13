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
4. Connect the Pi to wired ethernet so it gets Internet access, where it will download additional upgrades when available (highly recommended)

!> ssh access is by default only available over wired ethernet. Username/pwd pi/Aut0m0tive

5. Boot the Pi, this might take a few minutes the first time
6. Next it's time to connect to the Pi with a web-browser but first we need to resolve the IP to the broker.

   **Connected to Internet through WiFi router**

   If possible, the easiest way is the get the IP from your router.

   If this is not possible, you need to connect to the brokers internal WiFi access point.
   From your phone or computer, connect using WiFi **beamy-\*** (password: beamylabs) and navigate to http://192.168.4.1:8080. Under "About" your can find the URL where the broker is accessible on your regular WiFi.

   ![alt text](images/webclient_accessible_on.png "License and upgrading")

   Change back to your regular WiFi and use http://ip_in_your_router:8080 instead. You now have Internet
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

### Code samples

When your broker is up and running you are ready to connect and run your own code.

We offer a few code examples at our [Github samples repository](https://github.com/remotivelabs/remotivelabs-samples).

As a developer you may choose to use our maintained libraries or work directly towards our public _gRPC interface_.

#### Python

The [Python](https://www.python.org/) samples are found in the [python directory](https://github.com/remotivelabs/remotivelabs-samples/python) in our samples repository. All the Python samples use our Python library which is available in the Python Package manager [PyPi](https://pypi.org/user/remotivelabs/).

Install the Python library with `pip` in a terminal:

    pip install remotivelabs-broker

After the installation in complete you may execute any of the samples in the Python directory.

Remember all our samples requires a broker which is up and running. Each sample is provided with a _readme_ file explaining how to run the sample with the necessary arguments.

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
   "Start playback".

    ![alt text](images/traffic_monitor_notraffic.png "License and upgrading")

   This will upload a broker configuration together with a recorded drive, then start the recording and subscribe to some of the signals.

   If everything is ok, you should see some graphs beeing displayed with "live" data.

   ![alt text](images/test_drive_graphs.png "License and upgrading")

   You know have a working and licenced broker. _What_do_next_ ?

   


# Your first configuration

!> Requires that you have equipment to connect to the car your want to subscribe to signals from and
   that this equipment is properly setup.<br>
   You also need a dbc file that matches the car model

Once the broker is operational with a license you can use the web-client to generate a configuration that the broker can
use.

There are two ways to configure the broker, one is to use the UI wizard and the other way is to upload a configuration directory containing the required files. Here we will use the wizard.

1. In the menu in web-client choose "Configuration" and you should see something like this.

      ![alt text](images/configuration.png "License and upgrading")

2. Under "Don´t have a configuration?" , press "Create configuration __here__" to start the wizard.
   
   Pick your dbc file and then you can just click through all steps without any changes. The last step "Reconfigure" will upload the configuration to the broker

3. Your broker is now ready to subscribe to signals in your car.

## About configuration

You can always query the current configuration in the menu. In web-client choose "Configuration" and you should see a valid configuration.

![alt text](images/current_can_configuration.png "Current configuration")

The following is a typical and very simple configuration
```json
{
  "chains": [
    {
      "namespace": "my_can0",
      "type": "can",
      "database": "can/MyCAN.dbc",
      "device_name": "can0"
    },
    {
      "namespace": "my_can1",
      "type": "can",
      "database": "can/MyOtherCAN.dbc",
      "device_name": "can1"
    }
  ]
}
```
* `namespace` is your given name, which you can choose freely. This is the name you will use when you browse the bus in the `tree view` of write some code to access it. Suggestions would be: `BodyCAN`, `VehicleCan`  
* `type` suggest what kind of physical link we are connectiong to. This could be `can, canfd, vcan, lin, flexray, udp`
* `database` hold information on how to encode and decode the traffic on link. Typlically a file with extenision `ldf, dbc, xml`
* `device_name` is the physical socket representaion on your host computer. These names are controlled by your linux kernel and can be listed by doing `ip a`. On our prebuilt images valid names are `[can0..can1], [vcan0..vcan3]` 

The example above contains two namespaces for the sake of clarity. Your configuration can hold any number of namespace depeding on your hardware setup.

### Upload your custom configuration

You can upload your custom configuration, in the web-client choose "Configuration" and select "Pick directory". For the example above the directory which should be selected should contain the following

![alt text](images/configuration_folder.png "Current configuration")

Once uploaded the broker will verify that the configuration is valid, if not please verify that your `interfaces.json` and the relative database paths are correct.

## Additonal interfaces

As the configuration above suggested additional interfaces can be added to the existing setup. Some of these setups requires `ssh` and custom configuration of the host, in this scenario, the Raspberry Pi 4.

> Typical usb to ethernet adapter [here](images/USB-to-Ethernet.png) 

> In this case `host` referrs to Raspberry Pi 4

### LIN interfaces

Connect a secondary usb to ETH adapter to the host. Here you can connect a single `LIN transivers` box alternatively a switch with a number of `LIN transivers` each lin transiver is identified and configured according to it's unique `device_identifier`

This id needs to reflect and be present in `interfaces.json`. The following configuration shows two `lin` devices, `8` and `7`. Note that `8` has been configured to operate as master whereas `7` operates as slave.

Each LIN transiver need a unique set of `target_port` and `server port` which can be selected freely. Once the trancivers get powered their configurations will be distributed.

```json
{
  "chains": [
    {
      "namespace": "ecu_A",
      "type": "lin",
      "config": {
        "device_identifier": 8,
        "server_port": 2014,
        "target_port": 2013
      },
      "node_mode": "master",
      "database": "ldf/test.ldf",
      "schedule_file": "ldf/test.ldf",
      "schedule_table_name": "DEVMLIN01Schedule01",
      "schedule_autostart": true
    },
    {
      "namespace": "ecu_B",
      "type": "lin",
      "config": {
        "device_identifier": 7,
        "server_port": 2015,
        "target_port": 2016
      },
      "node_mode": "slave",
      "database": "ldf/test.ldf"
    }
  ]
}
```

!> The prebuilt image will host a DHCP server on the added adapter. LIN transivers and the Broker needs to reside on the same subnet. Other custom topologies are supported and sometimes preferred.

### CAN interfaces (additonal)

Any socketcan compatible USB dongle can be added when physical interfaces are required. Amongst others, [PEAK-System](https://www.peak-system.com/) does provide such devices. 
### FR interfaces

!> Write is currently not supported for FR devices
#### Technica CM CAN COMBO

!> Make sure that your Techinca devices is configured to use `PLP` headers and also make sure to note specified `Destination MAC` (available by clicking `SPY`) typically `01:00:5e:00:00:00`. 

Connect your Technica device to the secondary usb ethernet interface `eth1` which is mentioned above. As mulitcast address provide `Destination MAC`.
```json
{
  "chains": [
      {
         "type": "flexray",
         "device_name": "flexray0",
         "namespace": "MyFlexrayNamespace",
         "config": {
            "target_host": "127.0.0.1",
            "target_port": 51111,
            "hardware": "Technica_CM_CAN_COMBO",
            "target_config": {
               "interface": "eth1",
               "multicast": "01:00:5e:00:00:00"
            }
         },
         "database": "fibex_files/flexray.xml"
      }
   ]
}
```

#### Host Mobility MX-4 T30 FR

Please reach out to us (hello@remotivelabs.com) if you like to use MX30-FR as a flexray bridge.