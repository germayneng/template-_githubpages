---
title: "Monty Hall Simulation"
excerpt: "Two apps for Monty Hall Game and Simulation, along side a report for the Simulation."
header:
  teaser: montyhall.png
gallery:
  - url: montyhall-sim.png
    image_path: montyhall-sim.png
    alt: "Screenshot of the Application for the Monty Hall Simulation"
---

To understand this work we will see the motivation and the actual simulation with its results.

---

## Motivation

The Monty Hall Problem is a very interesting one and can be considered a probabilistic brain teaser. It can be defined as follows:

> Suppose you're on a game show, and you're given the choice of three doors: Behind one door is a car; behind the others, goats. 
> You pick a door, say No. 1, and the host, who knows what's behind the doors, opens another door, say No. 3, which has a goat. 
> He then says to you, "Do you want to pick door No. 2?" 
> Is it to your advantage to switch your choice?

Basically, after your first door choice, the host choses one door with a goat and asks if you want to change door. The main question is: what gives a higher probability of winning? switching door or not switching?

The brain teaser comes when calculating the probability of winning after switching. Since we end up with two doors after the host opens one, people tend to think that the probability of winning is 1/2 by switching or not. But actually the probability of winning by switching is 2 times (2/3) bigger than the probability of winnning by not switching doors (1/3).

In such cases where we might not be sure about the probabilities, a simulation might be useful to confirm our findings.

---

## Simulation

The idea is to observe the differences of switching or not switching door choice after the host shows one of the three doors. We will see these differences in terms of distributions of probabilties, and also mean, standard error and variance of probabilities, for each scenario (switching and not switching).

For this simulation I created two apps and a report. The report shows all the code used with the explanation of what it does. The first app allows different simulations with the results and the second app is the game itself.

{% include gallery caption="Screenshot of the Application for the Monty Hall Simulation." %}

The links for the apps and the report are below. All the code is shared on github.

* Report for the simulation: <a href="http://rpubs.com/ricardosc/MontyHall/" target='_blank' class="btn btn--info btn--small">Monty Hall Simulation Report</a>
* App for the simulation: <a href="https://ricardosc.shinyapps.io/MontyHallSim/" target='_blank' class="btn btn--warning btn--small">Monty Hall Simulation App</a>
* App for the game: <a href="https://ricardosc.shinyapps.io/MontyHallGame/" target='_blank' class="btn btn--warning btn--small">Monty Hall Game App</a>

For more information about the Monty Hall problem, go to <a href="https://en.wikipedia.org/wiki/Monty_Hall_problem" target='_blank'>"Wikipedia - Monty Hall Problem"</a>.
