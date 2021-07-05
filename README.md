# personal-computer-assistant

import pyttsx3
import speech_recognition as sr
import datetime
import wikipedia as googleScrap
import webbrowser as web
import os
import smtplib
import pyaudio
import pywhatkit as kit
import cv2
import random
import requests 
import pywhatkit as kit
import sys
import PyPDF2
from gtts import gTTS
from playsound import playsound
from googletrans import Translator
import pytz
import pyautogui as pg 
import keyboard
from PyDictionary import PyDictionary as Dict
import pyjokes
import wolframalpha
import speedtest
import bot
import json
import urlopen
import snake
#import qrscan
import time
import instaloader


app = wolframalpha.Client("4YU88Q-J4JKY26355")

print("Initializing Robo")
MASTER = "Navneetu"

engine = pyttsx3.init('sapi5')
voices = engine.getProperty('voices')
engine.setProperty('voice',voices[0].id)
engine.setProperty('rate',170)

#speech to text
def speak(audio):
    print(" ")
    engine.say(audio)
    print(f":{audio}")
    print(" ")
    engine.runAndWait()
os.startfile("C:\\Users\\KIIT\\Desktop\\roboui\\Robo1gui.py") #for gui of computer assistant views
speak("Hello !I am your personal assistance Robo")
    

# voice to text
def TakeCommand():
    r = sr.Recognizer()
    with sr.Microphone() as source:
      print("Listening...")
      audio = r.listen(source)
      
    try :
       print("Recognising...")
       query = r.recognize_google(audio,language = 'en-in')
       print(f"user said: {query}\n")
      
    except Exception as e:
        speak("sorry! i didn't catch your voice")
        
      
    return query

def TakeHindi():
      command = sr.Recognizer()
      with sr.Microphone() as source:
         print("Listening...")
         command.pause_threshold = 1
         audio = command.listen(source)
      
      try :
          print("Recognising...")
          query = command.recognize_google(audio,language ='hi')
          print(f"user said: {query}")

      
      except Exception as e:
          return "none"
        
      
      return query.lower()


def Tran():
      speak("Tell me the line!")
      line = TakeHindi()
      traslate = Translator()
      result = traslate.translate(line)
      Text = result.text                      
      speak(Text)





def wishMe(): # This function will wish you as per current time
    hour = int(datetime.datetime.now().hour)
    print(hour)

    if hour>=0 and hour< 12:
        speak("Good Morning ,Enjoy your day" )

    elif hour>=12 and hour<18:
        speak("Good Afternoon,Enjoy your day" )

    elif hour>=18 and hour<20:
        speak("Good Evening, Enjoy your day" )
    else:
     speak("Good night" )
    speak("How may i help you!")

def sendEmail(to,content):
  server = smtplip.SMTP('smtp.gmail.com',587)
  server.ehlo()
  server.starttls()
  server.login('abcd@gmail.com','abc1598**') #your mail-id and password
  server.sendmail('kumari@gmail.com',to,content) # sender mail-id
  server.close()

def notepad():
    speak("what should i have to write")
    speak("ok i am ready to write")

    writes = TakeCommand().lower()

    time =  datetime.datetime.now().strftime("%H:%M")

    filename = str(time).replace(":",".") + "-note.txt"

    with open(filename,"w") as file:
        
        file.write(writes)
        
    path = "C:\\automation\\" + str(filename)
    os.startfile(path)
    
def notepad_write():
  speak("what should i have to write")
  speak("ok i am ready to write")
  writes = TakeCommand().lower()

  pg.typewrite('Notepad.exe', writes)


def YoutubeAuto():
    speak("whats your task!")
    comm = TakeCommand().lower()

    if 'pause' in comm:
        keyboard.press('space bar')

    elif 'restart' in comm:
        keyboard.press('0')

    elif 'mute' in comm:
         keyboard.press('m')

    elif 'skip' in comm:
         keyboard.press('l')


    elif 'back' in comm:
         keyboard.press('j')


    elif 'full screen' in comm:
        keyboard.press('f')

    elif 'film mode' in comm:
        keyboard.press('t')

    speak("Done")
          
def Chromeauto():
    speak("chrome Auto mode!")

    comm = TakeCommand().lower()

    if 'close tab' in comm:
        pg.press('ctrl + w')

    elif 'open tab' in comm:
        pg.press('ctrl + t')

    elif 'open new tab' in comm:
        pg.press('ctrl + n')

    elif 'open history' in comm:
        pg.press('ctrl + h')

    
    elif 'display download window' in comm:
        pg.press('ctrl + j')

    elif 'close window' in comm:
         pg.press('ctrl + shift +w')
         
    speak("Done!")


