# Step 1 - Python

1. Check for Python and Install if needed.
2. Open Terminal. Click Start -> type "Terminal" ![[Pasted image 20230726111646.png]]
3. Enter: 
```
py -3 -V
```
	a. If you see Python 3.8+ this is good and you can move to Step 2.
	b. If you see Python 3.7 or no results, you'll need to install python.
4. https://www.python.org/downloads/
![[Pasted image 20230726113305.png]]
5. Once downloaded, run the installer and make sure to select the full install, should be the top option with the shield, as well as select the two check boxes at the bottom of the window that says, **"Install launcher for all users (recommended)"** and **"Add Python 3.x.x to PATH"**
6. Once the installer is complete go back to the terminal window.
7. Enter:
```
py -3 -m pip -V
```

You should be returned something like:

```
pip 23.1.2 from C:\Users\jason\AppData\Local\Programs\Python\Python311\Lib\site-packages\pip (python 3.11)
```

# Step 2

DRM override settings will take some time. 

You will need to download Android Studio, https://developer.android.com/studio
- Select Download Android Studio Giraffe
This is a fairly large app so might take time. 

1. Once downloaded install with default settings and launch the studio at the end. 
2. On the welcome screen click next, then follow the standard install. 
3. Agree to all the terms on the next screen and it will begin more downloads. 
4. When you get to this window click on *More Actions*
	1. ![[Pasted image 20230726121905.png]]
	2. Click *Create Device* at the top left
	3. Select *Pixel 6
		1. Click *Next*
	4. Select **S** and click on the *download icon* next to it to download that environment. Agree to the terms and the download will begin. as the System Image and *Click Next*
	5. Click *Finish*
	6. Don't Launch the emulator right away when it's completed.
	
# Step 3
1. Before we launch the emulator, there are a few items we will need to have available.
2. Download the file "dumper" from this folder. 
3. Extract it to your downloads folder and navigate to it. 
4. Once inside right click and select *Open in Terminal*
5. Type the following in the terminal
```
pip install -r .\requirements.txt
```
6. You should be returned with something similar to this:
	1. ![[Pasted image 20230726123434.png]]
	2. Keep this window open, we will need to come back to it soon.
7. Also download this file to your computer, *frida-server-16.1.3-android-x86_64* and we will be moving it to the android device. Once downloaded, you will need to copy this to a hidden folder for android.
	1. Typical copy the file, and paste it in the platform tools folder. Change the username as needed.
		1. `C:\Users\jason\AppData\Local\Android\Sdk\platform-tools`

# Step 4
1. Let's start the emulator
	1. Click the ▶️ button.
	2. If you get a windows defender or anti-virus alert, make sure you allow the program access.
	3. This may take a while to load, but you should see a phone pop up on your screen, that looks to be in the boot process. 
	4. It's resource intensive on my computer so don't be alarmed if it takes a bit.
2. Once it looks like it's a functional phone, open Chrome and accept any prompts but don't sign in, then leave it at the home screen. 
3. Now are going to open a new terminal window and you will type the following:
```
cd C:\Users\<whatever your username is>\AppData\Local\Android\Sdk\platform-tools\
```
4. Hit Enter, be sure to replace `<whatever your username is>` with your actual username. 
	1. Mine looks like: `C:\Users\jason\AppData\Local\Android\Sdk\platform-tools\`
	2. After you move to the new directory enter the following:
```
adb.exe devices
```
*If you see an error, use the following:*
```
.\adb.exe devices
```
4. You should now see "List of devices attached"
	1. ![[Pasted image 20230726130323.png]]
5. Now we are going to copy the Frida file and turn on the server.
6. Enter the following: 
```
.\adb.exe push frida-server-16.1.3-android-x86_64 /sdcard
```
7. Then now we have to connect to start up Frida. Type the following.
```
.\adb.exe shell

su

mv /sdcard/frida-server-16.1.3-android-x86_64 /data/local/tmp

chmod +x /data/local/tmp/frida-server-16.1.3-android-x86_64

/data/local/tmp/frida-server-16.1.3-android-x86_64

```
#### Side Note -
During any one of the phases you may be disconnected from the "shell" and taken back to your regular prompt. Just pick back up.
![[Pasted image 20230726134014.png]]As you can see that happened to me here. When you reconnect you will need to do **su** again.

You'll know it's running when you are just returned to either a blank emu line or back to your terminal line after entering the final `/data/local/tmp/frida-server-16.1.3-android-x86_64` text info.

8. Once you've typed in the last line (copy and paste it in works too.) as long as you don't get an error right away, now go back over to the Dumper terminal window and type the following.
```
python dump_keys.py
```
- You'll see text start to run by on the screen. Leave this open and go back to the emulator. 
	- Looks like this:![[Pasted image 20230726142753.png]]
- Now on the emulator open this page in chrome: https://bitmovin.com/demos/drm
- You will have to type it in, you can't copy it and the auto-complete from google is incorrect.

It should look similar to this:
![[Pasted image 20230726143121.png]]


