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

> To implement a distributed timestamp server on a peer-to-peer basis, we will need to use a proofof-work system similar to Adam Back's Hashcash \[6], rather than newspaper or Usenet posts. The proof-of-work involves scanning for a value that when hashed, such as with SHA-256, the hash begins with a number of zero bits. The average work required is exponential in the number of zero bits required and can be verified by executing a single hash. For our timestamp network, we implement the proof-of-work by incrementing a nonce in the block until a value is found that gives the block's hash the required zero bits. Once the CPU effort has been expended to make it satisfy the proof-of-work, the block cannot be changed without redoing the work. As later blocks are chained after it, the work to change the block would include redoing all the blocks after it.
>
> ![Blockchain](/img/bitcoin_pow_pdf.png)
>
> The proof-of-work also solves the problem of determining representation in majority decision making. If the majority were based on one-IP-address-one-vote, it could be subverted by anyone able to allocate many IPs. Proof-of-work is essentially one-CPU-one-vote. The majority decision is represented by the longest chain, which has the greatest proof-of-work effort invested in it. If a majority of CPU power is controlled by honest nodes, the honest chain will grow the fastest and outpace any competing chains. To modify a past block, an attacker would have to redo the proof-of-work of the block and all blocks after it and then catch up with and surpass the work of the honest nodes. We will show later that the probability of a slower attacker catching up diminishes exponentially as subsequent blocks are added.
>
> To compensate for increasing hardware speed and varying interest in running nodes over time, the proof-of-work difficulty is determined by a moving average targeting an average number of blocks per hour. If they're generated too fast, the difficulty increases.
>
> <text style="font-size: 80%">[6] A. Back, "Hashcash - a denial of service counter-measure," http://www.hashcash.org/papers/hashcash.pdf, 2002.</text>

## 原文日本語訳

ピアツーピアで分散タイムスタンプサーバーを実装するには、新聞やUsenetの記事ではなく、Adam BackのHashcash[6]と同様の校正作業システムを使用する必要があります。 作業証明には、SHA-256などのハッシュされたときにハッシュがゼロビットの数で始まる値をスキャンすることが含まれます。 要求される平均作業は、必要とされるゼロビットの数で指数関数的であり、単一のハッシュを実行することによって検証することができる。 私たちのタイムスタンプネットワークでは、ブロックのハッシュに必要なゼロビットを与える値が見つかるまで、ブロック内のノンスをインクリメントして作業証明を実装します。 CPUの労力を費やして作業証明を満足させると、作業をやり直すことなくブロックを変更することはできません。 後のブロックが後に連鎖するので、ブロックを変更する作業には、後のすべてのブロックのやり直しが含まれます。

![Blockchain](/img/bitcoin_pow_pdf.png)

仕事の証明はまた、大多数の意思決定において表現を決定するという問題を解決する。 過半数がone-IP-address-one-voteに基づいていたなら、それは多くのIPを割り当てることができる誰によっても破壊される可能性があります。 本人確認は本質的に1CPUの1票です。 多数決は最長のチェーンで表され、チェーンに投資された作業証明の労力は最大です。 大部分のCPUパワーが正当なノードによって制御されている場合、正直なチェーンは最も速く成長し、競合するチェーンを上回ります。 過去のブロックを変更するには、攻撃者はそのブロックとそれ以降のすべてのブロックの作業実績をやり直さなければならず、正直なノードの作業に追いついてそれを上回る必要があります。 後で説明するように、遅い攻撃者が追いつく確率は、後続のブロックが追加されると指数関数的に減少します。

時間の経過と共にハードウェアのスピードが増し、実行中のノードに関心が変化するのを補うために、作業実績の難しさは、1時間あたりの平均ブロック数を目標とする移動平均によって決定されます。 それらがあまりにも速く生成されると、難しさが増します。

## 解説

### まとめ

### 詳しい解説

<hr>
次章: 第5章　ネットワーク
