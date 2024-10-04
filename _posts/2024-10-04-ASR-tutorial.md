---
layout: post
title:  "Automatic Speech Recognition using Machine Learning"
date:   2024-10-04
description: A brief tutorial on how to leverage Machine Learning and ASR to transcribe audio files.
---

<p class="intro"><span class="dropcap">A</span>udio is becoming more and more prevalent in the world or technology. With all the new inventions such as Siri, Alexa, or other home devices, as well as transcripts of customer service calls, dictated notes, and real-time language translation, being able to work with audio and transcribing it is very important. In this blog post, I will talk about why working with audio is important, some difficulties that may arise when working with it, some basic techniques, and finally, provide a tutorial for you to be able to transcribe your own audio files.</p>

## Why Audio?
Data is the new buzz word in the technology world and has been for a while. Many companies think the more data that can be gathered, the better. With this push for new data and new insights, data is out there in modalities, or specific types of data, that haven't been explored as deeply. Being able to work with audio, video, and other modalities instead of just numerical or text data is the way of the future and will drive insights not previously possible to be made with traditional methods.

## Problems with Audio
Computers and machine learning models are able to work with numerical and text data fairly well. Forecasts can be made, text analyses can be run, and that is what has made text and numbers so important for companies. However, the technology to work with audio and video, especially when it comes to machine learning, has grown exponentially over the past couple of years, and as AI models get bigger and bigger, the need to be able to handle audio, images, and video is just that much more important. For Automatic Speech Recognition (ASR) specifically, the challenge becomes training a ML model to be able to accept audio files or waves as input and output the corresponding text. Numbers and words are fairly constant when compared to audio. Examples of variations in audio could be:
* Different speakers
* Accents
* Pauses or punctuation in the audio that may not correspond to exact words
* Background Noise
All of these inconsistencies can make training an ASR model very difficult.

## Basics of Training an ASR Model


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

