# Cryptocurrency ePaper Ticker 
(supports all 6000+ coins/currencies listed on [CoinGecko](https://api.coingecko.com/api/v3/coins/list))

A Python3 ePaper Cryptocurrency price ticker that runs on a Raspberry Pi connected to a [Waveshare 2.7 inch monochrome ePaper display](https://www.waveshare.com/wiki/2.7inch_e-Paper_HAT) or [Waveshare 2.13 inch monochrome ePaper display](https://www.waveshare.com/wiki/2.13inch_e-Paper_HAT). The script periodically (every 10 mins by default) takes data from CoinGecko and prints a summary to the ePaper.

A few minutes work gives you a desk ornament that will tastefully monitor a coin's journey moonward.

![Action Shot](/images/actionshot/BasicLunar.jpg)

![Action Shot](/images/actionshot/Ws213v2.jpg)

# Getting started

## Prerequisites

(These instructions assume that your Raspberry Pi is already connected to the Internet, happily running pip and has Python3 installed)

If you are running the Pi headless, connect to your Raspberry Pi using ssh.

Install the Waveshare Python module following the instructions on their [Wiki](https://www.waveshare.com/wiki/2.7inch_e-Paper_HAT).

(To install the waveshare_epd python module, you need to run the setup file in their repository)

```
cd e-Paper/RaspberryPi_JetsonNano/python
sudo python3 setup.py install
```
## Install & Run

Copy the files from this repository onto the Pi, or clone using:

Original

```
cd ~
git clone https://github.com/llvllch/btcticker.git
cd btcticker
```

This fork

```
cd ~
git clone https://github.com/estacaco/btcticker.git
cd btcticker
```

Install the required modules using pip:

```
python3 -m pip install -r requirements.txt
```

If you'd like the script to persist once you close the session, use [screen](https://linuxize.com/post/how-to-use-linux-screen/).

Start a screen session:

```
screen bash
```

Run the script using:

```
python3 btcticker.py
```

Detatch from the screen session using CTRL-A followed by CTRL-D

The ticker will now pull data every 10 minutes and update the display. 

# Interface

The ePaper is slow. There is a lag of a few seconds between button press and a change to the display. 

Here's what the buttons do:
- Button 1: Cycle through the cryptocurrencies listed in config.yaml
- Button 2: Rotate Display -90 degrees
- Button 3: Invert Display
- Button 4: Cycle through the fiat currencies listed in config.yaml

Update frequency can be changed in the config.yaml file (default is 600 seconds).

# Run on boot

If you would like the script to run on boot do the following:

Enter the following in command prompt

```
sudo raspi-config
```

Navigate to the boot options in raspiconfig and enable auto-login.

Once completed enter the following into the command prompt:

```
sudo nano /etc/profile
```

Scroll all the way to the bottom of the file and insert at the end:

For the 2.7 inch version

```
sudo python /home/pi/btcticker/btcticker.py
```

For the 2.13 inch version

```
sudo python /home/pi/btcticker/btcticker2in13.py
```

Ctrl+x to exit and 'Y' to save.
From there use:
```
sudo reboot
```

to reboot and test.

This method runs the script automatically after login which we have set to do automatically. Keep in mind this also means when you SSH into the device and login it will attempt to run the script again immediately and will require you to press Ctrl+C to cancel the script loading again and to get the command prompt.

# Contributing

To contribute, please fork the repository and use a feature branch. Pull requests are welcome.

# Links

- Video of the unit working [here](https://youtu.be/TN8lMPppR1c)
- A low(er)-effort kit and frame can be obtained at [https://llvll.ch/btcticker.html](https://llvll.ch/btcticker.html)

# Troubleshooting

Some people have had errors on a clean install of Rasbian Lite on Pi. If you do, run:

```
sudo apt-get install libopenjp2-7
sudo apt-get install libqt5gui5
sudo apt-get install python-scipy
sudo apt install libatlas-base-dev
```

and re-run the script.

If the unit is freezing, try switching to another power supply. 

# Licencing

The code in this project is licensed under MIT license.
