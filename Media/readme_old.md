# Instructions for getting the crap you paid for from that app
- There seems like a lot of work involved here, but it really isn't.
- I tried to give a lot of detail to make sure you don't get stuck anywhere.

A lot of this is based off of what is here: 

1. https://of-scraper.gitbook.io/of-scraper

2. https://github.com/datawhores/OF-Scraper 
3. https://github.com/wvdumper/dumper
4. https://forum.videohelp.com/threads/408031-Dumping-Your-own-L3-CDM-with-Android-Studio?s=f22ce643aaaca3496c59a76a2a78c567
5. https://github.com/lucidyan/dumper/tree/add-android-13-support
6. https://addons.mozilla.org/en-US/firefox/addon/onlyfans/
7. https://frida.re/docs/android/ 

#### Let me know if I can help :grin:


# Step 1 - Install Python

1. Check for Python and Install if needed.

2. Open Terminal. Click Start -> type "Terminal"

    ![Alt text](<Media/Pasted image 20230726111646.png>)

3. Enter: 
    ```
    py -3 -V
    ```
    - If you see Python 3.8+ this is good and you can move to Step 2.

    - If you see Python 3.7 or no results, you'll need to install python.
4. Go to: https://www.python.org/downloads/ and download Python for Windows.

    ![Alt text](<Media/Pasted image 20230726113305.png>)

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

# Step 2 - Install Android Studio

DRM override settings will take some time. 

You will need to download Android Studio, https://developer.android.com/studio
- Select Download Android Studio Giraffe

This is a fairly large app so might take time. 

1. Once downloaded install with default settings and launch the studio at the end. 

2. On the welcome screen click next, then follow the standard install. 
3. Agree to all the terms on the next screen and it will begin more downloads. 
4. When you get to this window click on *More Actions*
	1. ![Android Studio](<Media/Pasted image 20230726121905.png>)
	2. Click *Create Device* at the top left

	3. Select *Pixel 6
		1. ![Pixel 6](<Media/Pasted image 20230726231057.png>)
		2. Click *Next*
	4. Select **Pie** and click on the *download icon* next to it to download that environment. 
		1. Agree to the terms and the download will begin. as the System Image and *Click Next*
		2. ![pie](<Media/Pasted image 20230726231206.png>)
		3. Once it's completed Downloading click *Next*
	5. Click *Show Advanced Settings* and scroll down to RAM and VRAM. **You'll need to give this about 4 to 6 GB to make this experience even remotely tolerable. Depending on how much RAM you have on your computer.**  
5. Click *Finish*

6. Don't Launch the emulator right away when it's completed.

# Step 3 - Frida & Dumper

1. Before we launch the emulator, there are a few items we will need to have available.

2. Download the zip file called [dumper-main Download](dumper-main.zip). 
3. Extract it to your downloads folder and navigate to it. 
4. Once inside right click and select *Open in Terminal*
5. Type the following in the terminal
```
pip install -r .\requirements.txt
```
6. You should be returned with something similar to this:
	1. ![Requirements](<Media/Pasted image 20230726123434.png>)
	2. Keep this window open, we will need to come back to it soon.
7. Also download this file to your computer, [Frida Download](frida-server-16.1.zip) and we will be moving it to the android device. Once downloaded, unzip it, you will need to copy this to a hidden folder for android.

	1. Typical copy the file, and paste it in the platform tools folder. Change the username as needed.
    
		1. `C:\Users\jason\AppData\Local\Android\Sdk\platform-tools`

# Step 4 - Running the Emulator

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
	1. ![Devices](<Media/Pasted image 20230726130323.png>)

