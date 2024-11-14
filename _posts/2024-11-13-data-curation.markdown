---
layout: post
title:  "The Art of Winning: A Dive into College Basketball Data"
date:   2024-11-13
description: Exploring what makes winners winners in college basketball, and why they stay that way.
---

<p class="intro"><span class="dropcap">C</span>ollege Basketball is one of the most thrilling sports to watch. Every school has a rabid student section who pack their arena night in and night out to make as much noise as possible. It seems like on any given night, upsets are bound to happen with teams you've never even heard of taking down perennial powerhouses. But that begs the question: What makes these teams perennial powerhouses? Why is there this supposed upper echelon of teams each year that seems like it rarely changes? As an avid college basketball fan myself, I wanted to explore two specific questions. What are the key components of being a winning team in college basketball, and is there really an upper tier of teams that never really changes? This intro to exploratory data analysis will help answer those questions.</p>



# Heading 1

## Heading 2

### Ethical Scraping Practices

Data is necessary for everyone from players to general managers if they want to draw conclusions about how to win. While available almost everywhere, you have to be careful and mindful about how you go about collecting data. When scraping data or using APIs, it is important to understand the rules and regulations in place from where you are scraping or pulling data. Pay close attention to the terms of whatever site you are using to collect your data.

In this case, the data and statistics were scraped from [Sports Reference](https://www.sports-reference.com/cbb/schools/#all_NCAAM_schools), an online repository for sports statistics. It is free to scrape and available to the public, with the only caveat being a citation necessary. You can find that citation at the bottom of the page. Ultimately, the most important idea to keep in mind is be familiar with the guidelines your specific website is requesting.

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
#=> prints 'Hi, Tom'.
{%- endhighlight -%}

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
	<img src="https://a.espncdn.com/photo/2024/0225/r1295805_1296x729_16-9.jpg" alt=""> 
	<figcaption>Figure 1. - Fans storming the court</figcaption>
</figure>


{%- highlight html -%}
<figure>
	{% raw %}<img src="{{site.url}}/{{site.baseurl}}/assets/img/touring.jpg" alt="">{% endraw %}
	<figcaption>Figure 1. - This is an example figcaption</figcaption>
</figure>
{%- endhighlight -%}

