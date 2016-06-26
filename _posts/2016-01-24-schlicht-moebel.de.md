---
title   : Schlicht Moebel
info    : Designer group portfolio
github  : herrjemand/schlicht-moebel.de
web     : https://schlicht-moebel.de/
pid     : 20160124schlicht-moebel.de
---

In 2015, November, a group of designers from KISD(Köln International School of Design) had reached my friend, who is designer him self, and asked to design a portfolio website for them. That was a great group project opportunity that we decided to take.

We decided to take functionalistic approach. Straight lines, squared images, thing but clearly visible border between elements, dark gray background, orange icons. The system where each element has it's specific function, and it feels like if it breaks, it can be substituted. Simple, but effective. "Schlicht, means to focus on the essential design. Keep it pure. Moderate and unaffected." is the MOTO of the Schlicht Moebel group, and so the website have to correspond to these rules.

![Screenshot](/assets/post/20160124schlicht-moebel.de/screenshot.png)

For our technology stack we decided to use **Zurb Foundation** framework, as it was mature, well developed framework that has been tested in the past. CMS was simply too excessive, and complicated, for our project, but in the same time we had a need for templating. Static site generator was obvious choice, and so we went with **Jekyll**.

One of the major challenges was to implement multi-language support. We decided to separate English and German content into **de** and **en** folders correspondingly. Templates variables are stored in site config. Developed translation scheme allows us easily modify and add languages on-demand.

This project was challenging and educative. Working with German based project had improved my personal Deutsch sprechen skills, and writing fully static site had shown me different approach in web development.