5. Now we are going to copy the Frida file and turn on the server.
6. Enter the following:  <mark style="background: #FF5582A6;">(you can copy and in windows terminal/powershell just right click and it'll auto-paste)</mark>
    ```
    .\adb.exe push frida-server-16.1.3-android-x86 /sdcard
    ```
7. Then now we have to connect to start up Frida. Type the following.
    ```
    .\adb.exe shell
    su
    mv /sdcard/frida-server-16.1.3-android-x86 /data/local/tmp
    chmod +x /data/local/tmp/frida-server-16.1.3-android-x86
    /data/local/tmp/frida-server-16.1.3-android-x86
    ```

>## Side-Note
>During any one of the phases you may be disconnected from the "shell" and taken back to your regular prompt. 
>![disconnect](<Media/Pasted image 20230726134014.png>)
>
>Just reconnect and remember to you will need to **su** again. 
>Only if you haven't made it to the last line of the code.

You'll know it's running when you are just returned to either a blank emu line or back to your terminal line after entering the final `/data/local/tmp/frida-server-16.1.3-android-x86` text info.

8. Once you've typed in the last line (copy and paste it in works too.) as long as you don't get an error right away, now go back over to the Dumper terminal window and type the following.
```
python dump_keys.py
```
- You'll see text start to run by on the screen. Leave this open and go back to the emulator. 
	- Looks like this:
	- ![dump-keys](<Media/Pasted image 20230726204751.png>)

- Now on the emulator open this page in chrome: https://bitmovin.com/demos/drm
- You will have to type it in, you can't copy it and the auto-complete from google is incorrect.

Once you get the page to load, you'll click play on the video and you should also be able to see the terminal window at the same time. 
The terminal window will fill in really quick and you should see something like this:
![success](<Media/Pasted image 20230726204859.png>)

This is indicating that the keys have been saved to the dump_keys folder and we will need to save those for the only fans app.

Make a copy of these keys and rename them. The path can vary on what it creates, so you'll need to start at the dumper-main folder and start digging through dump_keys until you get to see 2 files. 

1. client_id.bin

2. private_key.pem

You will need these shortly, but first we are going to install the application for the OF Scraper itself. 
Then you'll come back to these.

# Step 5 - Setting up Auth and Config File

Download this file. https://github.com/datawhores/OF-Scraper/releases/download/de9ebfc/ofscraper_windows_de9ebfc.zip

Unzip the file to a directory that you would be happy with. 
I unzipped mine to `C:\Users\Jason\Data\ofscraper\` 

Wherever you unzip the folder to, navigate there and then open a terminal from there. Right-Click and select terminal.
- Enter the following
```
ofscraper
- or - 
.\ofscraper
```

You will then be prompted through the install process of the scraper.

## Cookie Info
### Suggested way
* If you use firefox, you can use this extension to get the necessary cookie information. You can download it here: https://addons.mozilla.org/en-US/firefox/addon/onlyfans/
	* Once installed. Sign into only fans and copy and paste the output from the add on into the terminal window when it asks for it and move onto the next Step 6

- But you can also get the information yourself using developer tools.

- **Sign into Onlyfans in your browser.**

### Manual Cookie Lookup

- This option will have you manual fill all the required information
```
{
    "auth": {
        "app-token": "",
        "sess": "",
        "auth_id": "",
        "auth_uniq_": "",
        "user_agent": "",
        "x-bc": ""
    }
}
```

- It's really not that bad. I'll show you in the next sections how to get these bits of info.

### Getting Your Auth Info
- Open DevTools, Hit F12 on your keyboard.

- Click on the network tab![Network tab](<Media/Pasted image 20230726212539.png>)
- then you can click on filter and search for id.
	- You may need to refresh Onlyfans to get the info to populate.
- You need to get the following: Explained below
	- `sess=`
	- `suth_id=`
	- `auth_uid=`
	- `User-Agent`
	- `x-bc`

>## :question: FYI
>Your `auth_uid_` will only appear if you have **2FA** (*two-factor authentication*) enabled. Also, keep in mind that your `auth_uid_` will have numbers after the final underscore and before the equal sign (that's your `auth_id`).
>Once you've copied the value for your `sess` cookie, go back to the program, paste it in, and hit enter. Now go back to your browser, copy the `auth_id` value, and paste it into the program and hit enter. Then go back to your browser, copy the `auth_uid_` value, and paste it into the program and hit enter **(leave this blank if you don't use 2FA!!!)**.
>
>Once you do that, the program will ask for your user agent. You should be able to find your user agent in a field called `User-Agent` below the `Cookie` field. 
>Copy it and paste it into the program and hit enter. After it asks for your user agent, it will ask for your `x-bc` token. You should also be able to find this in the `Request Headers` section.

# Step 6 - Additional Config File Settings

You should be able to move to the next part of the installation. 
I cannot redo it on my side so forgive me. But it should prompt you to install both of these files:

https://ffmpeg.org/download.html
https://www.bento4.com/documentation/mp4decrypt/

You can download them, extract the folders and all you need to do is copy these two files, no need to run them. 
- mp4decrypt.exe
- ffmpeg.exe

Place these in the folder that the scraper files are at, these should be created for you already in your user folder under a folder `.config` 
> ie: `C:\Users\Jason\.config\ofscraper\bin\` 

You will then need to tell the scraper where they are. But it should install these for you and place them in a similar spot as mine.

Once it's done and the configuration is complete let's close the terminal and we have to go back to the keys and set those up. You're almost done!

# Step 7 - The End!

In your keys folder, you want to take the two key files:
Make a copy of these keys and rename them. The path can vary on what it creates, so you'll need to start at the dumper-main folder and start digging through dump_keys until you get to see 2 files. 
1. client_id.bin
2. private_key.pem

And copy them to the location that has the scraper. For ease of use, I put them in the same folder as the mp4decrypt and ffmpeg files. So you can copy and paste them there and then you will rename them as follows.
- client_id.bin ➡️device_client_id_blob.bin
- private_key.pem➡️device_private_key.pem

Then you need to update your config file for the scraper so it points to the new stuff.

This should be located "`C:\Users\Jason\.config\ofscraper\config.json`"
If you cannot open it normally, right-click and do open-with notepad. Then you will update the following.

```
        "mp4decrypt": "",
        "ffmpeg": "",
        "discord": "",
        "private-key": "",
        "client-id": "",
        "key-mode-default": "auto",
        "dynamic-mode-default": "deviint",
        "partfileclean": true,
```
> ## :warning: Don't forget the extra "`\`"
> - To get the full path from, in windows, you can highlight the item and then right click and select copy as path. Then paste it between the quotes of the corresponding line.
>![copy as path](<Media/Pasted image 20230726223048.png>)
> - Be sure you add an additional back slash "`\`" to each existing "`\`" that's in the path otherwise you will get errors and the scraper will crash.
>   - For Example: "`        "private-key": "C:\\Users\\jason\\.config\\ofscraper\\bin\\device_private_key.pem",`" 
>- Update the path for the client-id, private-key, ffmpeg, and mp4decrypt

- Ensure that "`key-mode-default:`" is listed as "manual" in quotes. 
- I have my sample config file at the bottom for reference. 

- Once you are done editing. 
- Save the file and close. 
- Open terminal again. and this time type the following command: 

    ```
    ofscraper
    ```

#    You should be presented with something that looks similar to this:

![ofscraper](<Media/Pasted image 20230726223835.png>)

## CONGRATULATIONS. You should be able to download now.

1. Hit Enter on "Download content from a user"
	* Should welcome you and then give you a list of your subscriptions, current and expired. 
2. Hit Ctrl+Z to filter this list.
3. Hit Yes
4. Hit Enter
	* (I usually choose Active on this screen, since you can't download expired stuff)
5. Then decide Paid, Free, or Both. 
	* I have 1 person who is free and posts. Everyone else is paid. So I usually go to the paid stuff.
6. I leave the sort order alone so I say no then hit enter.
	* You then get a list again and now you can select who you want to download from. Use the arrows to go up and down. Pick one or many, Shift+Right Arrow will select one. 
7. Hit enter when you're ready.
8. Then it'll ask about scrape the entire paid page. Select False. 
	* First runs it'll do this anyway and it keeps track of duplicates. 
	* So no need to tell it to do it unless someone deletes their account in the middle of a subscription.
9. Then you'll get a list of items to download by post type. Basically it'll make a folder of each of these things under the username. 
	* I hit Ctrl+R and then Enter
	* But if you only want regular posts, Timeline is what you are looking for. 
	* Posts that were on a timeline that had been pinned will only fall into pinned folder.

It'll start downloading and show you progress along the way. You'll find the downloads in folders under : `C:\Users\%username%\Data\ofscraper` 
Sample of what it looks like on my side.
![success](<Media/Pasted image 20230726225515.png>)

When it's done it will ask you if you want to continue with script. Yes will allow you to reselect someone and no will close the terminal.

# My Config

This is what my config file looks like.
```
{
    "config": {
        "main_profile": "main_profile",
        "save_location": "C:\\Users\\jason\\Data\\ofscraper",
        "file_size_limit": 0,
        "dir_format": "{model_username}/{responsetype}/{mediatype}/",
        "file_format": "{filename}.{ext}",
        "textlength": "0",
        "space-replacer": " ",
        "date": "MM-DD-YYYY",
        "metadata": "{configpath}/{profile}/.data/{model_username}_{model_id}",
        "filter": [
            "Images",
            "Videos"
        ],
        "threads": "10",
        "code-execution": true,
        "custom": null,
        "mp4decrypt": "C:\\Users\\jason\\.config\\ofscraper\\bin\\mp4decrypt.exe",
        "ffmpeg": "C:\\Users\\jason\\.config\\ofscraper\\bin\\ffmpeg.exe",
        "discord": "",
        "private-key": "C:\\Users\\jason\\.config\\ofscraper\\bin\\device_private_key.pem",
        "client-id": "C:\\Users\\jason\\.config\\ofscraper\\bin\\device_client_id_blob.bin",
        "key-mode-default": "manual",
        "dynamic-mode-default": "deviint",
        "partfileclean": true,
        "responsetype": {
            "timeline": "Posts",
            "archived": "Archived",
            "pinned": "Posts",
            "message": "Messages",
            "paid": "Messages",
            "stories": "Stories",
            "highlights": "Stories",
            "profile": "Profile"
        }
    }
}
```
