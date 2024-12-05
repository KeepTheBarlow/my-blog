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

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6

<blockquote>Aenean lacinia bibendum nulla sed consectetur. Morbi leo risus, porta ac consectetur ac, vestibulum at eros. Cras mattis consectetur purus sit amet fermentum. Nulla vitae elit libero, a pharetra augue. Curabitur blandit tempus porttitor. Donec sed odio dui. Cras mattis consectetur purus sit amet fermentum.</blockquote>

Nullam quis risus eget urna mollis ornare vel eu leo. Cras mattis consectetur purus sit amet fermentum. Duis mollis, est non commodo luctus, nisi erat porttitor ligula, eget lacinia odio sem nec elit. Vivamus sagittis lacus vel augue laoreet rutrum faucibus dolor auctor.

## Unordered List
* List Item
* Longer List Item
  * Nested List Item
  * Nested Item
* List Item

## Ordered List
1. List Item
2. Longer List Item
    1. Nested OL Item
    2. Another Nested Item
3. List Item

## Definition List
<dl>
  <dt>Coffee</dt>
  <dd>Black hot drink</dd>
  <dt>Milk</dt>
  <dd>White cold drink</dd>
</dl>

Donec id elit non mi porta gravida at eget metus. Cum sociis natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Maecenas faucibus mollis interdum. Donec sed odio dui. Cras justo odio, dapibus ac facilisis in, egestas eget quam.

## Table

| Syntax      | Description |
| ----------- | ----------- |
| Header      | Title       |
| Paragraph   | Text        |
| Header      | Title       |
| Paragraph   | Text        |

## Code Snippet

{%- highlight python -%}
def print_hi(name):
  print("Hi" + name)
print_hi('Tom')
#=> prints 'Hi, Tom'.
{%- endhighlight -%}


## Figure with Caption

<figure>
	<img src="{{site.url}}/{{site.baseurl}}/assets/img/touring.jpg" alt=""> 
	<figcaption>Figure 1. - This is an example figcaption</figcaption>
</figure>


{%- highlight html -%}
<figure>
	{% raw %}<img src="{{site.url}}/{{site.baseurl}}/assets/img/touring.jpg" alt="">{% endraw %}
	<figcaption>Figure 1. - This is an example figcaption</figcaption>
</figure>
{%- endhighlight -%}