def Jokes():
    my_joke = pyjokes.get_joke('en',category='neutral')
    print(my_joke)
    speak(my_joke)

def news():
      main_url = 'https://newsapi.org/v2/top-headlines?country=us&category=business&apiKey=bfdd5aabfa834a188369228214b0e35f'

      main_page = requests.get(main_url).json()
      articles = main_page["articles"]
      head = []
      day=["first","second","third","fourth","fifth","sixth","seventh","eight","nine","tenth"]
      for ar in articles:
          head.append(ar["title"])
      for i in range(len(day)):
          speak(f"today{day[i]} news is: {head[i]}")
    
             

def SpeedTest():
     speak("checking speed of internet")
     speak("Tell me the  name to know which speed you wants to know like downloading,uploading or internetspeed")
     speed = TakeCommand().lower()
     st = speedtest.Speedtest()
     dl = st.download()
     correctDown = int(dl/800000)
     up = st.upload()
     correctUpload = int(up/80000)

     if 'uploading speed' in speed:
           speak(f"The uploading speed is{correctUpload} mbp s")

     elif 'downloading speed' in speed:
           speak(f"The downloading speed is{correctDown} mbp s")

     else:
          speak(f"The Downloading is {correctDown} and Uploading speed is {correctUpload} mbp s")
        



def Whatsapp():
     speak("Tell me the name of person!")
     name = TakeCommand().lower()
     
     if 'Navneet' in name:
        speak("Tell me message")
        msg= TakeCommand().lower()
        speak("Tell me the time please!")
        speak("Time in Hour!")
        hour = int(TakeCommand().lower())
        speak=("Time in Minutes!")
        min = int(TakeCommand().lower())
        kit.sendwhatmsg("+9187666666",msg,hour,min,20)
        speak("Ok,sending Whatsapp Message!")

     else:
        speak("Tell me phone number!")
        phone = int(TakeCommand().lower())
        ph = '+91' + phone
        speak("Tell me the message!")
        msg = TakeCommand().lower()
        speak("Time in Hour!")
        hour = int(TakeCommand().lower())
        speak=("Time in Minutes!")
        min = int(TakeCommand().lower())
        kit.sendwhatmsg(ph,msg,hour,min,20)
        speak("Ok,sending Whatsapp Message !")
        
        

def playMusic():
    speak("Tell me the name of song!")
    song = TakeCommand().lower()
    
    if 'Darshan raval' in  song:
          #os.startfile('C:\\music\\Gulaboo.mp3')
            kit.playonyt(song)

    elif 'badshah song' in song:
          #os.startfile('C:\\music\\Dabangg.mp3')
            kit.playonyt(song)

    elif 'sad song' in song:
           #os.startfile('C:\\music\\Dabangg.mp3')
            kit.playonyt(song)

    elif 'party song' in song:
           #os.startfile('C:\\music\\Dabangg.mp3')
            kit.playonyt(song)
           
    else:
           kit.playonyt(song)
    speak("your song play! Enjoy your song")






def screenshot():
    img = pyautogui.screenshot()
    img.save("C:\\screenshot\\robo.png")
    speak("I take screenshot!")



def Dict():
    speak("Tell me your equation!")
    prob = TakeCommand().lower()

    if 'meaning' in prob:
        prob = prob.replace("what is the", "")
        prob = prob.replace("robo","")
        prob = prob.replace("meaning of", "")
        result = Dict.meaning(prob)
        speak(f"The Meaning For {prob} is {result}")
        
    elif 'synonym' in prob:
        prob = prob.replace("what is the", "")
        prob = prob.replace("robo","")
        prob = prob.replace("synonym of", "")
        result = Dict.synonym(prob)
        speak(f"The Synonym  For {prob} is {result}")


    elif 'antonym' in prob:
        prob = prob.replace("what is the", "")
        prob = prob.replace("robo","")
        prob = prob.replace("antonym of", "")
        result = Dict.synonym(prob)
        speak(f"The Antonym  For {prob} is {result}")
        
