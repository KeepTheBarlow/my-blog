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

Before we begin collecting the data, it's important you understand the magnitude of this question. This is an image of fans storming the court after beating a higher ranked rival team. Clearly, there is passion and emotion coming from everyone there. From the players to the coaches to the fans, everyone wants to win and have these magical moments. The question is how to continue winning?

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

Of all the means, what stands out to me the most are the average number of Final Fours reached by each team (0.93), the average Field Goal Percentage in 2023 (0.445), and the average Three Point Percentage in 2023 (0.339). We see that the average team hasn't even made it to one Final Four, and we can see that the average shot in college basketball over the course of a whole season is actually more likely to miss.

### Answering our Questions

Now that we have our data and some interesting summary statistics, the questions that inspired this data collection can be answered. To begin, we can look at what variables inpact winning the most in a given season. We filter the dataframe to include just the columns we want, then we can create a correlation heatmap as follows:

{%- highlight python -%}
#Create a correlation heatmap using only 2023 data
columns_2023 = [
    'Games2023', 'WinPct2023','SRS2023', 'SOS2023', 'Points2023', 'OppPoints2023',
    'FGPct2023','3PPct2023', 'FTPct2023', 'OffReb2023','TotReb2023', 'Assists2023',
    'Steals2023', 'Blocks2023', 'Turnovers2023', 'Fouls2023'
]

season_df_2023 = complete_df[columns_2023]

correlation_matrix = season_df_2023.corr()

plt.figure(figsize=(16, 12))
sns.heatmap(correlation_matrix, annot=True, cmap='coolwarm', center=0)
plt.title("Correlation Heatmap for 2023 Season Stats")
plt.show()
{%- endhighlight -%}

<figure>
    <img src="{{ '/assets/img/corr_heatmap.png' | relative_url }}" alt="">
    <figcaption>Figure 1. - Correlation Heatmap of 2023 Season Stats</figcaption>
</figure>


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
	<img src="https://a.espncdn.com/photo/2024/0225/r1295805_1296x729_16-9.jpg" alt=""> 
	<figcaption>Figure 1. - Fans storming the court. Source - ESPN.com</figcaption>
</figure>


{%- highlight html -%}
<figure>
	{% raw %}<img src="{{site.url}}/{{site.baseurl}}/assets/img/touring.jpg" alt="">{% endraw %}
	<figcaption>Figure 1. - This is an example figcaption</figcaption>
</figure>
{%- endhighlight -%}

