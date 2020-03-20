# Coronavirus Simulation with a Very Simple Model

![](https://cdn-images-1.medium.com/max/2578/1*9-f6d9JZHX6zGo0ENk6OIg.jpeg)

### If _Leonardo Da Vinci_ was alive today and saw _Mona Lisa_ wearing a surgical mask, he probably would have been shocked… and stolen the mask for himself!

Jokes aside, the Coronavirus outbreak has already caused lots of suffering. It has the potential to become one of the deadliest pandemics ever. Many estimates predict millions of deaths by the end of 2020.

What causes me unnerve is the number of people, especially politicians, who do not take this seriously. For instance, this morning I saw a supposed “_professor”_ on national Russian TV say we should not do anything about this pandemic saying that seasonal flu kills more people than **COVID19** has. Later in the afternoon, I heard of my acquaintance throwing a large-scale party…

So I spent the last two days writing a simulation in Python to hopefully explain what _actually_ is going on.

_Should we care at all? Is seasonal flu more dangerous? Why do we need to self-isolate?_

![Photo by [Kelly Sikkema](https://unsplash.com/@kellysikkema?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/8580/0*dGK0njUbTPz-RyQj)

# Average Rate

What I call _average rate_, epidemiologists call _basic reproduction number_ (https://en.wikipedia.org/wiki/Basic_reproduction_number). Barring some technicalities, all it really means is how many people catch the virus from an infected person assuming nobody developed an immunity.

As of now, it’s not clear what’s the _average rate_ for COVID19. Most reports quote it as somewhere between 2–4. So I assumed it’s 3 initially. Why do I mention _initially?_

Well, because when the number of cases rises, governments start imposing bans — and sometimes complete lockdowns — and people start self-isolating.

> The average rate starts off high but eventually reaches some number which I call the **final average rate**.

![Average Rate Decreases until Convergence](https://cdn-images-1.medium.com/max/1820/1*iwyoVIdKbOTvyghzV13u6Q.png)

This number depends on how strongly governments impose bans and the social responsibility of its citizens; when the latter is strong, the _final average rate_ is lower (_people spread the virus in smaller numbers_).

I compared the spread and number of deaths from the *final average rate* in my model. (_We will come to it in a bit_).

The above figure shows the _average rate_’s dependence on the number of active cases in my model. It makes sense: when the active cases are large, governments impose stronger bans, people start to panic and stay at home.

# Model

_NOTE: Skip this part and move to “Results” section if you don’t want to understand the technical details of the model._

We start with 3 infected people and ignore incoming and outgoing cases (_assume closed borders_) and only focus on the spread of the virus inside the country. Here are the most important parameters I used in the model.

#### Parameters

**_Initial Average Rate_ =** 3

**_Death Rate_** = 3.0% 

**_Population_** = 3,000,000 (Armenia)

**_Healthcare Capacity_** = 5 bed for 1000 people

**_Percentage of Infected People who need Serious Medical Care =_** 14%

**_Percentage of Infected People who Develop Immunity =_** 80%

Note that I used Armenia's population but all the results are qualitatively the same!

We also vary the **_final average rate_** and find the dependence for different values.

![Parameters from the Python Code. (NOTE: If this confuses you, ignore it). ](https://cdn-images-1.medium.com/max/2074/1*lL8bP96LH557WvzJvk_qQA.png)

The model is simple but surprisingly works well.

On any given day, we have _new daily cases_. To calculate this, we use the current day’s *average rate* to first find the probability someone gets infected — this is simple to do. We then multiply this fraction by the number of people who can still get infected — the number of people who are not dead, have not developed perfect immunity and are not sick.

We also have people who either _die_ or _recover_. I assume that people who got sick exactly 14 days ago either die or recover. To calculate which fraction dies, I use the recovery rate. However, if the number of people who need medical care is higher than the medical capacity, the fraction of deaths is higher than the death rate of 3.0%.

_(NOTE: Don’t worry if you are lost here. Read the code and it would make more sense.)_

The Python code for it is in the _Coronavirus Simulation_ file.

# Results

The picture below shows the results for different values of _final average rate._

Intuitively speaking this makes sense. Initially, the number of active cases rises exponentially. You infect some people, they themselves infect others and so on: it’s like a chain reaction. When the number of cases grows too large, many people develop immunity towards the virus and do not get reinfected. 

Looking at the plot, it’s clear that with stronger social distancing, the peak (_highest value_) of the curve is lowered and the curve is delayed. (You may have heard “_flattening_” or “_spreading out_” the curve. This is exactly what happened here). Why do we care about _flattening_ the curve?

![](https://cdn-images-1.medium.com/max/1838/1*sWxjat7YJVQ_KgHLdEm6cw.png)

#### Lowering Peak

Unfortunately, there are a limited number of doctors and nurses so treating every patient is difficult. The black horizontal line in the graph is the _healthcare capacity._ The higher the peak is, the more people will be unable to get adequate treatment. (**_NOTE:_** _the black line’s position is arbitrary. I simply put it there to illustrate my point. In reality, it’s much lower than that._)

This what happened in **_Wuhan_** when the death rate was close to 20% and is what’s happening now in **_Italy_**. Hospitals are overwhelmed and patients who need treatment are left out. (_We will examine the effects of the healthcare capacity shortly)._

![Photo by [Macau Photo Agency](https://unsplash.com/@macauphotoagency?utm_source=medium&utm_medium=referral) on [Unsplash](https://unsplash.com?utm_source=medium&utm_medium=referral)](https://cdn-images-1.medium.com/max/7048/0*4BCj9RqRVGrxAIO_)

#### Delaying Peak

**1.** It gives us time to find the vaccine. Many companies are already working towards the vaccine so delaying the peak by as much as possible gives us a higher chance of finding the vaccine before many deaths happen.

**2.** It would give more time for researchers to understand the virus and hence prepare better guidelines and possible treatments.

**3** By delaying the peak, governments have time to quickly increase the healthcare capacity. In fact, there are many hotels in the UK that are already being transformed into hospitals. In Armenia, they are also making a building for coronavirus patients.

# The Outbreak Is Only Just Starting

Let’s check where on the graph we are. As of _19 March_, Armenia has _122_ confirmed cases. The below graph is the zoomed-in version of the above one. We place our **_“WE ARE HERE!!!”_** around x = 3 weeks and y = 120 confirmed cases.

![](https://cdn-images-1.medium.com/max/1814/1*4T97eJgKiHaNLR3b0otEZg.png)

Note that most countries are in a similar position. Let’s zoom out a bit more.

![](https://cdn-images-1.medium.com/max/1826/1*8ACAmHSGwl7B7yRLKl5x8g.png)

Hmmm… seems like we have a long way to go. Let’s zoom out just a little bit more.

![](https://cdn-images-1.medium.com/max/1838/1*8APCUUk1-FIvujkbr5vrgA.png)

Okay, we are there!

### The outbreak is only just beginning. Comparing the number of deaths NOW is not fair because most deaths are going to happen in the future.

Saying it has fewer deaths than seasonal flu is like saying “_Summer in 2020 had fewer days than Winter._” Yeah. Because Summer is yet to come

But in the case of the virus, it’s not summer that’s coming.

# Number of Deaths

What we really care about is the number of deaths and not the number of active cases. So let us plot the dependence of number of deaths depending on other parameters.

#### Final Average Rate

From the above plots, it is clear that lower values of _final average rate_ lower the active cases and therefore should lower the number of deaths too.

Here is the plot of number of deaths in a year from the _final average rate_. One year is approximately the expected time until we find a vaccine so it makes sense to only track the number of deaths for only one year.

![](https://cdn-images-1.medium.com/max/1826/1*Lvb-itF-nUxDatM9BoVhLw.png)

As expected, when social distancing is strong the number of deaths plummet massively. In other words, if everyone cut their social interactions by 3 — making the _final average rate_= 1.0 — the number of deaths would decrease by more than **50x** !!!

Also, note that if strong action is not taken and the rate is, say, 1.2 the number of deaths equals about **30,000** which is **1%** of the entire population of Armenia.

#### **Percentage of Infected People who Develop Immunity**

Let's now check the dependence of the number of deaths from the fraction of people who develop full immunity. This is out of our control but is still important to understand.

![](https://cdn-images-1.medium.com/max/1826/1*vrbv5DGrFHlcWyEp541p4Q.png)

As we expect, the higher the fraction is the lower are the number of deaths. In the critical case of only **10%** of people developing full immunity, the number of deaths rises to **500,000**. _(NOTE: don’t be scared. 10% is very unlikely and I fixed the **final average rate** = **1.4** which is worse than what we can achieve by self-isolation)._

#### Healthcare Capacity

Let’s now check how much the healthcare capacity changes the number of deaths.

![](https://cdn-images-1.medium.com/max/1832/1*KZTFeHxe1lrJha5rKhzscA.png)

We see that the number of deaths decreases when the healthcare capacity increases. This is expected of course.

# What does this mean for me?

> Stay home.

### Stay home.

**_Stay home._**

It is important to **stay home** if you can do so. Avoid social contact. Don’t go to parties and say “_coronavirus is not as deadly as the flu.”_

Every data there is shows that it is.

Try to work from home if you can. Yes, an 18-month quarantine will not work — it will completely screw up the economy and people need to eat.

But some self-isolation is better than none! You don’t need to go to parties to have a good economy.

And, at least in my book, “_avoiding the death of others_” beats “_party all day all night, dawg_”.

#### Final Remarks

The model is not to be used to predict or make decisions. As you may have noticed, I made lots of approximations that are not true in real life. This is a straightforward and simple model — the aim of which is to understand general patterns and tweak a few parameters here and there to see what happens.

In fact, for some values the model was unstable (did not work properly).

Machine Learning algorithms need to be used to understand the actual parameters, make more complex simulations and improve the underlying assumptions.

**_If this managed to change your mind, please share this article. Or at least use the arguments here to convince your friends to stay home._**
