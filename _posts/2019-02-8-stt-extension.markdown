---
title: "Transkribieren von Whatsapp-Sprachnachrichten"
layout: post
date: 2019-02-08 14:10
tag:
  - javascript 

headerImage: false
projects: true
hidden: true # don't count this post in blog pagination
description: "Eine Chrome Erweiterung, die Sprachnachrichten transkribiert."
category: project
author: timondohnke
externalLink: false
lang: de
ref: stt-extension
---

Whatsapp-Sprachnachrichten können sehr lang sein und man weiß nie, ob es eine wichtige Frage/Info im Audioclip gibt. Diese Tatsache hat mich so genervt, dass ich eine einfache Chrome Erweiterung schrieb, um die Sprachnachrichten automatisch in Text auf der Web-Version von Whatsapp zu transkribieren.

**Sprachnachrichten erkennen:**

Zuerst überprüfe ich in bestimmten Zeitabständen, ob eine Sprachnachricht geladen ist. Danach wird die Sprachnachricht aus dem Blob-Speicher  von Chrome geholt und gehasht.  

Der Hash wird mit Hashes von zuvor transkribierten Sprachnachrichten verglichen. Wenn der Audioclip bereits transkribiert ist, wird der Text der Nachricht aus dem Chromspeicher geladen. Andernfalls wird die Audiodatei transkribiert.

**Sprachnarichten transkribieren:**

Die Transkription des Audios erfolgt mit Hilfe von Googles Speech to Text (STT) Api. Wenn der Audioclip kürzer als 1 Minute ist, kann die Sprachnaricht direkt base64 kodiert gesendet werden. Der Ton der Sprachnachrichten ist mit OGG Opus kodiert und hat eine Abtastrate von 16000 Hz.

Bei längeren Sprachnachrichten muss der Audioclip zunächst in einen Google Bucket Speicher hochgeladen werden. Der temporäre Token für den Google-Speicher Json Api wird mit Googles Token Api und einem Json Web Token von einem privaten Schlüssel erzeugt. Dies ist in keiner Weise ein ideales/sicheres Setup zur Generierung des Json Web Token.  

Danach wird eine Anfrage an die STT-Api mit der URL der gespeicherten Audiodatei gesendet und anschließend wird die Audiodatei aus dem Google-Speicherbereich gelöscht. Schließlich wird der Vertrauenswert der STT api an das Ende der Nachricht angehängt, um einen Hinweis auf die Qualität des transkribierten Textes zu geben. Der STT-Api-Schlüssel und andere Geheimnisse können über das Popup-Menü der Erweiterung eingegeben werden. 

![](/assets/images/project_stt/expanded.png)
*Erweiterte Ansicht einer transkribierten Sprachnachricht*

![](/assets/images/project_stt/collapsed.png)
*Verkleinerte Ansicht*

**Fazit:**

Der transkribierte Text ist ziemlich ähnliche wie die tatsächlich gesprochene Worte, wenn es keine größeren Hintergrundgeräusche gibt. Der Transkriptionsprozess dauert jedoch etwa etwas weniger als die Dauer der Sprachnachricht selbst. Man muss also noch warten, bis man die Nachrichten gelesen haben, aber der Vorgang der Transkribtion geschieht automatisch im Hintergrund. Die beschriebene Erweiterung könnte theoretisch auch schwerhörigen Menschen helfen, Sprachnachrichten zu verstehen.

Allerdings verstößt die Erweiterung höchstwahrscheinlich gegen die Nutzungsbedingungen von Whatsapp/Google und lokalen Datenschutzgesetzen (z.B. DSGVO). Ich habe diese Art von Erweiterung nie benutzt oder befürwortet.

---

Wenn Sie weitere Fragen/Ideen hast, können Sie mir gerne eine E-Mail schicken an me[at]timondohnke.com  
