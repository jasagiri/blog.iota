https://iota-untangled.com/implementation-feeless-transaction-system/

# Implementing a feeless transaction system
By Hanna van Sambeek  In Machine Economy  8 December 2017  4 Min read  1 comment 
<!--
*One of the key features of IOTA is that there is no transaction fee. It is designed for micro transaction on the Internet of Things. This opens up a lot of possibilities (more on this in future posts).*
-->
*IOTAの大きな特徴は、取引手数料が無料であることです。これは、モノのインターネット上でのマイクロトランザクションのために設計されています。これは多くの可能性を開きます。（これについては今後の記事で）*

<!--
The problem however is, that as long as IOTA transactions are benchmarked against fiat money1 we are not able to reap the full benefits. Exchange rate risk premiums could counteract the feeless advantage of IOTA, until we have local IOTA transaction ecosystems.
-->
しかし、問題は、IOTA取引が不換紙幣とのベンチマーク1である限り、そのメリットを十分に享受できないことです。為替レートのリスクプレミアムは、ローカルなIOTAトランザクション・エコシステムを構築するまでは、IOTAの手数料無料のメリットを打ち消す可能性があります。

## It costs money to pay money
<!--
Fees are a given in our society. You might not notice it, but every monetary transaction you do has a fee, direct or indirect.
-->
手数料は、私たちの社会では当たり前のことです。あなたは気づかないかもしれませんが、あなたが行うすべての金銭的な取引には、直接または間接的に手数料がかかります。

<!--
You pay your bank a fee to transfer money (within a country or currency they might not charge an extra fee, but you do have to pay to have a bank account and have access to that service. The service costs of that account accommodate for that fee.) Money transfers to other countries or even other continents are usually very expensive. Online/digital fiat transfers can be cheaper, but they still come at a cost.
-->
あなたは銀行に送金手数料を払います（国や通貨の範囲内では追加手数料はかからないかもしれませんが、銀行口座を持っていてそのサービスにアクセスするためにはお金を払わなければなりません。その口座のサービス費用は、その手数料に見合ったものです）。他の国や他の大陸への送金は通常非常に高額です。オンラインやデジタル不換紙幣による送金のほうが安くなることもありますが、やはり費用がかかります。

<!--
When you pay online by credit card or PayPal you have to pay an extra fee. Sometimes it seems free, but if you’re not paying explicitly for it, then the costs are likely hidden in the price, because the seller sure does have to pay.
-->
あなたがクレジットカードやPayPalを使ってオンラインで支払うときは、余分な手数料を払う必要があります。ときにはそれは無料のようですが、明示的に支払っていない場合には、販売者は確かに支払う日宇養があります。なのでコストはおそらく価格に隠されています。

<!--
And it’s the same thing in your local store. They pay for card purchases. Paying by cash also comes with a cost: a store owner has to pay to deposit cash in the bank and pay to get small change. These are all costs that the consumer in the end has to pay for, because the store owner has to raise prices to cover the cost. So even if you don’t notice the transaction costs because the fee is paid by the other party, it impacts you.
-->
近くのお店でも同じように、彼らはカードで支払いをします。現金での支払いにもコストが掛かります。：店のオーナーは、銀行に現金を預けるためにお金を払わなければなりません。これらはすべて最終的に消費者が支払わなければならないコストであり、店主はそのコストをカバーするために値上げをしなければならないのです。そのため、手数料は相手が支払うものなので、取引コストに気づかなくても、あなたに影響を与えてしますのです。

## IOTA is feeless
<!--
The cryptocurrency IOTA is the only system I know that does not have any transaction fee at all. How can that be? Your computer/phone/device pays with a little bit of calculation power. To make one transaction you first have to confirm two other transactions, and as such confirm that previous transactions were legitimate. Because everyone participating is ensuring the integrity of the network, there is no trusted third party needed who has to be rewarded for the effort2.
-->
暗号通貨のIOTAは、私が知っている中で唯一取引手数料が全くかからないシステムです。どうしてそうなるのでしょうか？あなたのコンピューターやスマートフォンやデバイスは、少しの計算力で支払いを行います。１つの取引を行うには、まず他の２つの取引を確認し、以前の取引が正当なものであることを確認する必要があります。参加している全員がネットワークの整合性を確保しているため、その努力に対して報酬を得なければならない信頼できる第三者は必要ありません。2

