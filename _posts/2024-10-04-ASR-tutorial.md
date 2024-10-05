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
Computers and machine learning models are able to work with numerical and text data fairly well. Forecasts can be made, text analyses can be run, and that is what has made text and numbers so important for companies. However, the technology to work with audio and video, especially when it comes to machine learning, has grown exponentially over the past couple of years, and as AI models get bigger and bigger, the need to be able to handle audio, images, and video is just that much more important. For Automatic Speech Recognition (ASR) specifically, the challenge becomes training an ML model to be able to accept audio files or waves as input and output the corresponding text. Numbers and words are fairly constant when compared to audio. Examples of variations in audio could be:
* Different speakers
* Accents
* Pauses or punctuation in the audio that may not correspond to exact words
* Background Noise

All of these inconsistencies can make training an ASR model very difficult.

### Basics of Training an ASR Model
This tutorial isn't meant to be an in-depth explanation on how to train an ML model from scratch. There are much better examples and tutorials out there. However, I will go over the basics just so everybody is on the same level. Take, for example, an ML model that summarizes text (meaning the input is some text block and the output is the summary of the inputted text). The inner workings of the model cannot work with the text directly, so the words are passed into a "transformer encoder" that gives a representation of the words as a vector of numbers using math beyond the scope of this tutorial. The vector of numbers then is passed through the "transformer decoder" that takes the various vectors and hopefully prints out a summary of the text.

At the beginning, the weights or parameters of the encoder and decoder are randomized, so the vector of numbers is more or less random and the output summary is more or less gibberish. That gibberish is compared to a human-given summary of the text, measured to see how close it is (using some sort of metric like Mean Squared Error), then based off that metric, the parameters of the encoder and decoder are updated. Over hundreds of thousands or even millions of examples, the model will slowly learn until its output is very similar to the human-written summaries.

The same process applies to an ASR model. The audio waves are passed in to the encoder, encoded into numbers using complicated math, then decoded into text. Over a lot of training, the encoder and decoder are able to communicate such that the vectors of numbers correspond accurately with the words being said, and thus, the transcription of the audio is output. While there are some complications mentioned above, the more comprehensive the training data is, the better the model will be.

<figure>
	<img src="https://huggingface.co/datasets/huggingface-course/audio-course-images/resolve/main/asr_diagram.png" alt=""> 
	<figcaption>Figure 1. - Visual ASR Model</figcaption>
</figure>

### Picking a Model using HuggingFace
Training any sort of Machine Learning model from scratch can be very costly and time-intensive, especially those working with audio. Luckily enough, many people have already created highly accurate models that can be found on [HuggingFace](https://huggingface.co/). According to their website, HuggingFace is a "collaborative platform and community that helps users build, train, and deploy machine learning (ML) models”. On their website, you can find pre-built ML models and datasets that can be deployed very quickly and easily as I will show. For this example, we will be using the [Whisper Large Turbo ASR](https://huggingface.co/openai/whisper-large-v3-turbo) model from OpenAI, the same company that built ChatGPT.

### ASR on your own
Now, the moment we've all been waiting for, I will show you how to utilize an ASR model and transcribe your own audio files. The Python code can be run on any machine utilizing Google Colab, a free way to use Python without any additional downloads. In addition, this code, along with more complicated use cases if you would like to go deeper, can be found at the [model's website](https://huggingface.co/openai/whisper-large-v3-turbo).

#### Installing the Correct Packages
For this model, the "torch", "transformers", and "accelerate" libraries from HuggingFace will be used. Again, all of this code can be run in a brand new Google Colab notebook with no additional downloads.

{%- highlight python -%}
!pip install --upgrade pip
!pip install --upgrade transformers  accelerate
#=> installs required libraries
{%- endhighlight -%}

#### Importing the Model
With the libraries installed, you can now import the model from HuggingFace using:

{%- highlight python -%}
import torch
from transformers import AutoModelForSpeechSeq2Seq, AutoProcessor, pipeline
from datasets import load_dataset


device = "cuda:0" if torch.cuda.is_available() else "cpu"
torch_dtype = torch.float16 if torch.cuda.is_available() else torch.float32

model_id = "openai/whisper-large-v3-turbo"

model = AutoModelForSpeechSeq2Seq.from_pretrained(
    model_id, torch_dtype=torch_dtype, low_cpu_mem_usage=True, use_safetensors=True
)
model.to(device)

processor = AutoProcessor.from_pretrained(model_id)
{%- endhighlight -%}

The specifics of this code are not super important, but what should be noted is that we are using the "openai/whisper-large-v3-turbo" model. That line can be changed to be any other ASR model on the HuggingFace website and this will still work.

#### Creating the Pipeline
Now, all that's needed is creating a pipeline.

{%- highlight python -%}
pipe = pipeline(
    "automatic-speech-recognition",
    model=model,
    tokenizer=processor.tokenizer,
    feature_extractor=processor.feature_extractor,
    torch_dtype=torch_dtype,
    device=device,
)
{%- endhighlight -%}

This pipeline allows us to call the function with our audio file and obtain the transcription.

{%- highlight python -%}
result = pipe("example_audio.mp3")
result
#=> Will give the corresponding text to what was said in the audio
{%- endhighlight -%}

It's as simple as that! Now, you have access to a powerful model trained on millions of examples with millions of parameters that can transcribe any audio for you. Incorporating this into a personal project, app, or website is very straightforward.

### Conclusion
What we went over:
* Importance of audio
* Why audio is hard to work with
* Basic overview of training a model
* HuggingFace overview
* Creating your own ASR Pipeline

A great resource for learning more about working with ASR and audio is [this course](https://huggingface.co/learn/audio-course/en/chapter0/introduction) on audio by HuggingFace. It is made for the beginner to intermediate level and will teach more in-depth about machine learning, utilizing audio, the transformer encoders and decoders, and other audial tasks that can be done with machine learning. In addition, following the tutorial on this post will give you a great baseline to leverage ASR for your own projects. Try it out to kickstart your audio machine learning journey!