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

新たに「Proof of Work」という仕組みが提案されました。と言っても、Proof of Work自体の発想はビットコインが最初ではありません。本文中にあるように、Adam Backという人が「Hashcash」という仕組みを1997年に考案しています。

Adam Back博士のHashcashは、スパムメールを防止するために考案されました。通常の環境では、メールを送るコストはほとんどないため、送信者は大量のメールを送りつけることができます。そこで、「メール一通につき1円のコストがかかる」というルールが施行されたとしましょう。一般ユーザーにとっては少しだけ痛いかもしれませんが、大量のスパムメール送信者にとっては死活問題です。これと同じように、「メール1通送るのに、1秒の計算を行なった証明をつけなければならない」という発想がHashcashです。送信者にお金（Cash）を負担させるのではなく、時間を負担させれば、一度に何百万通ものメールを送ることができず、スパムメールがコスト的にペイしなくなります。

このHashcashは残念ながら普及しませんでしたが、例えばGoogleのreCAPTCHAのように、フォームの送信やWebサイトの閲覧時にユーザーにチェックを入れさせたり簡単な問題を解かせる、といった仕組みは身の回りにたくさんあります。

![reCAPTCHA](/img/recaptcha.png)

ビットコインではそのProof of Workの仕組みを、次のようなルールとしました。

> SHA-256のようなハッシュ関数を通した時に、先頭のnビットが0となる値を見つける作業

ハッシュ関数とは、これまで出てきたように、あるインプットに対して特定の長さのハッシュ値（アウトプット）を出す関数のことです。

ハッシュ関数の中でも、SHA-256のように、ハッシュ値からインプットを類推することができないものを、「暗号学的ハッシュ関数」呼びます（以降では「ハッシュ関数」と言ったときには「暗号学的ハッシュ関数」を指します）。

インプットに対してどのようなハッシュ値が出てくるかは、実際に値をハッシュ関数に入れてみないとわかりません。また、少しでもインプットが変わればハッシュ値は大きく変動します。

* Blockchain → （SHA-256） → 625da44e4eaf58d61cf048d168aa6f5e492dea166d8bb54ec06c30de07db57e1
* blockchain → （SHA-256） → ef7797e13d3a75526946a3bcf00daec9fc9c9c4d51ddc7cc5df888f74dd434d1

このような性質を持つハッシュ関数を用いて、ビットコインのProof of Workでは、ハッシュ値の先頭のnビットが0になるようなインプットを見つけることが求められます。

ではどのようにインプットを見つけるかというと、ノンス（nonce = **N**umber used **ONCE**）という値をひたすら0から1ずつ上げていき、総当たりで条件を満たすハッシュ値になるように計算を繰り返します。他にもインプットとなるデータがありますが、前のブロックハッシュや取引記録といったもので、Proof of Workを実行するノードが任意に操作できるのはノンスだけです。

仮に、他のインプットデータが「Blockchain」という文字列に収束されているとするならば、ノードは次のようにハッシュ計算を実行していきます。

* Blockchain0 → （SHA-256） → 1170bfd4266d3ff0472740483fd69223e04365054e621a72ef2482d5401d1f4d
* Blockchain1 → （SHA-256） → 0fc6e34f6899f5e2ca06688e49bb42cc104a45d5bb86c55eafe8c7d588204a48
* Blockchain2 → （SHA-256） → 4f07e031df167abda5623314c19c38e11358853f1c876b892a1d2ae494cc1058
* Blockchain3 → （SHA-256） → 20e39c7046b6be85eb64afacec02847fb217293cd7962b87667265cc159132c2
* （以下略）

最終的にハッシュ値の先頭nビットが、定められた数の0で生まれば計算終了です。

このProof of Workの計算は総当たりで実行するしかないため、0で満たさなければならない先頭桁数が増えるほどに計算量は指数関数的に増大します。一方で、実際に見つけたインプット（＝ノンス）がハッシュ関数を通したときに条件を満たすかは、一度の計算で済みます。検証が簡単であるので、検証するだけのノードのコストは低く抑えられます。

このようProof of Workによってノンスが見つかるとブロックが生成され、また次のブロックを生成するためのハッシュ計算が始まります。ノンスが見つかるスピードは、単純に機械の計算能力で決まります。計算能力があればあるほど、ブロック生成スピードが上がります。もし攻撃者が取引を改ざんしようとすると、インプットの値が変わる（例えば「Blockchain」が「blockchain」になる）ので、出てくるハッシュ値がかわり、先頭がn個の0を満たすという条件が成り立たなくなります。そのため、攻撃者は再度Proof of Workを行なって、条件を満たすようなノンスを見つけなければなりません。また、ただ該当ブロックのノンスを見つければいいのではなく、ブロックは連鎖していますので、改ざんしたブロックにつながる以降のブロック全てについて正しいノンスを見つけなければなりません。ただし、攻撃者がいそいそとノンスを計算しているうちにも、他のノードによってブロックは伸び続けています。ビットコインのブロックチェーンは「最も長いチェーンを正しいものとする」という合意があるため、攻撃者は他の善意のノードの計算スピードを上回り、現在のブロックに追いつき追い越して初めて改ざんに成功します。これを行うためにはノードの総合CPUパワーの過半数を取得しなければならず、大変な労力を必要とします。よくブロックチェーンは改ざん不可能ではないが現実的には困難、と言われるのはこのためです。





<hr>
次章: 第5章　ネットワーク
