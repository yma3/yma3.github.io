---
title: "Path of Exile Currency Prediction"
layout: archive
---

Path of Exile (PoE) is an Action RPG made by Grinding Gear Games. Players have characters that kill monsters and farm loot, much like any regular RPG. However, the unique way Path of Exile handles currency is what drew me to create this project. By observing the data dumps from [poe.ninja](https://poe.ninja/), it's possible to perform time-series analysis on the data and create a forecasting model to predict the value of certain items given some previous history.

{: style="text-align:center"}

Example Data taken from POE Ninja
![POE Ninja](/assets/images/poedata/poeninja.png)

[Click here](#poeecon) to jump to the section explaining PoE economy.

# PoE Currency as Time Series Data

Time series data has 3 major components: trend, seasonality, and noise. The observed data is a superposition of these three components, and thus by understanding some of the behavior of each, we can start to build a model around how the system should behave.

### Seasonality

Due to the nature of PoE's development cycle, every 3 months, there is a new "league" that is introduced. This includes an economy reset. Thus, every season, the trends that are observed within each 3-month period begin all over again, thus creating the seasonality within PoE's economy. During the beginning of each season, the prices on items are extremely low, and they appreciate in value quickly within a few days to the first week to the first month. These seasonal fluctuations are what we aim to learn to take advantage of to make the most currency at the beginning of a new season.

### Trend

Trend is defined as the overall direction of the data without periodic fluctuations, and noise. For items in PoE, there is an internal upwards trend within the first week to first month of any new league. Prices tend to stabilize within that time period. On an even broader scale, there is a small observed trend that the prices of items are going up slowly, league by league. The true reason is fully known, but we expect due to an increase number of bots farming low level currency, it lowers the purchasing power of the base unit of money, the Chaos Orb, thus raising the prices of all the other goods.

### Noise

Noise is something that models can't truly model if it is indeed, random. We simply make our systems as robust to noise as we can. If a popular streamer decided to use a specific item, it could create an anomaly in the time series data. These are generally good times to trade those items, however I don't try to predict when those will occur. Simply leveraging the opportunity when it comes works best.

# Modeling the Prices of Exalted Orbs

There are a few items that are always known to be of value. The first is the Exalted Orb, a more expensive version of the Chaos Orb whose main purpose for traders is to perform large-scale bulk trades. Other items such as "The Nurse" or "The Doctor" are also analyzed, but I will be specifically referring to the prediction of the price of an Exalted Orb.

{: style="text-align:center"}

![Exalted Prices](/assets/images/poedata/exaltedpriceall.png)

I chose a series of models and tested between each to determine which was the most effective at modeling this time series data. The models chosen were a Naive Forecasting method, a moving average method, and a Recurrent Neural Network (RNN) method.

### Naive Forecasting
The naive method simply assumes that the price of tomorrow's prediction will be exactly the same as the going price today. Carrying this through the entire dataset, this method is realized as a single-day shift in the time-domain. (Blue is base, orange is predicted)

{: style="text-align:center"}

![NaiveForecast](/assets/images/poedata/naiveforecast.png)

The direct result is a mean squared error (MSE) of 60.46 and an mean absolute error (MAE) of 4.71. We use these metrics as our baseline to the models.

### Moving Average Forecasting
We can define a sliding window that averages the values across the last N-days. The expectation is that this will smoothen the data to provide a better trend. In the case where the window size is chosen to be N = 1, the model degenerates to the Naive Forecasting case. For any values greater than 1, we see a much smoother model.

{: style="text-align:center"}

![Moving Average Forecast](/assets/images/poedata/movingaverage.png)

Although the model seems to have an overall smoother trend, due to the nature of the moving average, during large rise sections such as the beginning, the model lags heavily behind. This model has an MSE of 93.28 and an MAE of 6.83. As the window size increases, these errors increase, thus, this moving average model performs worse than the simple naive model. Thus, we look to another type of model.

### Recurrent Neural Networks

Recurrent Neural Networks (RNNs) are a type of neural network that connects nodes through a temporal sequence. This allows for the networks to learn temporal behavior such as the seasonality and trends of data based on previous history. There are many different types of nodes that can be used to form the fundamental RNN. The model in the notebook uses a 1-D Convolution along with four LSTM layers. GRU layers were also tested with similar results.

The training set was data from all of the previous leagues (Before Delirium), from the previous 600 days. 510 days were used in training with the last 90 days of the most recently completed league at the time, Delirium, being used as the validation set.

The model was trained for 2500 epochs with the learning rate decreasing by 1/3 at set intervals. This seemed to perform best during training. The window size for the inputs were set to the past 5-days. Other values such as 3-days to 7-days were tested with 5 performing optimally.

The figure below shows the training of the model. Blue is training MAE, orange is validation MAE.

{: style="text-align:center"}

![Training Loss](/assets/images/poedata/trainingvalloss.png)
![Exalted RNN](/assets/images/poedata/exaltedrnn.png)

<a name="poeecon"></a>
### The PoE Economy

In Path of Exile, there is no such thing as "gold". There's no standard currency that all enemies drop, or that you get from quests. In Wraeclast, the world of PoE, players trade for items entirely on a barter system where the price of an item is subject to supply and demand, and the purchasing power of each player fluctuates with the amount of items in the market.

And with this economic system, the natural direction is to pick an item with enough value, yet common enough in all parts of this world to act as a defacto standard akin to our historic gold standard. PoE doesn't use "gold". We pay with "chaos."

Chaos Orbs are just a fancier name for a dollar. It's what the players and the devs have decided to be the base unit of currency. Everything regarding trade is built on this idea. Items are worth X-amount of chaos. Even an Exalted Orb, similar to a $100 bill, has its value determined in chaos by supply and demand. Sometimes they're worth 150+ chaos (150+ C), and other times they're worth 60C.

### Currency as a stock

You can imagine now that this Exalted Orb (1 Ex) is a stock that goes up and down in price. If we buy 10 Ex at 60C a piece, and then sell back at 150C, we've made a net profit of 90C per Ex. Buying low, selling high is the most basic form of trading. Alternatively, we can purchase items that start as low as 10C, and within a month or two, their price has grown 20 times, and are now worth 200C apiece. We can even invest in this form of economy.

With both the ability to trade and invest, there is enough similarity to how we approach PoE's economy to how we approach the real world economy to start using some of the same techniques. Somebody even started an [in-game hedge fund](https://www.youtube.com/watch?v=NcfNC2epV5Q) to make currency.

# References
Portion of codebase from [Tensorflow in Practice](https://www.coursera.org/professional-certificates/tensorflow-in-practice)

Data dumps from [poe.ninja](https://poe.ninja/)

Wiki pages on [LSTMs](https://en.wikipedia.org/wiki/Long_short-term_memory), and [GRUs](https://en.wikipedia.org/wiki/Gated_recurrent_unit)
