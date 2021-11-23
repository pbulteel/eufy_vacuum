# Eufy Robovac control for Python

Work in progress! This is a fork of a fork, of a fork, its forkception

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
    type: MODEL CODE (Below)
```

**Available Model Codes:**

**30C** T2118 

**G30 Edge** T2251 

**G30 Hybrid** T2253 

**25C** T2123 

**11C** T2103 
   
**35C** T2117 

---

The ‘LocalKey’ is 16 characters long & the ‘devID’ is 21 characters long.

It looks like you need an older version of the EufyHome app to be able to get the LOCAL KEY and DEVICE ID. 

<Update with somewhat accurate instructions to gain the required info>
  
  
  You will need a chromebook for the below instructions. Said chromebook will need to have developer mode active, and the terminal enabled.
  
  You will also need to download the following file, or another copy of Eufyhome at least version 2.4.0: https://drive.google.com/file/d/1qoq03H6Gz_oPSUtwhAaRXDyDNq-T_p4n/view?usp=sharing
  
  Download the file to the "Linux files" location on the chrombook. Unzip if needed to make just .apk.
  
  Next, Install ADB and tools:
  
  ```sudo apt-get install android-tools-adb -y```
  
  In the terminal, navigate to the linux files/where you placed the aforementioend app file.
  
  Now, sideload the app in with ADB:
  
  ``` adb -s emulator-5554 install EufyHome_2.4.0_vevs.apk ```
  
  (the -s emulator-5554 tells adb which emulator to use, this should be the same as yours)
  
  
  Now, Eufyhome should be installed on your chromebook as an app, unless im missing a step...
  
  Run the following to enter into the shell:
  
  ```adb -s emulator-5554 shell```
  
  And you can do your own adb logcat commands, Or, run the following to get the tuya info you need:
  
 ``` adb -s emulator-5554 shell logcat -e 'tuya.m.my.group.device.relation.list' ```
  
  
  With that running in the terminal, open the app on your chromebook, and login using your Eufy credentials, There may be a ton of output from the logcat. But the command above should spit out a big block of text, that will contain:
  
  ```"devId":"21-22 alphanumeric",```
  
  ```,"localKey":"16 Alphanumeric"}],"a":"```
  
  Insert the info gained into the above Home Assitant config Block, and you should be good to go.
  


Yes, you must Restart HA to get the config in place.
  
  
 Once comfirmed good, **UNINSTALL THE APP**, its useless to use, and a security issue. If you need the key again, just do the process over, it takes a few minutes.
  

## Using Manual Process

Clone/Download the custom_component/eufy_vacuum directory. Add the same lines to your configuration.yaml and restart HA.
