---
layout: post
title: Detecing Bots using ChatGPT - Project Overview
date: 2024-10-17 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: chatgpt.avif # Add image post (optional)
categories: [Machine Learning]
tags: [ChatGPT, AI, Twitter, Bot, Topicmodeling, LDA] # add tag
---

## Project Collaboration with Ruth, a PhD Candidate in Communication at Misgihan State University

Recently, I had the honor of joining a project with Ruth, a PhD candidate in Communication at Misgihan State University.

**The Rise of AI Technology**

These days, AI technology is expanding rapidly. The former CEO of Google even mentioned that without advancements in AI, companies might not have a future. Thanks to AI tools like ChatGPT, many people now use them for coding, writing, and solving various questions. I can’t deny that I’ve also received help from ChatGPT while coding. I believe using AI tools is a good thing. While it’s important to have a strong foundation in learning, in a fast-paced world, asking ChatGPT for help instead of searching through every Stack Overflow post can sometimes be more efficient. However, we still need to study and have the basic knowledge to judge whether the answers we get from AI are correct.

**Exploring the Bot Problem**

Recently, social and political debates often arise on platforms like Twitter and Instagram. I've sometimes wondered if certain repetitive negative comments on Instagram were made by bots, not real people. In fact, research shows that bots on Twitter play a significant role in shaping public opinion, especially in political and social issues.

Whether or not bots should be regulated is another issue. What’s clear is that people need to be able to recognize whether they’re interacting with bots. But in reality, it’s not easy to tell if a random Twitter account is a bot or not.

**Project Overview**

In this project, we tried to see if bots could be detected using an existing AI tool. We provided the AI with four types of information to help determine if a user was a bot:

1. Account Information: This includes details like the account name, verification status, how long the account has been active, number of followers, people followed, and total tweets posted.
   
2. Text Information: The content of five tweets from the user is analyzed to decide whether the account is a bot or a real person.

3. Time Information: This involves looking at the patterns of when the user posts tweets, such as which days they tweet, what time of day they’re active, and the time gaps between tweets.

4. Social Interaction: This includes things like the percentage of tweets that are retweets, how often they mention other users, and a list of accounts they retweet or mention.

We gave ChatGPT these four types of data and tested how accurately it could detect bots.

**My Role and Contributions**

In this project, my main role was cleaning and organizing the data we got from the ChatGPT API. I used this data to calculate accuracy and other performance metrics, then compiled these findings into a report. I also looked into the explanations given by ChatGPT for its decisions and used a method called LDA (Latent Dirichlet Allocation) to analyze which topics came up most often in different cases, such as false positives, false negatives, and correct predictions. I’ll go into more detail about the LDA analysis in my next post.