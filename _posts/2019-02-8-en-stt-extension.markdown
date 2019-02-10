---
title: "Transcribing Whatsapp voice messages"
layout: post
date: 2019-02-08 14:10
tag:
  - javascript 

headerImage: false
projects: true
hidden: true # don't count this post in blog pagination
description: "A chrome extension transcriping voice messages"
category: project
author: timondohnke
externalLink: false
lang: en
ref: stt-extension
---

Whatsapp voice messages can be very long and you never know if there is an important question/info in the audio clip. I was so bothered by this fact that I wrote a simple chrome extension to automatically transcribe the voice messages into text on the web version of Whatsapp.

**Detecting voice messages:**

First of all I check  at certain time intervals if a voice messages is loaded in the content script of the extension. After that the voice message is fetched from the blob storage and hashed.  

The hash is compared to hashes of previously transcribed voice messages. If the audio clip is already transcribed, the text of the message is loaded from chrome storage. Otherwise the audio clip gets transcribed.

**Transcribing the audio:**

The transcription of the audio is made with help of Google's Speech to Text (STT) api. If the audio is less than 1 minute, the audio can be send directly base64 encoded to the api. The audio of the voice messages is encoded with OGG Opus and has a sample rate of 16000 Hz.

For longer voice messages the audio has to be first uploaded to a Google storage bucket. The temporary token for the Google storage json api is generated with Google’s token api and a Json Web Token from a private Key. This is in no way an ideal/secure setup to generate the Json Web Token.  

After that an api request is send to the STT api with the url of the stored audio file and following that the audio file gets deleted from the google storage bucket. Lastly the confidence score of the STT api is append to the end of the message, to give an indication about the quality of transcribed text. The STT api key and other secrets can be entred through the popup menu of the extension. 


![](/assets/images/project_stt/expanded.png)
*Expanded View of a transcribed german voice message*

![](/assets/images/project_stt/collapsed.png)
*Collapsed  View*

**Conclusion:**

The transcribed text is quite accurate to the actual spoken words, if there are no major background noises. However the transcription process takes roughly a bit less than the duration of the voice message itself. Thus you still have to wait before reading the messages, but this process is done automatically in the background. The described extension could theoretically also help hard of hearing people to understand voice messages.

That said the extension most likely violates the Terms & Service of Whatsapp/Google and your local privacy laws (e.g GDPR). I never used nor endorse this kind of extension.

---
If you have anymore questions/ideas, feel free to send me an email at me[at]timondohnke.com  
