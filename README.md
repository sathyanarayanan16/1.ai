import pyttsx3
import speech_recognition as sr

# Initialize the speech recognition and text-to-speech engines
r = sr.Recognizer()
engine = pyttsx3.init()

def speak(text):
    engine.say(text)
    engine.runAndWait()

def listen():
    with sr.Microphone() as source:
        print("Listening...")
        audio = r.listen(source)
        try:
            user_input = r.recognize_google(audio)
            print("You said: " + user_input)
            return user_input
        except sr.UnknownValueError:
            print("Sorry, I didn't catch that.")
            return ""
        except sr.RequestError:
            print("Sorry, there was an issue with the speech recognition service.")
            return ""

def virtual_assistant():
    speak("Hello! How can I assist you today?")
    while True:
        user_input = listen().lower()
        
        if "hello" in user_input:
            speak("Hello! How can I assist you?")
        elif "what's your name" in user_input:
            speak("I'm your virtual assistant.")
        elif "goodbye" in user_input:
            speak("Goodbye! Have a great day.")
            break
        else:
            speak("I'm sorry, I don't understand. Please try again.")

if __name__ == "__main__":
    virtual_assistant()
