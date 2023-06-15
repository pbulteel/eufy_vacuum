# Eufy Robovac control for Python
Archiving as there's a better implementation

https://github.com/bmccluskey/robovac

Work in progress! This is a fork of a fork. 

## Installation
Pre-requisites:
* openssl (used for encryption)

```
git clone https://github.com/pbulteel/eufy_robovac.git
cd eufy_robovac
python3 -m venv .
bin/pip install -e .
```
Or see futher below...

## Demo usage
```
bin/demo DEVICE_ID IP LOCAL_KEY
```

The demo:
* connects to your device,
* prints its state out,
* starts cleaning,
* waits 30 seconds,
* sends the device home,
* waits 10 seconds,
* disconnects & exits

## Home Assistant integration

**EXPERIMENTAL!**

## Using HACS
In HACS add this repo as an additional repository. I'm currently working on making it appear automatically. Install it. 

Add the following to your configuration.yaml
```
eufy_vacuum:
  devices:
  - name: Robovac
    address: 192.168.1.80
    access_token: YOUR LOCAL KEY HERE
    id: YOUR DEVICE ID HERE
    type: T2118
```
It looks like you need an older version of the EufyHome app to be able to get the LOCAL KEY and DEVICE ID. 

Restart HA.

## Using Manual Process

Clone/Download the custom_component/eufy_vacuum directory. Add the same lines to your configuration.yaml and restart HA.
