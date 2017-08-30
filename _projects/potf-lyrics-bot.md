---
layout: post
title: POTF Lyrics Bot
permalink: /projects/potf-lyrics-bot/
---
# **Poets of the Fall Lyrics Bot**   ![POTF-Moth](/docs/POTF-Lyrics-Bot/potf_moth.png){:class="img-responsive"}{:height="5%" width="5%"}

#### By **Oscar K. Sandoval** (Spring 2017)
_See the full project at **[https://github.com/mtfalls/POTF-Lyrics-Bot](https://github.com/mtfalls/POTF-Lyrics-Bot)**_

## **Summary**
<a class="post-link" href="https://twitter.com/POTFLyricsBot"><img src="/docs/POTF-Lyrics-Bot/potf_landing.png" style="width: 100%; height: 100%"/></a>
<br>
**POTF Lyrics Bot** is Twitter bot that posts a tweet every 6 hours based on three random lyrics from all Poets of the Fall songs! [Click here to view its Twitter page!](https://twitter.com/POTFLyricsBot)

## **Backstory**
As a longtime POTF fan, I wanted to create something meaningful based on what I know and what I wanted to learn how to do. My favorite aspect of POTF is the extensive vocabulary for their lyrics (I originally wanted to create a program that counted all the unique words across all their songs!). I eventually came to the idea of maintaining a bot that created abstract poems based on POTF lyrics. After a little research on Twitter bots, I found that Python's `tweepy` library abstracts the process into simply have the proper authentication keys and the text the program wants to post. Pulling single lines from text files is an easy task to do in Python, so together with `tweepy` the bot was born!

## **Hosting**
**POTF Lyrics Bot** is currently being hosted on a [Digital Ocean VPS](https://www.digitalocean.com/) for $5 a month. `compose.py` searches for three unique lyrics, checks the tweet length to be under 140 characters or less, tweets if successful, then sleeps for 6 hours. To ensure that the bot continues to run after the remote session is closed, I used:
{% highlight ruby %}
nohup python compose.py &
{% endhighlight %}
To take the bot down for maintenance, I search for the `process id` using `ps -x` and kill the process with `kill [pid]`.


## **Acknowledgements**
A few people I would like to thank in the development and creation of **POTF Lyrics Bot**:

* [Poets of the Fall](http://poetsofthefall.com/) for being one of the most inspiring bands I listened to throughout middle and high school
* [Python](https://www.python.org/) for being an approachable and easy-to-learn programming language
* [Molly White's](http://blog.mollywhite.net/) brilliant tutorial on [how to create a Twitter bot](http://blog.mollywhite.net/twitter-bots-pt2/)
* [Digital Ocean](https://www.digitalocean.com/) for providing an affordable cloud platform for amateur and professional developers alike
  * If you would $10 of credit for trying out Digital Ocean's products, [please follow this referral link! ](http://www.digitalocean.com/?refcode=d04140365cd1)
* my friends who actually though this was a neat idea to pursue (and the one friend who was considering making Kanye West variant haha)
* and finally you, the reader, for taking interest in **POTF Lyrics Bot** :)
