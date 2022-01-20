# Read First-
- This is the Example script of how to use Python's Library JarvisAI (https://pypi.org/project/JarvisAI)
- This script is always uses the latest version of JarvisAI with latest example.
## Getting started-
1. `pip install -r requirements.txt` to install all requirements, some of the things you may need to install manually so check requirements.txt file.
If anything is failing (or giving error) then skip that package or try to install that manually by searching on Google about that package. It's not a big deal.
2. Run `main.py` file. `python main.py`
3. Installation may take time because it uses heavy libraries like Tensorflow and Pytorch with some of the deep learning models. So, if you are limited by data (bandwidth) then this is not for you. *The first time installation will take some time and lots of data.*
4. Watch *tutorial* and read *usages* for more information from below section.
## Note-
* Add proper notes, guides, **traceback**, steps and description if you want to suggest something or raise issue.
* Check already exist issues first.
## Line of Codes
import JarvisAI
import re
import pprint
import random

obj = JarvisAI.JarvisAssistant()


def t2s(text):
    obj.text2speech(text)


while True:
    res = obj.mic_input()

    if re.search('weather|temperature', res):
        city = res.split(' ')[-1]
        weather_res = obj.weather(city=city)
        print(weather_res)
        t2s(weather_res)

    if re.search('news', res):
        news_res = obj.news()
        pprint.pprint(news_res)
        t2s(f"I have found {len(news_res)} news. You can read it. Let me tell you first 2 of them")
        t2s(news_res[0])
        t2s(news_res[1])

    if re.search('tell me about', res):
        topic = res.split(' ')[-1]
        wiki_res = obj.tell_me(topic)
        print(wiki_res)
        t2s(wiki_res)

    if re.search('date', res):
        date = obj.tell_me_date()
        print(date)
        print(t2s(date))

    if re.search('time', res):
        time = obj.tell_me_time()
        print(time)
        t2s(time)

    if re.search('open', res):
        domain = res.split(' ')[-1]
        open_result = obj.website_opener(domain)
        print(open_result)

    if re.search('launch', res):
        dict_app = {
            'chrome': 'C:\Program Files (x86)\Google\Chrome\Application\chrome.exe',
            'mozzila firefox': 'C:\Program Files\Mozilla Firefox\firefox.exe'
        }

        app = res.split(' ', 1)[1]
        path = dict_app.get(app)
        if path is None:
            t2s('Application path not found')
            print('Application path not found')
        else:
            t2s('Launching: ' + app)
            obj.launch_any_app(path_of_app=path)

    if re.search('hello', res):
        print('Hi')
        t2s('Hi')

    if re.search('how are you', res):
        li = ['good', 'fine', 'great']
        response = random.choice(li)
        print(f"I am {response}")
        t2s(f"I am {response}")

    if re.search('your name|who are you', res):
        print("My name is Pushpaa, I am your personal assistant")
        t2s("My name is Pushpaa, I am your personal assistant")

    if re.search('what can you do', res):
        li_commands = {
            "open websites": "Example: 'open youtube.com",
            "time": "Example: 'what time it is?'",
            "date": "Example: 'what date it is?'",
            "launch applications": "Example: 'launch chrome'",
            "tell me": "Example: 'tell me about India'",
            "weather": "Example: 'what weather/temperature in Mumbai?'",
            "news": "Example: 'news for today' ",
        }
        ans = """I can do lots of things, for example you can ask me time, date, weather in your city,
        I can open websites for you, launch application and more. See the list of commands-"""
        print(ans)
        pprint.pprint(li_commands)
        t2s(ans)

![Screenshot (11)](https://user-images.githubusercontent.com/92096587/150343232-c64141ca-8738-4a63-b180-9a03f6354217.png)
