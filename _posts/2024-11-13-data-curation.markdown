---
layout: post
title:  "The Art of Winning: A Dive into College Basketball Data"
date:   2024-11-13
description: Exploring what makes winners winners in college basketball, and why they stay that way.
---

<p class="intro"><span class="dropcap">C</span>ollege Basketball is one of the most thrilling sports to watch. Every school has a rabid student section who pack their arena night in and night out to make as much noise as possible. It seems like on any given night, upsets are bound to happen with teams you've never even heard of taking down perennial powerhouses. But that begs the question: What makes these teams perennial powerhouses? Why is there this supposed upper echelon of teams each year that seems like it rarely changes? As an avid college basketball fan myself, I wanted to explore two specific questions. What are the key components of being a winning team in college basketball, and is there really an upper tier of teams that never really changes? This intro to exploratory data analysis will help answer those questions.</p>

### Ethical Scraping Practices

Data is necessary for everyone from players to general managers if they want to draw conclusions about how to win. While available almost everywhere, you have to be careful and mindful about how you go about collecting data. When scraping data or using APIs, it is important to understand the rules and regulations in place from where you are scraping or pulling data. Pay close attention to the terms of whatever site you are using to collect your data.

In this case, the data and statistics were scraped from [Sports Reference](https://www.sports-reference.com/cbb/schools/#all_NCAAM_schools), an online repository for sports statistics. It is free to scrape and available to the public, with the only caveat being a citation necessary. You can find that citation at the bottom of the page. Ultimately, the most important idea to keep in mind is be familiar with the guidelines your specific website is requesting.

<figure>
	<img src="https://a.espncdn.com/photo/2024/0225/r1295805_1296x729_16-9.jpg" alt=""> 
	<figcaption>Fans storming the court. Source - ESPN.com</figcaption>
</figure>

Before we begin collecting the data, it's important you understand the magnitude of this question. This is an image of fans storming the court after beating a higher ranked rival team. Clearly, there is passion and emotion coming from everyone there. From the players to the coaches to the fans, everyone wants to win and have these magical moments. The question is, how can our favorite team continue winning?

### Collecting the Data

While all of the statistics we are looking for are right in the website and ready to be scraped, it is important to understand the basics behind what is actually happening within the code. We will be using BeautifulSoup to scrape our desired statistics, and their documentation can be found [here](https://www.crummy.com/software/BeautifulSoup/bs4/doc/). On the page we want to scrape, there are two tables. One is for Men's College Basketball and the other is for Women's. In this specific analysis, we are looking at just men's statistics, so taking advantage of the BeautifulSoup package, we grab the first table.

{%- highlight python -%}
url_teams = 'https://www.sports-reference.com/cbb/schools/#all_NCAAM_schools'
r_teams = requests.get(url_teams)

soup_teams = BeautifulSoup(r_teams.text)
table = soup_teams.find('table', id="NCAAM_schools")
#=> grabs the table specifically for NCAAM.
{%- endhighlight -%}

Then, we want to pull out just the text from the table. Many team names and statistics have hyperlinks, which we want to avoid.

{%- highlight python -%}
#We start with this code to pull out the header titles for each column
header_row = table.find('thead').find_all('tr')[0]
headers = []
for title in header_row.find_all('th'):
    headers.append(title['data-stat'])
headers = headers[1:]

#Collect all the rows in the table
rows = table.find('tbody').find_all('tr')

table_data = []

for row in rows:
    cells = row.find_all('td')
    row_data = []
    
    #This for loop adds just the text of the row into row_data
    for cell in cells:
        row_data.append(cell.text.strip())
    #Add the row data to our whole table
    table_data.append(row_data)

#Now we can create a dataframe with our text we have scraped
df_teams = pd.DataFrame(table_data, columns=headers)
{%- endhighlight -%}

With just this code, you already have a dataframe you can work with in Python! It's as easy as that. This specific table had just data on each team's all time statistics, so we also scrape [this page](https://www.sports-reference.com/cbb/seasons/men/2024-school-stats.html) for data specific to this past season. A more in depth look at scraping then merging the two dataframes can be found at [my repository](https://github.com/KeepTheBarlow/Data-Curation-Project).

### A Look at the Data

After having scraped our two desired tables and merged them together, we have a dataframe consisting of each team with their all time statistics, as well as statistics from this most recent year. For those of you who aren't basketball fans, I will provide a quick breakdown of what the more confusing columns in the dataframe represent.

* SRS = "Simple Ranking System". It's a very basic metric to rank teams
* SOS = "Strength of Schedule". Measures how difficult a team's schedule is.
* FG = "Field Goal". Any shot that isn't a free throw in basketball.
* 3P = "Three Pointer". Specifically a three point shot.
* FT = "Free Throw". An undefended shot taken after a foul.
* Reb = "Rebound". Grabbing the ball after a missed shot.

There are 361 teams (rows) and 45 columns (the team name then 44 statistics about the team). Some interesting summary statistics can be found using

{%- highlight python -%}
#Create a table of mean values of each numeric column
mean_values = complete_df.mean(numeric_only=True)

mean_df = mean_values.to_frame().T
mean_df
#=> prints a one row table of the mean of each column
{%- endhighlight -%}

<table border="1" class="dataframe" style="width:100%; border-collapse:collapse; margin:20px 0;">
  <thead>
    <tr style="text-align:center;">
      <th style="padding:8px; border:1px solid #ddd; text-align:center;">NCAAFinalFourCount</th>
      <th style="padding:8px; border:1px solid #ddd; text-align:center;">FGPct2023</th>
      <th style="padding:8px; border:1px solid #ddd; text-align:center;">3PPct2023</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="padding:8px; border:1px solid #ddd; text-align:center;">0.930748</td>
      <td style="padding:8px; border:1px solid #ddd; text-align:center;">0.445152</td>
      <td style="padding:8px; border:1px solid #ddd; text-align:center;">0.338787</td>
    </tr>
  </tbody>
</table>

Of all the means, what stands out to me the most are the average number of Final Fours reached by each team (0.93), the average Field Goal Percentage in 2023 (0.445), and the average Three Point Percentage in 2023 (0.339).

We see that the average team hasn't even made it to one Final Four, and we can see that the average shot in college basketball over the course of a whole season is actually more likely to miss.

### Answering our Questions

Now that we have our data and some interesting summary statistics, the questions that inspired this data collection can be answered. To begin, we can look at what variables inpact winning the most in a given season. Creating a correlation heatmap can tell us about which variables are closely related.

<figure>
    <img src="{{ '/assets/img/corr_heatmap.png' | relative_url }}" alt="">
    <figcaption>Figure 1. - Correlation Heatmap of 2023 Season Stats</figcaption>
</figure>

Obviously, winning percentage is highly correlated with variables like points or SRS (the simple ranking system). However, what's interesting to note is that there is a much stronger correlation with rebounds and assists (0.62 and 0.67) than with steals and blocks (0.35 and 0.35). There is a common adage in the basketball world that "defense wins championships", but this data seems to suggest that offensive statistics play a bigger role in winning than do defensive statistics.

To answer our other question of if there is an elite tier in college basketball, we can look at the relationship between number of all time NCAA tournament appearances (the biggest tournament in college basketball) and winning percentage in 2023.

<figure>
    <img src="{{ '/assets/img/ncaa_apps.png' | relative_url }}" alt="">
    <figcaption>Figure 1. - Scatterplot of the relationship between tournament appearances and win % (2023)</figcaption>
</figure>

According to the scatterplot, there is a obvious trend showing that the total number of tournament appearances all time is positively related with win percentage, even in one given season. This would suggest there is in fact an elite tier in college basketball, and even if the specific teams may vary slightly from year to year, you can always expect the traditionally "great" teams to win many games.

### Conclusion

Overall, we have seen how to ethically scrape data from a website into a dataframe. In addition, we have seen how exploratory data analysis can help us answer our questions we have about the data. The conclusions made were that offensive statistics tend to have a higher correlation with winning percentage than do defensive statistics and that there does appear to be an upper echelon of teams that consistently win games and make it to the biggest stage in college basketball. As you watch your favorite team this year (Go BYU!), pay close attention to how exactly they are winning games!

For a deeper look into more specifically how the tables were scraped and merged, as well as other EDA plots and their code we didn't have the time to get into, feel free to check out [my repository](https://github.com/KeepTheBarlow/Data-Curation-Project). Try webscraping out yourself on a topic that sounds interesting to you and watch how the data can come to life!

Citation:
Sports Reference LLC. College Basketball at Sports-Reference.com - College Basketball Statistics and History. http://www.sports-reference.com/cbb/. (11/13/2024)

