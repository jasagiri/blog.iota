https://iota-untangled.com/algorithms-inspired-swarm-behaviour/

# Algorithms inspired by swarm behaviour

By Hanna van Sambeek
In Biomimicry, Hackathon support, Machine Ecosystems
26 March 2018
3 Min read
1 comment
<!--
With autonomous machines you almost automatically touch on swarming. But what is swarming? There are two ways of looking at it: how and why. By imitating the how, we might get some nice optimizations, but the why is where the real benefits are.
-->
自律型機械では、ほぼ自動的に「群衆」に触れます。しかし、群衆とは何でしょうか？２つの見方があります：方法と理由です。方法を真似ることで、いくつかの素晴らしい最適解が得られるかもしれないですが、本当のメリットはなぜかという点にあります。

## Locust preventing collisions
<!--
[Locust](https://asknature.org/strategy/collision-detection-in-a-swarm/#.Wq-llGbWAWo) filter out excess stimuli to have enough brain capacity to react to relevant signals. It only recognizes movements that will interfere with its flight path. In other words, it only pays attention to objects moving directly toward it, rather than things moving around it. Its eyes still see everything but only relevant movements are converted to signals that go to the movement detection parts of the brain. That way it only needs a fraction of processing power to perform the same task – avoid collisions.
-->
Locust](https://asknature.org/strategy/collision-detection-in-a-swarm/#.Wq-llGbWAWo)は、過剰な刺激をフィルタリングして、関連する信号に反応するのに十分な脳の容量を持っています。自分の飛行経路の邪魔になるような動きだけを認識します。言い換えれば、それはそれの周りを移動するものではなく、それに向かって直接移動するオブジェクトのみ注意を払っています。目はまだ全てを見ていますが、関連する動きだけが脳の動き検出部分に行く信号に変換されます。このようにして、衝突を避けるという同じタスクを実行するために必要な処理能力はほんの僅かで済むのです。

## Optimal growth paths of bacteria
<!--
[Bacteria](https://asknature.org/strategy/smart-swarming/#.Wri9UmaYMWq) gather information collectively to find the optimal path to growth. When an individual bacteria finds a successful path, it pays less attention to the signals from others. But when encountering resistance, the individual will increase its interaction with the group and learn from its peers. Based on confidence in their own information and decisions, bacteria can adjust their interactions with the group. This way, the group will optimize its path finding, following a very simple algorithm.
-->
Bacteria](https://asknature.org/strategy/smart-swarming/#.Wri9UmaYMWq)は、集団で情報を集め、成長に最適な経路を見つけます。個々の細胞は、成功した道を見つけると、他の細胞からのシグナルにあまり注意を払わなくなります。しかし、抵抗に遭遇すると、個体は集団との交流を増やし、仲間から学ぶようになります。自身の情報や判断に対する自信に基づいて、最近は集団との相互作用を調整することができます。このようにして、非常に単純なアルゴリズムに従って、グループはその経路探索を最適化します。

## Information sharing inspired by ants
<!--
In swarms, not all participants have to have the same role. Ants share information by having a few well-connected individuals. Most ants have only a few information sharing interactions, but a few ants have most inform sharing interactions. This gives them a very efficient [information sharing system](https://asknature.org/strategy/individuals-share-information/#.Wq-W5mbWAWo).
-->
群れの中では、すべての参加者が同じ役割を持つ必要はありません。アリは、いくつかのよく繋がった個体を持つことで情報を共有しています。ほとんどのアリは情報共有の相互作用が少ないですが、少数のアリはほとんどの情報共有の相互作用を持っています。これは彼らに非常に効率的な[information sharing system](https://asknature.org/strategy/individuals-share-information/#.Wq-W5mbWAWo)を与えています。

## Decentralized task switching in swarms
<!--
Not all participants in a swarm have to have the same function. And there doesn’t need to be a mastermind working hard to monitor every individual and predict the needs of the system. But how do you then balance the distribution of different functions in a decentralized way? Some ants, bees, termites and other social insects have simple rules for [task switching](https://news.stanford.edu/pr/96/960318insects.html). They respond to cues from the environment or actions of other individuals. One method is based on the interaction rate with others. For example, if ants do not meet enough food gathering ants compared to ants with other tasks (recognized by smell), they will switch to food gathering assuming there is a lack of ants with this task. This mechanism could be used in cases like autonomous cars, delivery drones, repair robots or any other machine that can fulfill multiple tasks.
-->
群れの参加者全員が同じ機能を持っている必要はありません。また、すべての個人を監視し、システムのニーズを予測するために必死に働く首謀者は必要ありません。しかし、分散化された方法で異なる機能の分配のバランスを取るにはどうすればよいのでしょうか？アリ、ハチ、シロアリ、その他の社会的昆虫には[task switching](https://news.stanford.edu/pr/96/960318insects.html)の簡単なルールがあります。彼らは環境や他の個体の行動からの合図に反応します。１つの方法は、他の個体との相互作用に基づくものです。例えば、他のタスク（匂いで認識）を持つアリに比べて、餌を集めるアリに十分に出会えなかった場合、このタスクを持つアリが不足していると判断して、餌を集めるタスクに切り替えます。この仕組は、自律走行車や配達用ドローン、修理用ロボットなど、複数のタスクをこなす機械のような場合にも応用できそうです。

## The purpose of murmurations
<!--
We know birds in a [murmuration](https://www.woodlandtrust.org.uk/blog/2018/11/starling-murmurations/) seem to move as one, but there is a slight delay through the swarm when you look closely, almost like a wave. In reality a bird actually observes only its closest 6 neighbours to make its decision. A joint movement in the right direction is adopted through the swarm in the blink of an eye (less than 0.1 sec) but “wrong” decisions are dampened with the same algorithm. This works very efficiently, but only in optimizing current implementations.
-->
私たちは、[murmuration](https://www.woodlandtrust.org.uk/blog/2018/11/starling-murmurations/)の中の鳥たちが一斉に動いているように見えることを知っていますが、よく見ると、群れの中には波のように僅かな遅れがあります。実際には、鳥は一番近い６つの隣人だけを観察して判断しています。正しい方向への共同行動は、群れを介してあっという間に（0.1秒未満）採用されますが、「間違った」判断は同じアルゴリズムで減衰されます。これは非常に効率的に動作しますが、現在の実装を最適化する場合に限ります。

<!--
We want to challenge you to look further, and observe the purpose of using a swarm; not just because it looks cool. Birds don’t expend huge amounts of energy to put on a show. They do it to gather to flock before nightfall, in order to stay warm as a group. Or they use it to fend off a predator, just as cattle and fish do. When you opt for a swarm-solution, how will it benefit the whole ecosystem, and not just now, but also in the future?
-->
私たちは、さらに目を凝らしてみて、「かっこいいから」という理由だけでなく、「群れ」を使う目的を観察してみたいと思います。鳥は見せびらかすために大量のエネルギーを消費することはありません。日が暮れる前に集まって群れを作り、集団で暖を取るためです。また、牛や魚のように捕食者から身を守るために使うこともあります。群れの解決策を選択した場合、それは現在だけでなく、将来的にも生態系全体にどのような利益をもたらすのでしょうか？

## Inspiration for Hackathon
<!--
This post is part of a series providing inspiration from nature for participants at the Blockchaingers Hackathon, specifically with the Machine Economy track in mind. Read more about:
-->
この記事は、Blockchaingersハッカソンの参加者に自然からのインスピレーションを提供するシリーズの一部で、特に機械経済のトラックを念頭に置いています。続きを読むには：

- [Biomimicry inspiration at the Deep Dive](https://iota-untangled.com/nature-inspiration-worlds-largest-hackathon/)
- [Importance of information in nature and in a Machine Economy](https://iota-untangled.com/biomimicry-information-machine-economy/)
- [Envisioning a new society](https://iota-untangled.com/envisioning-a-new-society/)
- [Emergence as a solution to overengineering](https://iota-untangled.com/emergence-solution-overengineering/)
- [Talking forests: inspiration for resilient machine ecosystems](https://iota-untangled.com/talking-forests-inspiration-for-resilient-machine-ecosystems/)
