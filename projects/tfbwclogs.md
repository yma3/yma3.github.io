---
title: The Friendly Bunch Warcraft Logs
layout: archive
---

I believe one of the most powerful applications of data analysis is informed decision making, but doing it well is hard. Part of it is selecting metrics that are indicative of good or bad performance, and defining these metrics is very important.

The way large guilds handle raiding groups (20-man teams) is extremely similar to sports teams. There are starters, there's a bench, there are subs, there's a "captain" or raid lead. Even the language is similar. So when you're putting together a raid group, how do you determine who to start? In sports, you don't have the luxury to rotate through dozens of applicants a week, but in video games, you can.

The easiest way is to look at "DPS" on their fights. In WoW, players have logs of their past performances in different raids, and raid groups tend to use that as their main metric for performance. Players with good DPS numbers get placed in, and that's that. We've successfully picked the best team with data. We're done.

Well... no. Although DPS does correlate very well with good players, they don't necessarily correlate well with good raiders. Raiding is a 20-person effort where the mistake of one person propagates through the entire group.

{: style="text-align:center"}
![NZothFight](/assets/images/tfbwclog/bossHPmodel.png)

Take this plot that was calculated at around wipe 174. The constant dips back up to 100% health is because sometimes we mess up. We mess up a lot and it's only after a lot of trial and error do we see improvements. However, we can see with the moving average models that we're doing okay.

The horizontal bars indicate a day of raiding, and on day 3, we made some improvements! Then we regressed on day 4... But on day 5 we did really well! And on day 9, wow! We did really really well. It's easy to say day 1,2,3,4, but we have to remember that by day 9, well that's a month and a half into the fight.

At around that same time we had the big jump, we also started looking at other ways to recognize our performance. Let's look at how we're doing in terms of taking damage, because taking damage directly correlates to wiping.

{: style="text-align:center"}
![corrupted](/assets/images/tfbwclog/corruptedviscera.png) |
![NZothFight](/assets/images/tfbwclog/devourthoughts.png)

We see that at this point, we haven't really improved THAT much in terms of getting hit by Corrupted Viscera (Red), but we've improved pretty dramatically in terms of getting hit by Devour Thoughts (Purple). In fact, we realized devour thoughts was a more important mechanic to avoid, so we pushed heavily for our players to focus on dodging the purple. Turns out it was a good idea as we got that much closer to our goal.

This same data was how we determined if certain players were performing well or poorly. Instead of looking purely at DPS, we looked at how much each player contributed to getting hit by damage. Players who were contributing more to taking damage were told individually to be more mindful even at the sacrifice of DPS, and that direction ended up successful.

We killed N'Zoth on Wipe 226. A couple days after what we expected and hoped, but a finish nonetheless. I made a small infographic detailing our adventures in The Friendly Bunch, and our journey through the hardest content WoW had to offer at the time.

{: style="text-align:center"}
![NZothFight](/assets/images/tfbwclog/TFBInfoBig.png)
