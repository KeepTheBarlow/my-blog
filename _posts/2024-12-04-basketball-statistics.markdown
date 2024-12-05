---
layout: post
title:  "Visualizing a Winning Team: A Look into College Basketball Data"
date:   2024-12-04
description: Introducing an app that will let you explore why winners win.
---

<p class="intro"><span class="dropcap">C</span>ollege basketball captures the attention and imagination of millions every year, especially in March. Each team, along with hordes of their dedicated fans, will do most anything to increase their winning chances. Thousands of coaches, players, and fans across the country ask themselves how their team can win more games, so that was the question I set out to answer. In my <a href="https://keepthebarlow.github.io/my-blog/blog/data-curation/">previous post</a>, I showed how to scrape basketball statistics and some interesting features of the data. Here, we will dive deeper into the data and conclusions, as well as look at an app that will allow you to explore the data yourself. Ultimately, between this post and the app, we will be able to uncover some of the mystery behind winning teams in college basketball.</p>

## Insights

In the curated basketball statistics data scraped in the previous post (that can be found in [this repository](https://github.com/KeepTheBarlow/basketball-stats-app)), the data was broken up into all time data and data for the 2023 season. I'll focus on one interesting insight from each time period.

For the 2023 season, this correlation heatmap shows which variables were the most connected with winning percentage.

<figure>
    <img src="{{ '/assets/img/corr_heatmap.png' | relative_url }}" alt="">
    <figcaption>Figure 1. - Correlation Heatmap of 2023 Season Stats</figcaption>
</figure>

Interestingly enough, winning percentage seems to have a higher correlation with offensive statistics such as rebounds and assists (0.62 and 0.67 respectively) than with steals and blocks (0.35 and 0.35 respectively). At least in the 2023 season, it seems like offense was a better predictor of team success than was defense. While many people claim defense is the end all be all to winning a national championship, this shows that offense plays an arguably bigger role. It could be due to how offenses are becoming more optimized through data analytics.

For the all-time data, the relationship between NCAA tournament appearances (the biggest tournament in the sport) and win percentage in 2023 can provide insight into the "elite" tier of college basketball.

<figure>
    <img src="{{ '/assets/img/ncaa_apps.png' | relative_url }}" alt="">
    <figcaption>Figure 1. - Scatterplot of the relationship between tournament appearances and win % (2023)</figcaption>
</figure>

Although this is just one season, we can clearly see a strong, positive relationship between tournament appearances and win percentage in 2023. The relationship tells us that the historically successful teams continue to win at a higher clip than the lower teams, suggesting a higher tier of teams. While there are some outliers, with some teams potentially having down years, the trend is positive. The old adage of "the rich get richer" seems to apply to college basketball, with the top recruits going to successful programs and making it harder for the smaller programs to break through.

## Streamlit App

The great thing about sports statistics are the multitude of insights and conclusions that can be drawn. Many different variables go into winning and it can be more complicated than just a heatmap or scatterplot. For this reason, I decided to make a [Streamlit App](https://college-basketball-statistics.streamlit.app/) that will allow you to explore the data and find your own conclusions.

The app includes:
* A team selector
* Summary statistics for 2023 season and all-time
* Comparison of selected team with all other teams
* Ability for you to create your own scatterplot
* Other interesting graphs that couldn't be included in this post

#### Instructions

While using the app, all you have to do is select a team from the search area on the sidebar. This will pull up the summary statistics for your team, compare them with the top 10 all time winningest teams, and highlight them in a scatterplot for the 2023 season. The scatterplot itself allows you to select your own variables to find interesting conclusions for yourself and about a team of your choice. For example, you could select the team "Brigham Young", put assists on the X-axis, and winning percentage on the Y-axis. Now, you can see the relationship between assists and winning percentage across the entire NCAA with BYU highlighted in red. Ultimately, the purpose of the app is to allow any user to explore relationships they are curious about.

## Conclusion

Working with basketball data allows you to dip your feet into the energy and and fervor that accompanies NCAA basketball. Fanatical fans and passionate players do all they can to will their team to a victory. Interestingly enough, statistics are becoming a bigger and bigger part of that winning formula. Just from this basic data exploration, we have seen how offensive stats seem to impact winning more. In addition, we found the existience of an elite tier of teams that continue to win and make it to the NCAA tournament. The [Streamlit App](https://college-basketball-statistics.streamlit.app/) allows you to ask your own questions and make your own conclusions. Try the app out and see if you can find other conclusions in the data!

[GitHub Repository](https://github.com/KeepTheBarlow/basketball-stats-app)
[Streamlit App](https://college-basketball-statistics.streamlit.app/)

Citation:
Sports Reference LLC. College Basketball at Sports-Reference.com - College Basketball Statistics and History. [http://www.sports-reference.com/cbb/](http://www.sports-reference.com/cbb/). (11/13/2024)