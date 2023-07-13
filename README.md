# GUI-with-Virtual-Assistant-using-python

#Modules used in this project

import speech_recognition as srt

import pyttsx3

import pywhatkit

import time

from time import ctime

import webbrowser

import playsound

import os

import random

from gtts import gTTS

from tkinter import *

from PIL import ImageTk, Image

import wikipedia

import datetime

import pyjokes


# Voice Recognizer
print('Say something...')

r = srt.Recognizer()

speaker = pyttsx3.init()

# Microphone access

def record_audio(ask=False):

    with srt.Microphone() as source:
    
        if ask:
        
            lee_voice(ask)
            
        audio = r.listen(source)
        
        voice_data = ''
        
# Exception Handling        
        try:
            voice_data = r.recognize_google(audio)
            print('Recognizer voice :' + voice_data)
        except Exception:
            #print('Oops something went Wrong')
            lee_voice('Oops something went Wrong')
        return voice_data
def lee_voice(audio_string):
    # Play audio text to voice
    tts = gTTS(text=audio_string, lang='en')
    r = random.randint(1, 10000000)
    audio_file = 'audio-' + str(r) + '.mp3'
    tts.save(audio_file)
    playsound.playsound(audio_file)
    print(audio_string)
    os.remove(audio_file)

# GUI of Virtual Assistant
class Widget:
  
    def _init_(self):
        root = Tk()
        root.title('PSPK')
        root.geometry('520x320')

        img = ImageTk.PhotoImage(Image.open(r'C:\Users\rayap\OneDrive\Desktop\minion.jpg'))
        panel = Label(root, image=img)
        panel.pack(side='left', fill='both', expand='no')

        userText = StringVar()
        userText.set('$Virtual Assistant')
        userFrame = LabelFrame(root, text='PSPK', font=('Railways', 24, 'bold'))
        userFrame.pack(fill='both', expand='yes')
        top = Message(userFrame, textvariable=userText, bg='black', fg='white')
        top.config(font=("Century Gothic", 35, 'bold'))
        top.pack(side='top', fill='both', expand='yes')

        btn = Button(root, text='Speak', font=('railways', 20, 'bold'), bg='red', fg='white', command=self.clicked).pack(fill='x', expand='no')
        btn2 = Button(root, text='Close', font=('railways', 20, 'bold'), bg='yellow', fg='black' ,command=root.destroy).pack(fill='x', expand='no')

        lee_voice('hai ,How can i help you...?')
        root.mainloop()
        
# BUTTON CALLING
    def clicked(self):
        

        print("working...")

        voice_data = record_audio()
        voice_data = voice_data.lower()

        if 'who are you' in voice_data:
            lee_voice('I am your Virtual Assitant,Pulamma ')

        elif 'search' in voice_data:
            search = record_audio("What do you want to search for...?")
            url = 'https://google.com/search?q=' + search
            webbrowser.get().open(url)
            lee_voice('this is what i found' + search)

        elif 'find location' in voice_data:
            location = record_audio('What is your location?')
            url = 'https://google.nl/maps/place/' + location + '/&amp;'
            webbrowser.get().open(url)
            lee_voice('Here is location' + location)

        elif 'who is' in voice_data:
            person = voice_data.replace('who is', '')
            info = wikipedia.summary(person, 1)
            print(info)
            lee_voice(info)

        elif 'play' in voice_data:
            song = voice_data.replace('play', '')
            lee_voice('playing ' + song)
            pywhatkit.playonyt(song)

        elif 'joke' in voice_data:
            lee_voice(pyjokes.get_joke())

        elif 'what is the time' in voice_data:
            lee_voice("Sir the time is :" + ctime())

        elif 'open youtube' in voice_data:
            webbrowser.open_new_tab("https://www.youtube.com")
            lee_voice("youtube is open now")
            time.sleep(5)

        elif 'open google' in voice_data:
            webbrowser.open_new_tab("https://www.google.com")
            lee_voice("Google chrome is open now")
            time.sleep(5)

        elif 'open gmail' in voice_data:
            webbrowser.open_new_tab("mail.google.com")
            lee_voice("Google Mail open now")
            time.sleep(5)

        elif 'hello' or "hai" in voice_data:
            hour = datetime.datetime.now().hour

            if hour >= 0 and hour < 12:
                lee_voice("Hello,Good Morning")

            elif hour >= 12 and hour < 18:
                lee_voice("Hello,Good Afternoon")

            else:
                lee_voice("Hello,Good Evening")

        elif 'exit' in voice_data:
            lee_voice('Thanks have a good day ')
            exit()

        else:
            lee_voice("Say the command again")

def respond():

    pass
    
if __ _name_ __ == '__ _main_ __':

    widget = Widget()

time.sleep(1)

while 1:

    voice_data = record_audio()
    
    respond(voice_data)

speaker.runAndWait()
