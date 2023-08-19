This is an update for the project at:

     https://github.com/palmmaximilian/ReactNativeArduinoBLE

being a noob I wasn't going to push this code onto his.

I am using a Linux OS, so the commands are for that terminal.

## React-Native side
First thing, cloning the original project did not work for me, it ran into all sorts of issues and conflicts between packages and versions, so I followed the steps below.  Note, if you are going to try to clone this project and want to back it up to github you may need to check your git destination is not this one, use:
       git remote -v

if it does need to be changed then use:
       git remote set-url origin <set this bit to your git repo>

If you do clone this do not forget to change your sdk path, and to also run:
      npm install --save

Onto the code, I started a new project using my normal React-Native method:
   npx react-native init BleExample 

I then checked that it built by starting the server:   
   npx react-native start
   
and loading it onto my phone (I don't have an emulator):
   npx react-native run-android

Then I started adding the dependecies and rechecking after each dependency was added, in the end I had to change npm versions and also add one extra dependency to the original code, the packages that worked/were needed were:
   "@react-native-community/checkbox": "^0.5.16",
    "@types/react-native-base64": "^0.2.0",
    "react-native-base64": "^0.2.1",
    "react-native-ble-plx": "^2.0.3"

Check how to install the packages at:   https://www.npmjs.com/

Yes, I added two base64's, that is intentional in resolving some issue.  Incidentally I was using: 
   "react": "18.2.0",
   "react-native": "0.72.4"

After I knew that the project built with the dependencies and template code I copied and pasted the code from/to 'App.tsx' (and had to make some adjustments from the original code), and also had to copy the "Styles/styles.tsx" folder, file and code.  

The project then built (see build instructions above).  

## ESP32 side
The oddity in the code for the ESP was the libraries, I got a conflict and it seems to be from the order of the library imports!  Also, in resolving the issue I added one extra library from the original - maybe it can be removed - I haven't bothered:
   #include <BLE2902.h>    //added, unnecessarily ??
   #include <BLEDevice.h>
   #include <BLEServer.h>
   #include <BLEUtils.h>

Naturally, the ESP code needs to be loaded from a different window; I used the Arduino IDE, with relevant libraries installed.  

Remember, if you change the name of the name of the ESP32 at the line:
         // Create the BLE Device
         BLEDevice::init("YOUR ESP NAME HERE");
Then you must change the target name in the APP code: 
      if (scannedDevice && scannedDevice.name == 'YOUR ESP NAME HERE') {


## Good luck
I hope that if you clone this project it is successful and works right out of the box for you!  

##  Thank you
Thank you to palmmaximilian for taking the time to do the original code 
     https://github.com/palmmaximilian/ReactNativeArduinoBLE
and his Youtube post:
     https://www.youtube.com/watch?v=erWibryA_tE
and his website:
     https://www.uniquelymade.de/

     
##  Happy Coding!