def Pdf_reader():
    book = open('C:\\Users\\KIIT\\Desktop\\java book.pdf','rb')
    pdfReader = PyPDF2.PdfFileReader(book) #pip install PyPDF2
    pages = pdfReader.getNumPages()
    speak(f"Total number of pages in  this books {pages} ")
    speak("Enter page number i have to read")
    pg = int(input("please enter the page number: "))
    page = pdfReader.getPage(pg)
    text = page.extractText()
    speak(text)

def date():
    t_date = datetime.datetime.now(tz=pytz.timezone('Asia/Calcutta'))
    speak(t_date.strftime('%d %B,of %Y'))
    
def openapp():
      speak("Ok sir ,tell me the name of app!")
      app = TakeCommand().lower()

      if 'open map' in app:
            web.open('https://www.google.com/maps/@26.5918137,85.4834772,14z')

      elif 'open whatsapp' in app:
            os.startfile("C:\\Users\KIIT\\AppData\\Local\\WhatsApp\\WhatsApp.exe")
        
      elif 'open chrome' in app:
           os.startfile("C:\\Program Files\\Google\\Chrome\\Application\\chrome.exe")
        
      elif 'open facebook' in  app:
            web.open('https://www.facebook.com/')

      elif 'open instagram' in app:
            web.open('https://www.instagram.com/')

      elif 'open code' in app:
            os.startfile("C:\\Program Files (x86)\\Dev-Cpp\\devcpp.exe")


      elif 'open notepad' in query:
           npath = "C:\\Windows\\System32\\notepad.exe"
           os.startfile(npath)
           

      elif 'open youtube' in app:
         web.open('https://www.youtube.com')
      speak("Done")
    
def closeapp():
      speak("Ok ,wait a second ,tell me name of app!")
      app = TakeCommand().lower()
      

      if 'close youtube' in app:
          os.system("TASKKILL  /F /im chrome.exe")

      elif 'close chrome' in app:
          os.system("TASKKILL /F /im  chrome.exe")

      elif 'close code' in app:
          os.system("TASKKILL /F /im  devcpp.exe")

      elif 'close facebook' in app:
          os.system("TASKKILL /F /im  chrome.exe")


      elif 'close instagram' in app:
          os.system("TASKKILL /F /im  chrome.exe")



      elif 'close instagram' in app:
          os.system("TASKKILL /F /im  notepad.exe")
    

      elif 'close map' in app:
          os.system("TASKKILL /F /im  chrome.exe")


      elif 'close whatsapp' in  app:
          os.system("TASKKILL /F /im  WhatsApp.exe ")
        
      speak("Your program is successfully close")
      
       
      
