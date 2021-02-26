---
layout: post
title: FEH Gauntlet Bot
permalink: /projects/feh-gauntlet-bot/
---
# **Fire Emblem Heroes Gauntlet Bot**   ![Battle Flag](/docs/FEH-Gauntlet-Bot/battle_flag.png){:class="img-responsive"}{:height="4%" width="4%"}

#### By **Oscar K. Sandoval** (Summer 2017)
_See the full project at **[https://github.com/atemosta/FEH-Gauntlet-Bot](https://github.com/atemosta/FEH-Gauntlet-Bot)**_

## **Summary**
<a class="post-link" href="https://twitter.com/FEHGauntletBot"><img src="/docs/FEH-Gauntlet-Bot/gauntlet_landing.PNG" style="width: 100%; height: 100%"/></a>
<br>
**FEH Gauntlet Bot** is a Twitter bot thats posts hourly updates when disadvantage multipliers are up for #FEHeroes Voting Gauntlets! [Click here to view its Twitter page!](https://twitter.com/FEHGauntletBot)

## **How This Bot Works**
At a high-level overview, this bot scrapes webpage data from the current Voting Gauntlet (e.g [https://support.fire-emblem-heroes.com/voting_gauntlet/tournaments/6](https://support.fire-emblem-heroes.com/voting_gauntlet/tournaments/6)), stores the scores of the currently competing units, compares each pair of competing units, then tweets if either unit has their disadvantage multiplier up! Depending on each hourly situation, **FEH Gauntlet Bot** may posts up to four tweets at once during the first round, or not tweet at all if all the matches are close.

### **Scraping Voting Gauntlet Data**
As **Fire Emblem Heroes** has no developer API to support app creation (especially during seasonal events such as the Voting Gauntlet), the next best way to extract data about the game would be going to their online site! Luckily enough, **Fire Emblem Heroes** has a series of webpages dedicated to exhibiting ongoing Voting Gauntlets and preserving previous competitions. These webpages hardcode the number of votes a unit currently has at a given time, so extracting that data is as simple as finding where the number of votes are written in the source code and associating that value that with the correct unit!

### **When To Tweet**
To determine the current score multiplier during a typical 45 hour round, the formula reduces to simply <br>
`(hour of the competition * 0.1) + 3.1` for a maximum mutiplier of 7.5x during hour 44 (hour 45 does not have a multiplier since the round ends at that time). But when does **FEH Gauntlet Bot** know when an army has their disadvantage multiplier up? After comparing the current number of votes between competing units every hour, if one unit's army has **10% more votes** than its competitor, the disadvantage multiplier is set for the next hour! Unfortunately for players that are dedicated to their army, this bot is unbiased and will tweet when any unit has a disadvantage multiplier up, not just their army! There may also be droughts where the bot will not tweet at all due to close competition between all current competitors in a round. Lastly, the bot will tweet important announcements related to the current Voting Gauntlet or about the bot itself (typically when updating tweet content or before going down for maintenance).

## **Why Twitter?**
As **Fire Emblem Heroes** is a mobile game, I wanted to utilize the fact that most players will have their phone on hand during Voting Gauntlets. What is the best way to alert users with a mobile device? I mused on the idea of creating an application with notifications, but my expertise is limited to Android, which excludes over half of the current playerbase who own Apple devices. This application is also too specific and only used seasonally, so this may not be be considered a worthwhile download for potential users. I also mused on the idea of sending SMS texts, but this may also become a burden to players with hourly messages on team updates they may not care about. I finally settled on using Twitter as the platform for live alerts, but **why Twitter?** There are three main reasons for this choice:

* **Twitter is easy to access and understand without an account**: As Facebook is a platform that likes to place popular and trending content on the forefront of their users' feeds, Twitter instead opts for recent posts as the forefront of their users' feeds. By simply visiting [https://twitter.com/FEHGauntletBot](https://twitter.com/FEHGauntletBot), users will be able to see up-to-the-hour updates on which armies currently have a disadvantage multiplier up, all without needing an account!
* **Twitter has an amazing mobile application with notifications for hardcore users**: For those users who want live updates on when their favorite account tweets, Twitter's mobile application has mobile device notifications! As users have to manually toggle mobile notifications per account they follow, this enables users to pick-and-choose from where and when they wish to receive notifications (perhaps for seasonal Voting Gauntlets? *Hmmmm* 😉). If an account posts too much or changes their seasonal content, users can simply turn off mobile notifications or unfollow them.
* **Making a Twitter bot is ridiculously easy with Python**: So long as you know what you want to post and have your application credentials ready, Python's `tweepy` library makes posting to twitter as simple as `api.update_status(text)`!
  * If you're interested in making your own Twitter Bot, check out [Molly White's awesome tutorial](http://blog.mollywhite.net/twitter-bots-pt2/) or my very own [POTF Lyrics Bot](http://localhost:4000/projects/potf-lyrics-bot/)!

## **Hosting**
**FEH Gauntlet Bot** is currently being hosted on a [Digital Ocean VPS](https://www.digitalocean.com/) for $5 a month. To ensure that the bot continues to run every hour after the remote session is closed, I used:
{% highlight ruby %}
nohup python gauntlet.py &
{% endhighlight %}
To take the bot down for maintenance, I search for the `process id` using `ps -x` and kill the process with `kill [pid]`.


## **Acknowledgements**
A few people I would like to thank in the development and creation of **POTF-Lyrics-Bot**:

* [Intelligent Systems](https://www.intsys.co.jp/) for developing an awesome mobile based on an amazing game series
* [Python](https://www.python.org/) for being an approachable and easy-to-learn programming language
* [Molly White's](http://blog.mollywhite.net/) brilliant tutorial on [how to create a Twitter bot](http://blog.mollywhite.net/twitter-bots-pt2/)
* [Digital Ocean](https://www.digitalocean.com/) for providing an affordable cloud platform for amateur and professional developers alike
  * If you would $10 of credit for trying out Digital Ocean's products, [please follow this referral link! ](http://www.digitalocean.com/?refcode=d04140365cd1)
* And finally you, the reader, for taking interest in **FEH Gauntlet Bot** :)
