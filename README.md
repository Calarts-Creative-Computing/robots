![Calarts Creative Computing Logo](https://i.imgur.com/235dOcD.png)

<p align="center">
  <a href="https://github.com/Calarts-Creative-Computing/robots/stargazers">
    <img src="https://img.shields.io/github/stars/Calarts-Creative-Computing/robots?style=social" alt="Stars">
  </a>
  <a href="https://github.com/Calarts-Creative-Computing/robots/watchers">
    <img src="https://img.shields.io/github/watchers/Calarts-Creative-Computing/robots?style=social" alt="Watchers">
  </a>
  <a href="https://github.com/Calarts-Creative-Computing/robots/network/members">
    <img src="https://img.shields.io/github/forks/Calarts-Creative-Computing/robots?style=social" alt="Forks">
  </a>
</p>

<p align="center">
  <a href="https://github.com/Calarts-Creative-Computing/robots/blob/main/LICENSE">
    <img src="https://img.shields.io/github/license/Calarts-Creative-Computing/robots" alt="License">
  </a>
  <a href="https://github.com/Calarts-Creative-Computing/robots/issues">
    <img src="https://img.shields.io/github/issues/Calarts-Creative-Computing/robots" alt="Issues">
  </a>
  <a href="https://github.com/Calarts-Creative-Computing/robots/pulls">
    <img src="https://img.shields.io/github/issues-pr/Calarts-Creative-Computing/robots" alt="Pull Requests">
  </a>
  <a href="https://github.com/Calarts-Creative-Computing/robots/commits/main">
    <img src="https://img.shields.io/github/last-commit/Calarts-Creative-Computing/robots" alt="Last Commit">
  </a>
</p>

<p align="center">
  <a href="https://github.com/Calarts-Creative-Computing/robots">
    <img src="https://img.shields.io/badge/View_on-GitHub-181717?logo=github&logoColor=white" alt="View on GitHub">
  </a>
  <a href="https://github.com/Calarts-Creative-Computing/robots/archive/refs/heads/main.zip">
    <img src="https://img.shields.io/badge/Download-ZIP-28a745?logo=github" alt="Download ZIP">
  </a>
</p>


robots
======

There are currently two servers, one for the hiduino bots (JackBox, BreakBot, Clappers, GanaPati, MahaDevi), 
and one for the serial bots (Lydia, MarimBot, StringThing).

The two servers should always be left running. In the case that they aren't, simply type the following into terminal.

    $ robots

This will run a bash function that kills any running ChucK programs, and then starts the server.

    robots() {
        SERVICE='chuck'

        if ps ax | grep -v grep | grep $SERVICE > /dev/null
        then
            echo "$SERVICE killing running chuck programs"
            killall chuck
        fi

        chuck ~/git/robots/serial-robot-server/master.ck --port:8888 &
        chuck ~/git/robots/hiduino-robot-server/master.ck --port:8889
    }

communication
-------------

**IT IS NOT RECOMMENEDED TO CONNECT WIRELESSLY**

While it is entirely possible to connect using the wireless network, you will definitely experience lag and dropped OSC messages.

To connect using ChucK using OSC with a LAN connection:

    OscOut out;

    ("chuckServer.local", 50000) => out.dest;

To send to a robot using its OSC address.

    out.start("/clappers");
    out.add(note);
    out.add(velocity);
    out.send();

A full list of robots by their OSC addresses

    // hiduino robots
    /drumBot
    /clappers
    /ganapati
    /jackbass
    /jackgtr
    /jackperc
    /devibot


    // serial robots
    /marimba
    /trimpspin
    /trimpbeat
	/stringthing
    /snapperbot
    /rattletron

To connect using MIDI, see the [midi-robot-client](https://github.com/MTIID/robots/tree/master/midi-robot-client) repo.

quick-test-code
---------------
Copy/paste this to quickly see if you can successfully connect using a wired connection.

    OscOut out;
    ("chuckServer.local", 50000) => out.dest;

    while(true) {
        out.start("/clappers");
        out.add(Math.random2(0, 20));
        out.add(127);
        out.send();
        10::ms => now;
    }

maintenance and troubleshooting
------------

In general, if there the server is acting up a simple restart of the ChucK
code will clear things up 90% of the time. This can be done by
opening up terminal and entering in the "robots" command described above.
Also check for multiple instances of terminal that might be 
running on the robots computer. If needed, close the
extra instances and relaunch the server. 

If one of the bots is not responding, first check to see if the bot has
power connected. Some bots, such as Lydia and JackBox, can sometimes be 
accidentally unplugged. Likewise, check the USB cable going to the bot in
question, and if JackBox is the bot that is acting up also check the two 
MIDI cables. If the cable looks good on the bot end, 
don't forget to check the hub end as well. 

If more than one robot is unresponsive, there is a chance that something went 
wrong with one, or more, of the USB hubs. 
Check to see that the hubs are plugged into their power 
bricks, that they are turned on, and plugged into the robots computer.

If you are running code on your computer through the MIDI Client 
and are having issues this might help:

1. Test using ChucK or another programming language without the MIDI Client. 
    - Sometimes the MIDI Client can be a bit finicky, this will tell you if
        its the client itself or some other link in the chain.
2. Restart the MIDI Client (after closing the instance of it).
    - "Uninstall Everything" - Owen Vallis
3. Make sure you have the most recent version of the code ('git pull' the repo).
    - This repo is constantly being updated, the most recent code will be more 
        stable, there is a chance the issue you are running into has been fixed.
4. Test your code (or set) or the robots computer.
    - Is it your computer, or the server?
5. Are any of the bots working, or is it just one or two that is not responding?

programmers
-----------

hiduino-robot-server and midi-robot-client written by Ness Morris and Bruce Lott in the winter of 2013-2014, based on code by Ajay Kapur, Owen Vallis, and Dimitri Diakopoulos

serial-robot-server written by Eric Heep in the summer of 2014. Code is currently maintained by Nathan Shaw.

if there are any questions, concerns or issues feel free to email Nathan at: nathanshaw@alum.calarts.edu

---


<p align="center">
  <img src="https://www.hanoverresearch.com/wp-content/uploads/2020/05/CALARTS-01.png" alt="Calarts Creative Computing Logo" width="300"/>
</p>

Creative Computing at California Institute of the Arts is a forward-thinking interdisciplinary program that fuses the power of computational engineering skills with the limitless possibilities of artistic expression. This innovative degree encourages students to explore the intersection of technology and creativity, using computational tools to craft work that is both personally and culturally meaningful, while preparing them for industry. Our program is designed to provide an integrative learning experience that equips students with the skills to push the boundaries of art, music, and technology. With a strong foundation in computer science, electrical engineering, signal processing, and emerging technologies including virtual/augmented reality, robotics, and machine learning, students will be empowered to innovate, experiment, and reimagine what technology can do in artistic contexts.

<p align="center">
  <a href="https://creativecomputing.calarts.edu/">Learn More</a>
</p>