def TaskExecution():
    #speak("hello ")
    wishMe()
    
    #Reader()
    while True:
        query = TakeCommand().lower()
        #logic for perform task
        if "write on notepad" in query:
             notepad_write()
             
            
        elif "open command prompt" in query:
            os.system("start cmd")

        elif "what is time" in query:
            strTime= datetime.datetime.now().strftime("%H:%M:%S")
            speak(f"the time is{strTime}")
            print(strTime)


        elif "today date" in query:
             date()
             
        elif "open calculator" in query:
            os.system("start calculator")


        elif 'call ruby' in query: # here i add address of another CA to call inside  this code
               speak("ok")

               while True:
                    permission = TakeCommand().lower()
                    if 'call ruby' in permission:
                        path = ("C:\\Users\\KIIT\Desktop\\Bixby.py")
                        os.system(path)
                        speak("Thanks for call me ,have a good day , what can i do for you")

                    elif 'sleep ruby' in query or 'you can go' in query:
                         speak("Thank you ,have a good day and see you later!")
                         sys.exit

              

        elif 'open app' in query:
               openapp()

        elif 'close app' in query:
                closeapp()


        elif "read pdf" in query:
               Pdf_reader()

        elif "screenshot" in query:
               screenshot()
            
        elif "open code" in query:
            path = ("C:\\Program Files (x86)\\Dev-Cpp\\devcpp.exe")
            os.startfile(npath)

        elif 'Tell me joke' in query or 'joke' in query:
               Jokes()

        elif "open camera" in query:
            cap = cv2.VideoCapture(0)
            while True:
                ret,img = cap.read()
                cv2.imshow('webcam',img)
                k = cv2.waitKey(50)
                if k==27:
                    break;
            cap.release()
            cv2.destroAllWindows()

        elif "play music" in query:
             music ='C:\music'
             songs = os.listdir(music)
             rd = random.choice(songs)
             os.startfile(os.path.join(music,rd))

        elif "ip address" in query:
            ip = get('https://api.ipify.org').text
            speak(f"Your IP address is {ip}")
            print(ip)

        elif 'set alarm' in query:
            speak("Enter the time !")
            time = input(": Enter the time :")

            while True:
                Time_du = datetime.datetime.now()
                now = Time_du.strftime("%H:%M:%S")

                if now == time:
                    speak("Time to wake up! time to wake up dear wake up its")
                    playsound("C:\\Users\\KIIT\\Desktop\\morning song.mp3")
                    speak("Alarm closed")
                    print("Alarm closed")

                elif now>time:
                   break

        elif 'open map' in query:
            web.open('https://www.google.com/maps/@26.5918137,85.4834772,14z')

        elif  'close music' in  query:
            os.startfile("TASKKILL /F /im  music.exe")

        elif "whatsapp message" in query:
            #kit.sendwhatmsg("+9187677777754","This is testing protocol",12,21)
              Whatsapp()

        elif "play song on youtube" in query:
             cm = TakeCommand().lower()
             kit.playonyt(f"{cm}")



        elif 'play song' in query or 'song' in query:
                playMusic() 
        

             
        elif "email to mannu" in query:
             try:
                 speak("What should i say?")
                 content = TakeCommand().lower()
                 to ="kumarinavneetu@gmail.com"
                 sendEmail(to,content)
                 speak("Email has been sent")

             except Exception as e:
                print(e)
                speak("Sorry, i am not able to sent mail")
                  

       
        elif 'talk' in query or 'talk with me' in query:
               speak("why not!")
               result=bot.firstChatBot()  #typing bot
               speak(result)

               
            
        elif "thank you" in query or "thanks" in query:
            speak("its my pleasure")

        elif "you can sleep" in query or "sleep now" in query:
            speak("ok,You can call me anytime")
            break
            

        elif 'wikipedia' in query.lower():
          speak('Searching wikipedia...')
          query = query.replace("wikipedia", "")
          results = wikipedia.summary(query,sentences =2)
          speak(results)
          print(results)

        elif "open youtube" in query:
             result = 'https://www.youtube.com/results?search_query=' + query
             web.open(result)
             speak('This is what I found for Your search.')
             pywhatkit.playonyt(query)
             speak("This May Help you.")
           # speak("What should I search on Youtube")
             speak("What should i search on Youtube")
             cm = TakeCommand().lower()
             web.open(f" {cm}")
            
            
        elif "search" in query:
             query = query.replace("rabo", "")
             query = query.replace("search","")
             speak("This is what i found on the web!")
             kit.search(query)

             try:
                 result = googleScrap.summary(query,3)
                 speak(result)

             except:
                 speak("No search data available")


  #open operation                   
        elif "whatsapp message" in query:
            #kit.sendwhatmsg("+91000012348","This is testing protocol",12,21)
              Whatsapp()

        elif "play song on youtube" in query:
             cm = TakeCommand().lower()
             kit.playonyt(f"{cm}")

             
        elif "email to mannu" in query:
             try:
                 speak("What should i say?")
                 content = TakeCommand().lower()
                 to ="abcdfg@gmail.com"
                 sendEmail(to,content)
                 speak("Email has been sent")

             except Exception as e:
                print(e)
                speak("Sorry, i am not able to sent mail")



        elif 'pause' in query:
            keyboard.press('space bar')
 

        elif 'restart' in query:
              keyboard.press('0')
 

        elif 'mute' in query:
            keyboard.press('m')


        elif 'skip' in query:
             keyboard.press('l')

        elif 'open adobe reader' in query or 'pdf' in query:
            os.startfile("C:\\Program Files (x86)\\Adobe\\Acrobat Reader DC\\Reader\\AcroRd32.exe")

        elif 'back' in query:
              keyboard.press('j')



        elif 'full screen' in query:
               keyboard.press('f')


        elif 'film mode' in query:
               keyboard.press('t')


        elif 'volume up' in query:
               pg.press('volumeup')

        elif 'volume down' in query:
               pg.press('volumedown')

        elif 'volume mute' in query:
               pg.press('volumemute')

               
        elif 'youtubeauto' in query:
               YoutubeAuto()

        elif 'close tab' in  query:
             pg.press('ctrl + w')

        elif 'open tab' in query:
              pg.press('ctrl + t')

        elif 'open new tab' in query:
              pg.press('ctrl + n')

        elif 'open history' in query:
              pg.press('ctrl + h')

    
        elif 'display download window' in query:
              pg.press('ctrl+j')

        elif 'close window' in  query:
             pg.press('ctrl + shift +w')


        elif 'chromeauto' in query:
              Chromeauto()
        elif 'open dictionary' in query:          
                Dict()
             
        elif "hello" in query or "hey" in query:
             speak("Hello,may i help you with something")
             
        elif "how are you" in query or 'whats up' in query:
            speak("I am fine,what about you")
            
        elif "good" in query or "fine" in query:
            speak("that's great to hear from you")
            
        elif'who are you'in query or 'tell me about yourself'in query or 'about you' in query:
            speak("I am Robo a computer based an AI program ! i am like your friends i try to help and solve your problem and Query always")



        elif 'who created you' in query or 'developed' in query:
            speak("I was created by Navneetu on 1st june 2021 but we all are created by god")
            
        elif "thank you" in query or "thanks" in query:
            speak("its my pleasure")

        elif 'repeat my word' in query:
            speak("say what you want to say!")
            ss = TakeCommand().lower()
            speak(f"you said : {ss}")
       
        elif 'weather' in query or 'today climate' in query :
            speak("Tell me name of place!")
            place = TakeCommand().lower()
            res = app.query(place)
            speak(next(res.results).text)
            print(next(res.results).text)

        elif 'calculate' in query:
            speak("What should i task perform?")
            term = TakeCommand().lower()
            term = term.replace("Multiply", "*")
            term = term.replace("plus" ,"+")
            term = term.replace("Substract","-")
            term = term.replace("Divide","/")
            res = app.query(term)
            speak(next(res.results).text)


       
        elif 'open paint' in query:
             os.startfile('mspaint.exe')
            
                
        elif 'downloading speed' in query:
                SpeedTest()


        elif 'uploading speed' in query:
                SpeedTest()


        elif 'internet speed' in query:
                SpeedTest()


        elif 'open documents'in query or 'documents' in query:
             os.startfile('C:\\Users\\KIIT\\Documents')

        elif 'switch to window' in query or 'switch desktop' in query:
               pg.keyDown("alt")
               pg.press("tab")
               time.sleep(1)
               pg.keyUp("alt")

        elif 'instagram profile' in query or 'profile on instagram' in query:
             speak("please enter the user name correctly")
             name = input("Enter username here:")
             web.open("www.instagram.com/{name}")
             speak("here is the profile of user{name}")
             time.sleep(5)
             speak("would you like to install profile picture of this account.")
             condition = TakeCommand().lower()
             if 'yes' in condition:
                 mod = instaloader.Instaloader()
                 mod.download_profile(name,profile_pic_only=True)
            
              
        elif 'hide  files' in query or 'hide this folder' in query or 'visible for everyone' in query:
               speak("tell me you want to hide this folder or make it visible for everyone")
               condition = TakeCommand().lower()
               if 'hide' in condition:
                   os.system("C:\Robo +h /s /d")
                   speak("All files of this folder is hide")
               elif 'visible' in condition:
                   os.system("C:\Robo  -h /s /d")
                   speak("All files in this folder is now visible")
                   
               elif "leave it" in condition or 'leave for now' in condition:
                    speak("ok")
                     

        elif 'translator' in query or 'translate' in query:
                Tran()

        #elif 'qrscan' in query:
            #qrscan.scan()

        elif 'news' in query or 'today news' in query:
            speak("wait for few minutes")
            news()


        elif 'game' in query:
             speak("ok")
             result=snake.game()
             speak(result)


        elif 'shutdown' in query or 'switchoff' in query:
              os.system("shutdown /s /t S")

        elif 'restart' in query:
            os.system("shutdown /r /t S")
             
        elif "you can go" in query or 'you need a break' in query:
             os.system("TASKKILL /F /im  Rainmeter.exe")
             break

        elif "exit" in query:
              quit()

        else:
            speak("try again")

       
            
            
        
             
        #speak("Do you have any other work")'''
#app = wolframalpha.Client("4YU88Q-J4JKY26355")              
if __name__ =="__main__":


    while True:
          permission = TakeCommand().lower()
          if "hello" in permission or "ok robo" in  permission:
              TaskExecution()
          elif "goodbye" in permission  or "bye" in permission:
             speak("Thanks for use me ,have a good day")
             sys.exit()
              

      
            
             
