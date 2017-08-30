---
layout: post
title: ReMus
permalink: /projects/remus/
---
# **🎼 ReMus: Restoration of Music 🎼**

#### By **Oscar K. Sandoval** and **2 Anonymous Contributors** (Spring 2017)
_See the full project, including all stages of development at [https://github.com/mtfalls/ReMus](https://github.com/mtfalls/ReMus)_

## **Summary**
![ReMus-Landing](/docs/ReMus/ReMus_Landing.png){:class="img-responsive"}{:height="100%" width="100%"}
<br>
**ReMus** is a platformer where the player must use their hookshot to travel from platform to platform
and collect music notes before music is lost forever. Each level starts off with a dreary background and distorted music, and each time the player collects a certain threshold of notes, the level gradually becomes restored. Should the player collect the required amount of notes to fully restore a level, they are presented with a song that is the order of the notes they had collected throughout the level. Should the player fail, they are presented with a future where music is lost forever.

## **Controls**

### **Keyboard** ![keyboard-icon](/docs/ReMus/keyboard.png){:class="img-responsive"}{:height="5%" width="5%"}

* Arrow Keys - Move left, right, and jump
* Q - turn the hookshot counterclockwise
* W - turn the hookshot clockwise
* Spacebar - fire the hookshot

### **Xbox 360 Controller** ![xbox360-controller-icon](/docs/ReMus/xbox360_controller.png){:class="img-responsive"}{:height="5%" width="5%"}

* Left Stick - Move left, right, and jump
* Right Stick - Aim the hookshot
* Left Bumper - turn the hookshot counterclockwise
* Right Bumper - turn the hookshot clockwise
* Right Trigger - fire the hookshot

## **Level Design**

### **Tutorial**

<iframe width="560" height="315" src="https://www.youtube.com/embed/mdb10MJK0nM" frameborder="0" allowfullscreen></iframe>
The Tutorial is very simple in design philosophy: introduce the player to the basic controls, and allow them to play around with the hookshot mechanic in an environment that does not not penalize them for failing.  The Tutorial also introduces the player to the <span style="color:blue">**blue platform**</span>, which does stays in place and does not move unless the screen is descending (as shown in the subsequent levels).

### **Level 1**
<iframe width="560" height="315" src="https://www.youtube.com/embed/7-Nd6Ja_IlY" frameborder="0" allowfullscreen></iframe>
**Music:** MapleStory - *Ereve* <br>
Level 1 introduces the concept of failing via not collecting enough notes, which is designated as the **Note Lives Left** in the top left corner of the HUD. Should the player run out of Note Lives (which are lost when they are no longer in the playing area), they will lose the level. Level 1 also introduces the player to the concept of **Restoration**, where the player's gradual success during a level slowly restores the background and the music.

### **Level 2**
<iframe width="560" height="315" src="https://www.youtube.com/embed/45aEiBAZsiU" frameborder="0" allowfullscreen></iframe>
**Music:** MapleStory - *The Temple of Time* <br>
Level 2 introduces the concept of failing via falling. Should the player's entire character model fall below the bottom of the screen (where they are no longer visible), the player will fail the level.

### **Level 3**
<iframe width="560" height="315" src="https://www.youtube.com/embed/lOo-Xztib-A" frameborder="0" allowfullscreen></iframe>
**Music:** Super Smash Bros. Brawl - *Bramble Blast* <br>
Level 3 introduces the player to a horizontally moving playing field, and several new platforms:

* <span style="color:red">**red platforms**</span> which move back and forth horizontally
* <span style="color:lime">**green platforms**</span> which the player cannot stand on, but can only be hooked onto
* <span style="color:yellow">**yellow platforms**</span> which move back and forth vertically
* <span style="color:orange">**orange platforms**</span> which the player can bounce on

### **Level 4**
<iframe width="560" height="315" src="https://www.youtube.com/embed/oIjIYgkBWC0" frameborder="0" allowfullscreen></iframe>
**Music:** Brave Frontier - *The Tower* <br>
Level 4 introduces the concept that the player may have to do several passes of a screen to succeed in a level. The player may also realize from some of the harder jumps that the hookshot does not instantaneously hook onto a platform. In reality, there is a small delay where the hookshot must reach its maximum length before being able to hook onto any platform.  

### **Level 5**
<iframe width="560" height="315" src="https://www.youtube.com/embed/vRoufgBQWqw" frameborder="0" allowfullscreen></iframe>
**Music:** DJ Genki - *Lisa RICCIA (DJ Genki Remix)* <br>
Level 5 is essentially the pinnacle of challenge for pro hookshotters to test their meddle. The level scrolls quickly with few blue platforms for rest, and introduces the player to <span style="color:pink">**pink platforms**</span>, which do not move regardless of how the screen is traveling.  

## **Acknowledgements**
A few people I would like to thank in the development and creation of ReMus:

* my fellow collaborators for their hard work in the project
* the University of Virgina's Computer Science Department for offering a Game Design course
* Professor Floryan for teaching the Spring 2017 Game Design course, among mentorship and continual feedback for everyone's projects
* the Graduate TA's for having the perseverance to (eventually) grade everything, from our code to our written pieces
* and finally you, the reader for taking interest in ReMus :)
