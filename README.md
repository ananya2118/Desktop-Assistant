# desktop-AI
import pyttsx3
import datetime
import speech_recognition as sr
import wikipedia
import webbrowser
import os
import smtplib
import random
#speak function
engine=pyttsx3.init('sapi5')
voices=engine.getProperty('voices')
engine.setProperty('voice',voices[0].id)                        #to set male and female voice
def speak(audio):
    engine.say(audio)
    engine.runAndWait()

def wishme():
    hour=int(datetime.datetime.now().hour)
    if(hour>=0 and hour<12):
        speak("good mormning")
    elif(hour>=12 and hour<16):
        speak("good afternoon")
    elif(hour>=16 and hour<20):
        speak("good evening")
    else:
        speak("good night")
    
    speak("hi mam iam jack.. please tell me how may i help you")
    
def takecommand():
    #it takes microphone input from user and returns string output 
    r=sr.Recognizer()
    with sr.Microphone() as source:
        print("listening ....")
        r.pause_threshold=1
        audio=r.listen(source)
        
    try:
        print("recognizing ...")
        query=r.recognize_google(audio,language='en.in')
        print(f"user said :{query}\n")
    
    except Exception as e:
        # print(e)
        print("say that again please")
        return "None"
    return query

    
if __name__=='__main__':
    
    wishme()
    while True:
        
        query=takecommand().lower()
        if "wikipedia" in query:
            speak("searching wikipedia.....")
            query=query.replace("wikipedia","")
            results = wikipedia.summary(query, sentences=2)
            speak("according to wikipedia")
            print(results)
            speak(results)
            
        elif "open youtube" in query:
            webbrowser.open("youtube.com")
            
        elif "open google" in query:
            webbrowser.open("google.com")
            
        elif "open stackoverflow" in query:
            webbrowser.open("stackoverflow.com")
            
        elif "open w3schools" in query:
            webbrowser.open("w3schools.com")
            
        elif "say a quote" in query:
            speak("dont believe anyone other than your family")
            
        elif "music" in query:
            musicdr="C:\\Users\\Ananya N\\Documents\\somgs"
            songs=os.listdir(musicdr)
            print(songs)
            i=random.randint(0,len(musicdr)-1)
            print(i)
            os.startfile(os.path.join(musicdr,songs[i]))
            
        elif "time" in query:
            ct=datetime.datetime.now().strftime('%h:%m:%s')
            speak(f"mam,the time is {ct}")
         
        elif "open code" in query:
            codepath="C:\\Users\\Ananya N\\AppData\\Local\\Programs\\Microsoft VS Code\\Code.exe"      
            os.startfile(codepath)
            
        elif "jack sendmail" in query:
            try:
                speak("what should i say")
                content=takecommand()
                to="ananyannaik3@gmail.com" 
                sendmail(to,content)
                speak("email has been sent")
            except Exception as e:
                print(e)
                speak("sorry iam unable to send email")
