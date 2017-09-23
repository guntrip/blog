---
layout: post
title:  "Frame software"
categories: hacking
---
I had a frame, a box of other frames I didn't want to talk about, some circuit boards, and a piece of expensive plastic to hold it all together. My next task was to make it all work.

It would have been possible to use the Pi's IO pins to communicate directly with the screen but I was not confident I'd get that working. Instead, I ordered a USB interface (USB2TCM) sold by the manufacturer. This mounts as a USB flash drive and allows you to transfer a single file which the interface reads and communicates to the screen.

Raspbian is a Pi-friendly version of Debian. I've installed Apache, so I can have some user-facing settings and an easier time debugging, and PHP 7, which this will be written in. So I can work on this locally, quickly deploy it to the frame, and eventually share the code with others, I've built a simple settings page that allows the user to add calendars and API tokens. This also allows me to toggle the environment; the "demo" environment halts execution after the image is built and displays it in the browser rather than trying to send it to the frame.

The `task.php` script gathers all the necessary information and draws a PNG using PHP's graphics libraries. I'm using the private .ics address from Google Calendar. This gives me a file I can parse for each calendar but causes a few problems; the output is very.. raw. I've had to write my own function to recreate repeating events from their patterns (and modify individual occurrences as they are changed or cancelled). This is working most of the time.

The script also calls upon Darksky's API to collect some weather information (what would a Raspberry Pi display project be without weather?). It also has a to-do list powered by a tiny API that allows me to update it remotely via a public-facing home server. Finally, you can also send the API little 32x32 pixel doodles that display in a repeating pattern at the bottom for 24 hours.

The biggest challenge in this project, other than talking to framers and cutting straight lines, was Pervasive Displays' EPD format. The documentation contains a single snippet of Java for converting a bitmap into this format. Each screen they offer has a different format, and some -  such as my 7" screen - are confusingly interlaced with each byte representing two parts of the image. I tried to recreate this snippet in PHP but had trouble using PHP to write binary data. It's not something I had touched before and I couldn't keep my nice stream of 1s and 0s in the right format.  

I got so close at one point that I was sending images to the frame to try and perfect what each bit represented. These are meant to be triangles:

![Trying to get the screen working](/assets/images/blog/frame/frameconfusion.jpg)

I gave up using PHP for this. As I had the working Java snippet, I made a quick command line Java application that accepts a PNG and converts it into an EPD. Learning to make my first Java application was less infuriating than getting this working in PHP. I since had someone who understands Java look at my creation and confirm that it is not terrible.

This makes the process a little more chaotic than I would have liked: A cron job triggers a bash script every ten minutes and runs `task.php` in PHP CLI. *If* something has changed, PHP saves a new PNG and executes another bash script (>.<) that runs that PNG through my Java application and then transfers it to the frame. Once the screen has processed the image, after about twenty seconds, it updates. It's possible to force it to update quicker by mounting and unmounting the device but I'm not in a hurry.

![Up and running!](/assets/images/blog/frame/frame12.jpg)

My plan is to release all the plans and all the software on my GitHub account once it's usable.