## NOT feeless if there is an exchange rate risk premium
<!--
With IOTA the transaction fee for payments or transferring money can be zero. The middle man is cut out and the buyer and seller are better off. However I think there is a risk the lower transaction cost could be eaten up by exchange rate risk premiums, at least until a broader implementation of IOTA has happened.
-->
IOTAを使えば、支払いや送金の際の取引手数料はゼロになります。中間業者が排除され、買い手と売り手の利益が向上します。しかし、少なくともIOTAの広範な実装が行われるまでは、取引コストの低さが為替レートのリスクプレミアムに食われてしまうリスクがあると思います。

<!--
Right now companies run on fiat currency, report in fiat and pay taxes in fiat. When deals are made in foreign currencies a risk premium is added to cover the risk that the exchange rate can move. The same is likely true for companies that now do transactions in IOTA (if you work for a company where paying in IOTA is possible, please let me know how you do it.)
-->
現在、企業は不換紙幣で経営し、不換紙幣で報告し、不換紙幣で納税しています。外貨で取引する際には、為替レートが変動するリスクをカバーするためにリスクプレミアムが付加されています。現在、IOTAで取引を行っている企業も同じことが言えそうです（IOTAでの支払いが可能な企業にお勤めの方は、どのようにしているか教えて下さい）。

<!--
If fees end up being bigger than a potential profit/advantage, that transaction will not happen. Potentially this means that transactions that could be beneficial for society do not happen because of transaction fees. This risk is especially high for microtransactions.
-->
手数料が潜在的な利益やアドバンテージよりも大きい場合、その取引は発生しません。これは、社会にとって有益である可能性のある取引が、取引手数料のために行われないことを意味します。このリスクは、特にマイクロトランザクションの場合に高いです。

## IOTA as a feeless, self-sustained ecosystem
<!--
For IOTA to be successful and for society to reap the benefits of a feeless system, it needs to be a system where intra-day fluctuations in IOTA/EUR exchange rate would not affect the prices of products.
-->
IOTAが成功し、社会が手数料なしなシステムの利点を享受するために、IOTA/EUR為替レートの日内変動が製品の価格に影響を与えないようなシステムである必要があります。

<!--
One way to do this is to make it a self-contained system. A system where sometimes you receive money/IOTA and sometimes you pay, but in the end it balances out.
-->
一つの方法としては、自己完結型のシステムにすることです。お金を受け取ることもあれば、お金を払うこともありますが、最終的にはバランスが取れているシステムです。

<!--
There is however another way, more viable in the short term, until broad adoption becomes reality. And that is taking the risk that the conversion to fiat will have a positive effect, not regardless of volatility, but because of it. Anyone who has followed the cryptocurrency markets has experienced this. Anything under a 50% price increase or decrease is just another day. A favorable price opportunity to buy or sell is hardly ever lost. For companies looking for a competitive edge, they might forego charging exchange rate risk premiums. This makes their prices more competitive. At the same time their ‘risk’ of the price jumping up the minute after the transaction is real, but the likelihood of a correction within days if not hours is also there. In the end it will likely even out, or even a profit might be made.
-->
しかし、広く普及するまでの間、短期的にはより実行可能な別の方法があります。それは、不換紙幣への転換が、ボラティリティに関係なく、ポジティブな効果をもたらすというリスクを取ることです。暗号通貨市場を見てきた人なら誰もが経験していることです。価格が５０％以下の上昇・下落は、ただの一日の出来事です。購入または売却するための有利な価格の機会を失うことは殆どありません。競争優位性を求める企業は、為替レートのリスクプレミアムを請求することを見送るかもしれません。これは価格をより競争力のあるものにします。同時に、取引後すぐに価格が跳ね上がるという「リスク」もありますが、数時間ではなくても数日以内に修正される可能性もあります。最終的には、それはおそらく互角になるでしょうし、利益が出るかもしれません。

<!--
(Embracing the ‘risk’ goes against some traditional economic theory, but then again, so does much of the cryptomarket. We will be diving further into these possible paradigm shifts in future posts.)
-->
（「リスク」を受け入れることは、伝統的な経済理論に反することですが、暗号市場の多くも同様です。今後の記事では、これらの可能性のあるパラダイムシフトについて更に掘り下げていく予定です。）
