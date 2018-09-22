---
templateKey: blog-post
title: ビットコイン原論文解説　第4章「Proof of Work」
date: 2018-09-21T18:22:27.853Z
description: ビットコイン原論文の第4章「Proof of Work」について分かりやすく解説します。
tags:
  - ビットコイン
  - 解説
---
![Bitcoin](/img/bitcoin-header.jpg)

## 目次

概要

第1章　イントロダクション

第2章　取引

第3章　タイムスタンプ・サーバー

**<font color="Green">第4章　Proof of Work</font>**

第5章　ネットワーク

第6章　インセンティブ

第7章　ディスク領域の再利用

第8章　簡易版支払い検証

第9章　価値の結合と分割

第10章　プライバシー

第11章　計算

第12章　結論

## 原文

> To implement a distributed timestamp server on a peer-to-peer basis, we will need to use a proof-of-work system similar to Adam Back's Hashcash \[6], rather than newspaper or Usenet posts. The proof-of-work involves scanning for a value that when hashed, such as with SHA-256, the hash begins with a number of zero bits. The average work required is exponential in the number of zero bits required and can be verified by executing a single hash. For our timestamp network, we implement the proof-of-work by incrementing a nonce in the block until a value is found that gives the block's hash the required zero bits. Once the CPU effort has been expended to make it satisfy the proof-of-work, the block cannot be changed without redoing the work. As later blocks are chained after it, the work to change the block would include redoing all the blocks after it.
>
> ![Blockchain](/img/bitcoin_pow_pdf.png)
>
> The proof-of-work also solves the problem of determining representation in majority decision making. If the majority were based on one-IP-address-one-vote, it could be subverted by anyone able to allocate many IPs. Proof-of-work is essentially one-CPU-one-vote. The majority decision is represented by the longest chain, which has the greatest proof-of-work effort invested in it. If a majority of CPU power is controlled by honest nodes, the honest chain will grow the fastest and outpace any competing chains. To modify a past block, an attacker would have to redo the proof-of-work of the block and all blocks after it and then catch up with and surpass the work of the honest nodes. We will show later that the probability of a slower attacker catching up diminishes exponentially as subsequent blocks are added.
>
> To compensate for increasing hardware speed and varying interest in running nodes over time, the proof-of-work difficulty is determined by a moving average targeting an average number of blocks per hour. If they're generated too fast, the difficulty increases.
>
> <text style="font-size: 80%">\[6] A. Back, "Hashcash - a denial of service counter-measure," http://www.hashcash.org/papers/hashcash.pdf, 2002.</text>

## 原文日本語訳

P2Pで分散タイムスタンプサーバーを実現するには、新聞やネットニュースのような仕組みではなく、Adam BackのHashcash\[6]と同様のProof of Workシステムを使用する必要があります。Proof of Workでは、例えばSHA-256のようなハッシュ関数を通した時に、先頭のnビットが0となる値を見つける作業を行います。要求される平均的な作業は、必要とされる0のビット数に応じて指数関数的に増加する一方、検証をするには一つのハッシュを実行するだけで済みます。私たちのタイムスタンプネットワークでは、ブロックのハッシュに要求される先頭nビットが0になる値が見つかるまでブロック内のノンスをインクリメントすることで、Proof of Workを実現しています。CPUの労力を費やしてProof of Workを満たすと、Proof of Workやり直すことなくブロックを変更することはできません。ブロックは次々と連鎖するので、一つのブロックを変更するには、そのブロックに連なるすべてのブロックを作り直す必要があります。

![Blockchain](/img/bitcoin_pow_pdf.png)

Proof of Workはまた、大多数の意思決定において代表を決定するという問題を解決します。もし過半数の根拠が「1 IPアドレス＝1票」の原則に基づいていたなら、それは多くのIPを割り当てることができる誰しもが破壊できる可能性があります。Proof of Workは本質的に「1CPU＝1票」です。多数決の結果は最長のチェーンで表され、最長であるということはチェーンに投資されたProof of Workの労力が最大であると意味します。大部分のCPUパワーが善意のノードによって制御されている場合、善意のチェーンは最も速く成長し、競合するチェーンを上回ります。過去のブロックを変更するには、攻撃者はそのブロックとそれ以降のすべてのブロックのProof of Workをやり直さなければならず、善意のノードの作業に追いついてそれを上回る必要があります。 後で説明するように、善意のノードよりも遅い攻撃者が追いつく確率は、後続のブロックが追加されると指数関数的に減少します。

時間の経過と共に、ハードウェアの計算スピードが増したり、ノードを運用しようという関心が変化するのを補うため、Proof of Workの難易度は1時間あたりの平均ブロック生成数を目標とする移動平均によって決定されます。ブロックがあまりにも速く生成されると、難易度が増します。

## 解説

### まとめ

* P2Pの分散タイムスタンプサーバーを実現するため、Proof of Workという仕組みを用いる。
* Proof of Workとは、ある値xをハッシュ関数に通して、先頭のnビットが0になるような結果を得る値xを見つける作業である。
* このProof of Workは何ビット先頭が0となるかを調整でき、指数関数的に作業量を増やせる一方で、検証は一度で済む。
* ブロックはチェーン状に連鎖するので、あるブロックを書き換えるには、後続するブロック全てについてProof of Workをやり直さなければならない。
* 「最長のチェーンを正しいものとする」ならば、善意のノードがCPUパワーの過半数を占めれば、悪意を持った攻撃者よりも早くブロックを作れるので、改竄される可能性はブロックが追加されるほど減少する。
* 現実ではハードウェア性能が上がったり、ノードの参加者が増減するのでブロック生成に費やされるCPUパワーは一定ではない。そのため、Proof of Workの難易度（＝先頭何ビットを0にするか）は過去のブロック生成数によって調整される。

### 詳しい解説

<hr>
次章: 第5章　ネットワーク
