import speech_recognition as sr
import os
from gtts import gTTS
import playsound
from time import ctime
import re
import webbrowser
import smtplib


def listen():
    r = sr.Recognizer()    ## recognize the voice using Recognizer method of sr!!
    with sr.Microphone() as source:     ## use microphone to speek
        print('i am listening...')      ## show that you are listening
        audio = r.listen(source,phrase_time_limit = 5)    ## listen for how many seconds?
    data = ''
    try:
        data = r.recognize_google(audio,language = 'en-US')  #specify language
        print('you said : ' + data)
    except sr.UnknownValueError:
        print('sorry i don\'t know other than english')
    except sr.RequestError as e:
        print('request Failed')
    finally:
        print('i did it')
    return data


def respond(string):
    
    print(string)
    
    tts = gTTS(text = string,lang = 'en')
    tts.save('speech.mp3')
    playsound.playsound('speech.mp3')
    os.remove('speech.mp3')

    
# voice assistant replying 

def voice_assistant(data):
    
    
    # how are you??
    if 'how are you' in data:
        listening = True
        respond('fine thank you')
    
    
    # what is the time??
    if 'time' in data:
        listening = True
        respond(ctime())
        
    
    # can you open google??
    
    if 'open google' in data:
        listening = True
        url = 'https://www.google.com'
        webbrowser.open(url)
        respond(done)
        
    # sending email
    
    if 'email' in data:
        
        listening = True
        
        respond('whom should i send??')
        
        to = listen()
        
        edict = {'me':'akash.malvi5@gmail.com','not_me':'akakka'}
        to_address = edict[to]
        respond('what is the subject?')
        subject = listen()
        respond('what is the matter?')
        message = listen()
        content = 'subject:{}\n\n message:{}'.format(subject,message)
        mail = smtplib.SMTP('smtp@gmail.com',587) # for gmail port no
        mail = ehlo() # communication purpose
        mail.starttls()
        mail.login('akash.malvi5@gmail.com','shivababa2036')
        mail.sendmail('akash.malvi5@gmail.com','to_addr',content)
        mail.close()
        respond('email sent')
        
    if 'wiki' in data:
        listening = True
        respond('what should i search?')
        query = listen()
        response = requests.get('https://www.wikipedia.org/wiki/'+query)
        if response is not None:
            html = bs4.BeautifulSoup(response.text,'html.parser')
            
            paragraphs = html.select('p')
            
            intro = (i.text for i in paragraph)
            
            halo = ''.join(intro)
            
            respond(halo[:200])
    
    
    if 'stop' in data:
        
        listening = False
        respond('thank you')
        

# initially what it says??

respond('hello akash , what can i do for you??')
listening  = True        


while listening == True:
    
    data = listen()
    
    listening = voice_assistant(data)


try:
    return listening
except UnboundlocalError:
    print('time out')
