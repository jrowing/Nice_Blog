---
layout: post
title: "Radioactive decay modeling with dice"
description: "A neat model of a random decay"
date: 2017-06-19
tags: [teaching, physics, radioactivity]
comments: true
share: true
---


# Exponential decay with dice

The classic high-school modelling of radioactive decay requires many dice, and a little patience.

While it is not possible to predict when any given radioactive nuclei will decay; it is possible to predict with a high degree of probability the average rate of decay for a large number of nuclei within a given sample. This is because the rate of decay for each type of radioactive isotope is a constant and is a characteristic or that given isotope.
The decay process is then a statistical process. The decay of a radioisotope is a random event.
That is, it is the decay of a given nuclei is not dependent on the environment of the nucleus nor its past history. One can then use statistical analysis to determine the probability of the rate of decay; likewise, one can use statistical analysis to determine the probability that a given die will roll a specific number
when tossed.
For dice, the probability that a specific number will be tossed is based solely on the number of sides the die has. For 6-sided dice, there is a 1 in 6 probability (chance) or rolling a 5 (or any of the numbers 1-6). For example, if one took one hundred 6-sided dice and rolled them all at once and
removed all of the 5s that were face up, then how many of the 100 dice would one expect to remove?

Since the probability of rolling a 5 is 1 in 6, then multiply 1/6 by 100. The result is 16.6 or since dice come in whole numbers about 16 or 17 dice would be removed. If 17 are removed from the original 100, there would be 83 remaining. One could then predict in the next roll that the number of dice that would land with the 5 face up would be 1/6 (83) or 13.8. Thus the rate of decay is constant and can be used to simulate radioactive decay

## Apparatus:
50 dice, dice thrower

## Procedure:

1.	Count 50 dice into the dice thrower and then cast the dice CAREFULLY onto the bench top.
This is throw number, t = 1 with dice number N = 50.
2.	Count and remove any dice showing a ‘6’. Replace the remaining dice back in the thrower.
3.	Repeat the above until there are less than six dice left.
4.	Repeat all of the above twice more.
5.	For each of your throw numbers (t) calculate the average number of dice before the throw (Nav)
6.	Tabulate your results under the headings:
Throw number (t); Average number of dice before throw (Nav); ln (Nav)

7.	The decrease in the number of dice left after each throw is analogous to the decay of unstable nuclei. Each throw number represents the passage of a certain amount of time, for example 1 second. A graph of ‘average dice after throw’ against ‘number of throw’ would look the same as a graph of ‘number of nuclei left’ against ‘time’ such as you should have come across at GCSE. From this graph you should know how to calculate a half-life value.

Use the code below to try it out:
<div class="sage">
            <script type="text/x-sage">
# -*- coding: utf-8 -*-
"""
Created on Thu Feb  1 10:29:18 2018

@author: joe
"""

# some library objects we need
import matplotlib as mpl
mpl.use('Agg')
from numpy.random import binomial, seed
from numpy import zeros, arange
from matplotlib import pyplot as plt
# initial population
P0 = 50
fig = plt.figure(figsize=(10, 8))
# number of rolls per experiment
n_rolls = 50

# number of experiments
n_exp = 1

# probability that any given die will "decay" on a given roll
p = 0.1

# location to track average dice remaining for each roll number
pop_avg = zeros(n_rolls+1)

# "seed" the random number generator
# (This makes the results look different
# each time the code is run.)
seed()

# loop over experiments
for n in range(n_exp):
    
    # reset the dice population
    P = P0

    # roll the dice
    for k in range(1,n_rolls+1):
    
        # figure out how many dice decay this time
        r = binomial(P,p)
    
        # remove the dice
        P -= r
    
        # update the average
        pop_avg[k] += P
    
# final division to compute the averages
pop_avg /= n_exp

# we always started with P0
pop_avg[0] = P0

# compute the model predictions
model = (1-p)**arange(n_rolls+1)*P0
pl1 = list_plot(pop_avg,plotjoined=True,marker='+',legend_label='averaged',axes_labels=['roll #', '# dice'])
pl2 = list_plot(model,plotjoined=True,linestyle='--',color='red',marker='x',legend_label='model')

show(pl1+pl2)

            </script>


8.	Plot a graph of ‘average dice before throw Nav’ against ‘number of throw, t’ and calculate the ‘half-life’ of the dice in terms of throws.
9.	Plot a graph of ‘ln (Nav)’ against ‘number of throw, t’.
	This graph should be a straight line of negative gradient.

10.	Measure the gradient of your second graph, it is equal to the NEGATIVE of the decay constant,  of the dice.
11.	Explain why you would expect the decay constant to equal 1/6th.
12.	See if your half-life value is equal to ln (2) /   as would be expected from theory.
13.	Why would this experiment would give better results if more dice were used?
14.	What would you expect your values of ‘half-life’ and ‘decay constant’ to be if:
	(a) dice with ‘5’ as well as ‘6’ were removed.
	(b) dice with ‘4’, ‘5’ & ‘6’ were removed.
