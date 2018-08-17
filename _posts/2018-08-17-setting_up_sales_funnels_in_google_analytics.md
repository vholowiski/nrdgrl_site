---
layout: post
title: Setting up a goal sales funnel in Google Analytics
categories: GoogleAnalytics
---

## The stuff nobody tells you

First thigns first. A sales funnel isn't just for selling things. If you have an important goal on your web site that has distinct steps to it, you want to set up a sales funnel. A sales funnel allows you to track drop-off throughout the goal completion steps, so that you can identify improvements to increase your conversion rate.

Like everything google, there is no shortage of documentation, but like everything google, the devil is in the details, and there's some important things that are unclear, left out, or just hard to find. I'll show you how to set up a sales funnel properly in google analytics.

### Below is a list of tips tricks & troubleshooting for google analytics sales funnels. Keep coming back & I'll keep updating this. 

* [Sales funnel data collection is not retroactive](#sales_funnel_retroactive)
* [There are a limited number of goals you can set up](#limited_number_of_goals)
* [You can't ever delete a goal, or goal data](#cant_ever_delete_goal)
* [The Destination match type applies to funnel steps](#destination_match_type)

<span id="sales_funnel_retroactive">**To create a sales funnel**</span> you need to set up a goal first. Goals are not retroactive, they start collecting data from the moment you create them. If you add steps to a goal later those are also not retroactive. If you create goal steps part way through the day, you can't really trust the data until the next day because you will have a mix of data with and without the goal steps.

<span id="limited_number_of_goals">**There are a limited number of goals** and you can't delete previous goal data</span>. The limit for the 'free' version of google analytics is 20 per view. You CAN go over 20, you just have to create a new view (You can create up to 25 - I've read 50 elsewhere but my account shows 25) and create the additional goals there (note that a view also doesn't start recording data until you create it. Might be a good idea to create a bunch ahead of time!). If you need more than 20 goals you'll have to pony up for google analytics premium ($150,000+ USD/Year!)

<span id="cant_ever_delete_goal">**You can't ever delete a goal!**</span> You can only stop recording on a goal and/or rename it. When I'm done with a goal I will disable it and change the name to DELETED so I know to reuse it later - but be careful, you can't ever delete goal data so old conversions will show for a goal even after you've changed it. For this reason, I'd recommend testing goals first in a seperate testing view before putting them in you main view, so you don't 'pollute' your main data.

<span id="destination_match_type">**You need to choose a 'destination' for a goal**</span> if you want a sales funnel. The match type you choose ('Equals To', 'Begins With', 'Regular Expression') doesn't only apply to the destination url, it applies to all the steps as well. Yeah. Hard to figure that one out but it's documented here: https://support.google.com/analytics/answer/1116091?hl=en

That's all for now, but be sure to check back for more gotchas as I discover them!
