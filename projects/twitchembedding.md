---
title: "Text Embedding for Twitch Emotes"
layout: archive
---
It's not crazy to think of Twitch emotes as emoticons and emojis. Despite not having a movie, within the gaming community, Twitch emotes have become colloquial. It's pretty common to hear the use of the word "Pog" when I'm talking to friends on Discord. And when coupled with the images from twitch emotes, you can start getting some context as to what these emotes mean.

To learn these embeddings I've decided to use a [dataset from Harvard Dataverse](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/VE0IVQ) made by Kim, Jeongmin. It scraped the chat logs of 2162 streaming videos by 52 streamers between 2018-04-24 to 2018-06-04.

The big step at the moment is to clean the data. I have some ideas as to how to approach the embedding. I've tried a preliminary GloVe embedding to no avail, as it was on roughly tokenized text without any further processing. Most of the instances of the emotes were in single-word messages with only the emote and no context, or spammed heavily with, once again, no context. This makes finding instances where the emote is used with valuable surrounding context a necessary endeavor. Cleaning and processing this data will be crucial in being able to learn anything from it.

An alternative embedding could follow from paper [emoji2vec](https://arxiv.org/abs/1609.08359). It learns an embedding as a linear combination of already-present word vectors. This is learned through classifying the correct emoji-description pairs. The difficulty in applying a similar method here is that Twitch emotes don't have a default description as do emojis. The words are meaningless and is used entirely based on situational context. Maybe curating a dataset by having many people describe the emotes and create an average description could be a step in a meaningful direction.

As there are many problems with this at the moment, I'm still working on trying to figure out what is the best approach. I'll be working on cleaning up the data and hopefully build something on top of that.
