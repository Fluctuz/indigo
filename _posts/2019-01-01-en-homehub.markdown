---
title: "HomeHub - small useful screen"
layout: post
date: 2019-01-01 12:10
tag:
  - python
  - raspberry_pi
headerImage: false
projects: true
hidden: true # don't count this post in blog pagination
description: "This project allows one to access different apis through a small display on a Raspberry Pi 3."
category: project
author: timondohnke
externalLink: false
lang: en
ref: homehub
---

 <p style="text-align: center"><img src="/assets/images/project_homehub/timefinal.jpg" width="220" />
</p>

# HomeHub
---

The project allows one to access different apis through a small display on a Raspberry Pi 3. The display is 128x64 pixel monochrome LCD with 6 buttons from [Pimoroni](https://shop.pimoroni.com/products/gfx-hat). The interface consists of multiple screens, which each display the information from one api, and can be switched through by button presses.

The screens run on a separate thread, which can be interrupted through button presses. This allows the screen thread to sleep most of the time, because the apis don’t provide any new information that often.

Furthermore it’s possible through a flag in the screen controller file to switch the output to a tkinter (gui) application. This can be useful to test the application on a pc.

**Tkinter Application:**
   <p float="left">
      <img src="/assets/images/project_homehub/gui_time.png" width="220" />
      <img src="/assets/images/project_homehub/gui_spotify.png" width="220" /> 
    </p>


**Project File Structure:**

The projects structure allows to separate the the data gathering in one module(“Api” folder) and the drawing of it in another module(“Screens” folder). Through this designs it’s easy to add different apis/screen without changing existing code. The api keys are stored in the config.json file.


{% highlight raw %}
HomeHub/
├── Screens/
│   ├── screen.py //abstarct class 
│   ├── spotify_screen.py  
│   ├── weather_screen.py
│   		⋮
├── Api/
│   ├──config.json
│   ├──spotify_api.py
│   	 	⋮
├── Screen_controller/
├── Fonts/
├── Assets/
├── manager.py
└── background_script.py
{% endhighlight %}




**The different screens:**
    
  
  <p>Weather and Time screen:  &nbsp; &nbsp;&nbsp; &nbsp; &nbsp; &nbsp; Spotify screen (control playback/shows current song): </p>

   <p float="left">
        <img src="/assets/images/project_homehub/timefinal.jpg" width="220" />
        <img style="margin-left: 10%;" src="/assets/images/project_homehub/spotifyfinal.jpg" width="220" /> 
    </p>


  
  <p>ToDo list screen with Todoist Api:&nbsp; &nbsp; &nbsp; Time tracking screen with Toggl:
 </p>

   <p float="left">
        <img src="/assets/images/project_homehub/todoistfinal.jpg" width="220" />
        <img style="margin-left: 10%;" src="/assets/images/project_homehub/togglfinal.jpg" width="220" /> 
    </p>

---

You can check the project out on my [github](https://github.com/Fluctuz/HomeHub).