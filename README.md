# Chatterbox 

## Aim:

A probably outdated-by-now project to create OpenAI assistants with access to manuals for equipment like 3d-printers in order to make it easier and funner for new users to learn to use said equipment. Bonus addition of voice effects to differentiate the voices a bit from stock open-AI voices. 

In many ways, this project is like a home assistant speaker box. While an internet/phone application would likely be the best implimentation of such a concept from a cost perspective, I started doing this and had a bit of fun learning along the way. 

This is similar to the chatbot designed by [pdp12](https://www.instructables.com/Customizes-a-ChatGPT-Assistant-Using-a-RaspberryPi/). In this case I am making a hobbyist hat for a raspberry pi zero two W.

## Assumed Knowledge:
It is assumed that you are comfortable with soldering, hooking together breakout dev boards for chips, using a raspberry Pi OS and/or SSH and python programming.

## Hardware:
![image of a Raspberry Pi Zero Two W with many rainbow ribbon innie-to-innie cables connecting a computer key switch, a DAC amp, a 3W speaker, and an I2S MEMS Microphone V1.0](PXL_20241026_100359807.MP.jpg)

## To use:
Use the Raspberry Pi Imager to load the OS onto the Raspberry Pi Zero Two W.

An OpenAI account and subsquent API key is required.
Save your API details into the .env file


## Code:
This code needs to be cloned and put on the Raspberry Pi Zero Two W.
You will need to then install the required libraries with the following command:
```
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

## Setup for auto-starting on boot: 
To have it auto-start on boot, you need to add teh chatter.service to the /etc/systemd/user directory.

If your user for the pi is not chatter2 you will need to modify the following lines int eh chatter.service file:
Environment="USER=chatter2"         # the user you want to run the service as
Environment="HOME=/home/chatter2"   # the home directory of the user
ExecStart="/home/chatter2/Chatterbox/start.sh" # location of the start.sh file

Then as the user you want to run the service, enable the service with the following command:
```
systemctl --user enable chatter.service
```

You will also need to make sure the user is logged in automatically on boot. You do this by going to the Raspberry Pi Configuration tool and setting the user to auto-login.
```
sudo raspi-config
```
System Options -> Boot / Auto Login -> Console Autologin

## To do: 
The ability to close old threads and start new threads would be nice
Stream the audio to the API to speed up the processing times.
