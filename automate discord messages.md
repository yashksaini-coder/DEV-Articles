  <img src="https://media2.dev.to/dynamic/image/width=1000,height=420,fit=cover,gravity=auto,format=auto/https%3A%2F%2Fdev-to-uploads.s3.amazonaws.com%2Fuploads%2Farticles%2Fnzzx04rxqtw82opvpdol.png" alt="Cover Image" />
  <hr />
  
  # Automate Discord Messages
  
  **Tags:** automaton, discord, opensource, python

  **Published At:** 3/29/2025, 10:40:03 AM

  **URL:** [https://dev.to/yashksaini/automate-discord-messages-30ip](https://dev.to/yashksaini/automate-discord-messages-30ip)

  <hr />
  Hi 👋 **DEVs**, in order to get my perspective and objectives of why I did this project and How I built this weekend project, let me first tell you about myself.

{% embed https://github.com/yashksaini-coder %}

I'm a person who is passionate for building things my way like with retro, simple, and one that can allow me to skip or automate basic tasks. I started my Open Source journey over 3 years ago, At first I struggled with the basic commits, issues and PR stuff. However I loved the idea of all the open source projects, ideas, projects widely available for learn and use. 

I discovered Discord and there I joined many communities where i met and interacted with many Developers, each working on some project either their own or someone's else. 
 
![Discord platform](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vt84b4bjlk83qscw0ri6.png)

---

## ✨ Why I Built this project ?

Now, recently I was introduced to fun gaming bot widely famous and known as [OWO](https://owobot.com/) where users can hunt, battle, gamble, complete quests and build their team to battle with among players. The main idea is to hunt and gather _resources_ & _animals_  to build and strengthen your team. Complete _quests_ & _gamble_ 

But as I am lazy I wasn't motivated enough to do this manually by typing. There I thought of why not automate this by using a python program to locally run a bot and write messages on certain channel using their ID. Then I started researching on web, how to use discord API and send messages through it with proper authorized token. 

I wanted to send more than one message with proper intervals so that my activity wouldn't be flagged as suspicious or malicious bot. So came up with the idea to set a custom **_minimum_** & **_maximum_** intervals of each message. Instead of using hard coded in lines, Generally I used to approach of using simple JSON (JavaScript Object Notation) implementation, for setting up user_tokem, channel_ID and messages. 

```json
{
  "Config": [
    {
      "token": "your_token_here",
      "channel_id": "your_channel_id_here",
      "messages": [
        {
          "content": "Hello, this is a test message!",
          "min_interval": 5,
          "max_interval": 10
        },
        {
          "content": "This is another message.",
          "min_interval": 10,
          "max_interval": 15
        }
      ]
    }
  ]
}
```
---

## 😉 How I built this project ?

I built this project during the weekend and I wanted to make it feel like a simple Retro Terminal tools like [bagels](https://github.com/EnhancedJax/Bagels), [btop](https://github.com/aristocratos/btop) I wrote the code to use rich and colorama to higlight the texts with proper color palette. Then later on decided to use Looping to send messages using Discord API with POST request. 

Oh! Almost forgot to mention this. Recently I started building all my general projects of Python using,  

##[UV](https://docs.astral.sh/uv)

![UV](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/unghonbfh5fohpdr0wrc.png)

It's nn extremely fast package and project manager, written in Rust. Much better to use and better then all the other alternative tools `pip`, `pip-tools`, `pipx`, `poetry`, `pyenv`, `twine`, `virtualenv`,

And for the program to feel more like a Terminal tool I used 

- [Rich](https://github.com/Textualize/rich)
![Rich](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5wwilra4z8d9kv1w3zjd.png)

- [Typer](https://typer.tiangolo.com/)
![Typer](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6giqlscof7ohh5p5688p.png)

---


### ⚡Key Features

- **Automated Message Sending:** The bot sends messages to a specified Discord channel at random intervals within a defined range.

- **User-Friendly CLI Interface:** Uses [Typer](https://typer.tiangolo.com/) and [Rich](https://github.com/Textualize/rich) for an interactive and visually appealing command-line experience.

- **JSON-Based Configuration:** Stores user settings, including the Discord bot token, channel ID, and message configurations.

- **Multi-Threaded Execution:** Each message runs in its own thread, ensuring asynchronous delivery without delays.

- **Graceful Shutdown Handling:** Supports interruption via `Ctrl+C` while safely stopping all active threads.

- **Logging & Error Handling:** Implements structured logging using `rich.logging` and handles errors gracefully.

## ✨ *Workflow Overview*

The proper workflow that the script follows to allow users to automate messages can be visualized as follows:-

![Workflow](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/r6d9s6sx1f0st2yyqym0.png)

#### **1. Configuration Setup**  
- On the first run, the script checks for `config.json`.  
- If missing, it prompts the user to enter:  
  - Discord bot token  
  - Channel ID  
- Saves this data in `config.json`.  

#### **2. Adding Messages**  
- Users can add messages to be sent at specific intervals.  
- Each message includes:  
  - Message content  
  - Minimum and maximum interval (in seconds)  
- Messages are stored in `config.json`.  

#### **3. Starting the Bot**  
- Loads settings from `config.json`.  
- Spawns a separate thread for each message.  
- Sends messages at random intervals.  
- Logs each sent message with timestamps.  

#### **4. Shutting Down**  
- When interrupted (`Ctrl+C`), the bot stops all threads.  
- Ensures a graceful shutdown without abrupt termination.

---

## 🤖 <u>Project Repository</u>

Although the project didn't took much time on coding phase, the research and ideation phase took almost a day, before I finalized a proper structure, design and proper logic to implement to build this project. 

{% github yashksaini-coder/Auto-MSG-Discord %}

Here's 🎞️ demo of me testing and running the bot live to automate sending messages on a particular channel on my own Discord server.

{% youtube https://www.youtube.com/watch?v=e_oeqp96lRc %}

---

## 🌐Conclusion

This project was very fun and challenging. Instead of using high use-case Python libraries, I used simple logic with very simple libraries to automate and send messages to a widely used application and the best part was to see that the code was working as it was intended and designed to do. Fulfilling and working properly, with a seamless, minimal, sleek UI design.
 


    
  