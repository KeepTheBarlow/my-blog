---
layout: post
title:  "Automatic Speech Recognition using Machine Learning"
date:   2024-10-04
description: A brief tutorial on how to leverage Machine Learning and ASR to transcribe audio files.
---

<p class="intro"><span class="dropcap">A</span>udio is becoming more and more prevalent in the world or technology. With all the new inventions such as Siri, Alexa, or other home devices, as well as transcripts of customer service calls, dictated notes, and real-time language translation, being able to work with audio and transcribing it is very important. In this blog post, I will talk about why working with audio is important, some difficulties that may arise when working with it, some basic techniques, and finally, provide a tutorial for you to be able to transcribe your own audio files.</p>

### Why Audio?
Data is the new buzz word in the technology world and has been for a while. Many companies think the more data that can be gathered, the better. With this push for new data and new insights, data is out there in modalities, or specific types of data, that haven't been explored as deeply. Being able to work with audio, video, and other modalities instead of just numerical or text data is the way of the future and will drive insights not previously possible to be made with traditional methods.

### Problems with Audio
Computers and machine learning models are able to work with numerical and text data fairly well. Forecasts can be made, text analyses can be run, and that is what has made text and numbers so important for companies. However, the technology to work with audio and video, especially when it comes to machine learning, has grown exponentially over the past couple of years, and as AI models get bigger and bigger, the need to be able to handle audio, images, and video is just that much more important. For Automatic Speech Recognition (ASR) specifically, the challenge becomes training a ML model to be able to accept audio files or waves as input and output the corresponding text. Numbers and words are fairly constant when compared to audio. Examples of variations in audio could be:
* Different speakers
* Accents
* Pauses or punctuation in the audio that may not correspond to exact words
* Background Noise

All of these inconsistencies can make training an ASR model very difficult.

### Basics of Training an ASR Model
This tutorial isn't meant to be an in-depth explanation on how to train a ML model from scratch. There are much better examples and tutorials out there. However, I will go over the basics just so everybody is on the same level. Take, for example, a ML model that summarizes text (meaning the input is some text block and the output is the summary of the inputted text). The inner workings of the model cannot work with the text directly, so the words are passed into a "transformer encoder" that gives a representation of the words as a vector of numbers using math beyond the scope of this tutorial. The vector of numbers then is passed through the "transformer decoder" that takes the various vectors and hopefully prints out a summary of the text. At the beginning, the weights or parameters of the encoder and decoder are randomized, so the vector of numbers is more or less random and the output summary is more or less gibberish. That gibberish is compared to a human-given summary of the text, measured to see how close it is (using some sort of metric like Mean Squared Error), then based off that metric, the parameters of the encoder and decoder are updated. Over hundreds of thousands or even millions of examples, the model will slowly learn until its output is very similar to the human-written summaries.

The same process applies to an ASR model. The audio waves are passed in to the encoder, encoded into numbers using complicated math, then decoded into text. Over a lot of training, the encoder and decoder are able to communicate such that the vectors of numbers correspond accurately with the words being said, and thus, the transcription of the audio is output. While there are some complications mentioned above, the more comprehensive the training data is, the better the model will be.

### Picking a Model using HuggingFace
Training any sort of Machine Learning model from scratch can be very costly and time-intensive, especially those working with audio. Luckily enough, many people have already created highly accurate models that can be found on HuggingFace. According to their website, HuggingFace is a "collaborative platform and community that helps users build, train, and deploy machine learning (ML) models”. On their website, you can find pre-built ML models and datasets that can be deployed very quickly and easily as I will show. For this example, we will be using the Whisper Large Turbo ASR model from OpenAI, the same company that built ChatGPT

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

