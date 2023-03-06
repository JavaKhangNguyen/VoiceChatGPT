# GPT-VCC 2.0 (formerly GPT3-STTC)
# Make sure to read this document before using!
***This version is a rework based on https://github.com/Adri6336/gpt-voice-conversation-chatbot*** 

This is a bot that allows you to have a spoken conversation with ChatGPT using your microphone. If you'd prefer to type rather than speak, you can also converse with the bot via the terminal.

The tool uses a modified GPT chat preset, handles keeping track of the conversation, and uses ChatGPT's API by default. You can tell GPT something and it will remember what you said for the session and you can also have the bot develop a memory of you over time if you'd like. Despite limitations based on GPT's max token count, GPT-VCC should still be able to converse with you for as long as you'd like without losing awareness about what you've talked about. In order to use this tool, you will need a valid OpenAI API key.

The bot requires OpenAI's moderation and GPT APIs to be working properly without too much latency. You can find the status here: **https://status.openai.com/**

The releases are stable, as far as previous testing goes, but will not have all of the newest features. If you would like to have all the features as listed here, clone the repository and run 'git pull' every now and then. This will get you the newest features and bug fixes as they come, but it could be unstable. 



![_image_](https://github.com/JavaKhangNguyen/VoiceChatGPT/blob/main/bot.jpeg)


# Installing

Make sure that Python is installed in your computer and you have an OpenAI account

**In case this document is skipped, a README file which is included in your installation directory will pop up after installation, to ensure that the instructions are properly read before using this application.**

Create your OpenAI account here (if you have yet to own one): **https://platform.openai.com/signup**

1. Get OpenAI API key here (you will need to own an account to get it): **https://platform.openai.com/account/api-keys**

2. Get Python (if have yet to be installed): **https://www.python.org/ftp/python/3.11.2/python-3.11.2-amd64.exe**

3. Open the ***keys.txt*** file, at the label OpenAI_Key, replacing *[your_OpenAI key_here]* with your OpenAI key. 

*Optional: By default, this application use the Google Text To Speech API to detect your voice and processing the speech. This application also have ElevenLab Text To Speech API service available. To enable this service, add your ElevenLab API key to the ***keys.txt*** *file, just like how the OpenAI key is inserted*

4. Follow the steps listed in Using GPT-VCC


### Windows

***For Developers ONLY***

1. Download this repo by git cloning the repo, or pressing the code button towards the upper right and pressing "Download ZIP".

2. Extract contents, then move into folder with the files.

3. If you have Windows Terminal installed, right click the empty part of the folder and select 'Open in Terminal'. Otherwise, use Win + R and enter cmd. Once you're in a terminal window and at the proper directory, use "pip install -r requirements.txt". If this is done successfully, you should be ready to go.



***For Windows End-users***

Just download the installer from this link: ***https://github.com/JavaKhangNguyen/VoiceChatGPT/raw/main/ChatGPT.exe*** then follow the instructions in the **Installing** section to install and find the guide lines for this application at **Using GPT-VCC** section til the end of this document.



### Linux (Debian / Ubuntu based)

1. Install pip3

        sudo apt install python3-pip
        
2. Download this repo by git cloning the repo, or pressing the code button towards the upper right and pressing "Download ZIP".

3. Extract files, move into directory, open requirements.txt, and delete pyaudio==0.2.13 from file. Make it look like it was never there, preserving the original formatting.

4. Download pyaudio with apt as follows:

        sudo apt install python3-pyaudio
        
5. Download espeak with apt as follows (needed for interface communication):

        sudo apt install espeak
        
6. Download other requirements with pip as follows:

        pip3 install -r requirements.txt
        
7. Follow the steps listed in Using GPT-VCC


# Using GPT-VCC

***For Developers ONLY***

To use this chatbot, enter the following command once you've navigated to the bot's folder

    python main.py

***For Windows End-users***

After running the installer file, two shortcuts will appear on your desktop as ChatGPT (voice) & ChatGPT (text). Run ChatGPT (voice) to voice chat with ChatGPT or ChatGPT (text) to chat in text messages with ChatGPT using Windows Terminal/Command Prompt.


A Pygame GUI will pop up; you will see a cute robot. This shows that the bot is ready for using, but it has yet to listen to you. Follow the instructions on the screen, press SPACE on your keyboard to make it listen to you.

As the display shows Listening, that means you can talk freeky, and your speech will be recorded converted to text, then fed to GPT if it is in compliance with OpenAI's policies. When GPT is ready to reply, the screen will display *"ChatGPT is answering your question..."*.


# Content Moderation

The moderation uses both OpenAI's moderation tool and NLTK. Combined, they hope to prevent the use of GPT that is outside of OpenAI's useage policy. This is not an infaliable method though, so please exercise caution with what you give GPT.

Please note that outages or latency problems with the moderation api will prevent you from using this chatbot. If you must talk with the bot while OpenAI is having issues, please edit the chatbot.py file to exclude the "not self.flagged_by_openai(text)" condition. I do not recommend this though.


# Controls

#### Keyboard

- **SPACEBAR**: This starts a recording. Whatever you say will be then transcribed and sent to GPT (if it passes filters).

- **ESCAPE**: This exits without memorizing.

- **Q**: This quits and has bot remember details about you and your conversations (data is saved in the text file called memories.txt)

- **P**: This attempts to cancel a request to GPT. It will either prevent transcribing of message or will avoid sending it to GPT.

#### Voice Commands (All work with CLI version too except for the robot-speaking commands)

- **Say 'please set tokens to #'**: When the bot recognizes this phrase, it will try to set the max_tokens of the reply to the value you specified.

- **Say 'speak like a robot'**: This will set all responses from GPT to be spoken with a robotic TTS program that works offline.

- **Say 'stop speaking like a robot'**: This will revert bot's TTS to whatever you had before (either Google or ElevenLabs TTS).

- **Say 'please display conversation'**: This will output your entire conversation to the terminal window.

- **Say 'please display memories'**: This will provide an output of all memories saved into long term storage.

- **Say 'please restore memory'**: This will attempt to repair the working memory of the bot by consolidating a certain number of memories from the long term storage .

- **Say 'please set preset to'**: This will set the preset (a text string given to AI at start of every conversation) for the bot. For example, the preset 'speak like a pirate' makes AI speak like a pirate.

- **Say 'please reset preset'**: This will delete the preset you made.

- **Say 'please set name to'**: This will set the name of the bot to whatever you specify, so long as it is in accordance with OpenAI's usage policies. After setting name, the bot will refer to itself by the name you set.


# Features

- Have a personalized conversation with ChatGPT (Vietnamese language is possible)

- Hear GPT talk to you with Google's TTS tool (will pronounce accents accurately if it can), in ElevenLab's life-like TTS (if you have a valid api key), or as a robot (say "speak like a robot" to activate)

- Speak with GPT outloud using Google's speech recognition tech  

- Bot will remember things about you if you close the application with the 'Q' key

- See text GPT's replies as text in the terminal window. Most UTF-32 characters (like Chinese and Arabic text) will also be printed

- Automatically save conversations to a file on your disk to help you keep track of what you've talked about 

- Save a custom preset to have an experience better suited for you and your needs

- Customize the bot's name

- Chat with GPT via the terminal (Windows and Linux)

Copyright (c) 2023, Nguyen Phuc Khang. All rights reserved
