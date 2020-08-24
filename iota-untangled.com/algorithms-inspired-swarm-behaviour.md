https://iota-untangled.com/algorithms-inspired-swarm-behaviour/

# Algorithms inspired by swarm behaviour

By Hanna van Sambeek
In Biomimicry, Hackathon support, Machine Ecosystems
26 March 2018
3 Min read
1 comment

With autonomous machines you almost automatically touch on swarming. But what is swarming? There are two ways of looking at it: how and why. By imitating the how, we might get some nice optimizations, but the why is where the real benefits are.

## Locust preventing collisions

[Locust](https://asknature.org/strategy/collision-detection-in-a-swarm/#.Wq-llGbWAWo) filter out excess stimuli to have enough brain capacity to react to relevant signals. It only recognizes movements that will interfere with its flight path. In other words, it only pays attention to objects moving directly toward it, rather than things moving around it. Its eyes still see everything but only relevant movements are converted to signals that go to the movement detection parts of the brain. That way it only needs a fraction of processing power to perform the same task – avoid collisions.

## Optimal growth paths of bacteria

[Bacteria](https://asknature.org/strategy/smart-swarming/#.Wri9UmaYMWq) gather information collectively to find the optimal path to growth. When an individual bacteria finds a successful path, it pays less attention to the signals from others. But when encountering resistance, the individual will increase its interaction with the group and learn from its peers. Based on confidence in their own information and decisions, bacteria can adjust their interactions with the group. This way, the group will optimize its path finding, following a very simple algorithm.

## Information sharing inspired by ants

In swarms, not all participants have to have the same role. Ants share information by having a few well-connected individuals. Most ants have only a few information sharing interactions, but a few ants have most inform sharing interactions. This gives them a very efficient [information sharing system](https://asknature.org/strategy/individuals-share-information/#.Wq-W5mbWAWo).

## Decentralized task switching in swarms

Not all participants in a swarm have to have the same function. And there doesn’t need to be a mastermind working hard to monitor every individual and predict the needs of the system. But how do you then balance the distribution of different functions in a decentralized way? Some ants, bees, termites and other social insects have simple rules for [task switching](https://news.stanford.edu/pr/96/960318insects.html). They respond to cues from the environment or actions of other individuals. One method is based on the interaction rate with others. For example, if ants do not meet enough food gathering ants compared to ants with other tasks (recognized by smell), they will switch to food gathering assuming there is a lack of ants with this task. This mechanism could be used in cases like autonomous cars, delivery drones, repair robots or any other machine that can fulfill multiple tasks.

## The purpose of murmurations

We know birds in a [murmuration](https://www.woodlandtrust.org.uk/blog/2018/11/starling-murmurations/) seem to move as one, but there is a slight delay through the swarm when you look closely, almost like a wave. In reality a bird actually observes only its closest 6 neighbours to make its decision. A joint movement in the right direction is adopted through the swarm in the blink of an eye (less than 0.1 sec) but “wrong” decisions are dampened with the same algorithm. This works very efficiently, but only in optimizing current implementations.

We want to challenge you to look further, and observe the purpose of using a swarm; not just because it looks cool. Birds don’t expend huge amounts of energy to put on a show. They do it to gather to flock before nightfall, in order to stay warm as a group. Or they use it to fend off a predator, just as cattle and fish do. When you opt for a swarm-solution, how will it benefit the whole ecosystem, and not just now, but also in the future?

## Inspiration for Hackathon

This post is part of a series providing inspiration from nature for participants at the Blockchaingers Hackathon, specifically with the Machine Economy track in mind. Read more about:

- [Biomimicry inspiration at the Deep Dive](https://iota-untangled.com/nature-inspiration-worlds-largest-hackathon/)
- [Importance of information in nature and in a Machine Economy](https://iota-untangled.com/biomimicry-information-machine-economy/)
- [Envisioning a new society](https://iota-untangled.com/envisioning-a-new-society/)
- [Emergence as a solution to overengineering](https://iota-untangled.com/emergence-solution-overengineering/)
- [Talking forests: inspiration for resilient machine ecosystems](https://iota-untangled.com/talking-forests-inspiration-for-resilient-machine-ecosystems/)
