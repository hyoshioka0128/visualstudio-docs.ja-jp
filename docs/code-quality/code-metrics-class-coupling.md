---
title: コードメトリックス-クラスの結合
ms.date: 1/8/2021
description: Visual Studio のコードメトリックスのクラス結合メトリックについて説明します。
ms.topic: conceptual
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: db1308843cb3c4fe8fb0a4aa32300e545e5e3a7c
ms.sourcegitcommit: b1f7e7d7a0550d5c6f46adff3bddd44bc1d6ee1c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2021
ms.locfileid: "98069562"
---
# <a name="code-metrics---class-coupling"></a>コードメトリックス-クラスの結合

また、クラスの結合は、 [CK94](#ck94)によって最初に定義されたオブジェクト (CBO) 間の名前の結合によっても行われます。 基本的に、クラスの結合は、1つのクラスで使用されるクラスの数を測定したものです。 大きな数値は不適切であり、通常、このメトリックには小さい数値が適しています。 クラスの結合は、ソフトウェアの障害を正確に予測するために示されており、最近の研究により、上限値9が最も効率的な [S2010](#s2010)であることがわかりました。

Microsoft のドキュメントによれば、クラスの結合は、パラメーター、ローカル変数、戻り値の型、メソッドの呼び出し、ジェネリックまたはテンプレートのインスタンス化、基底クラス、インターフェイスの実装、外部型で定義されたフィールド、および属性の装飾を通じて、一意のクラスへの結合を測定します。 優れたソフトウェア設計では、型とメソッドが高い凝集度と低結合を持つ必要があります。 結合率が高い場合は、他の型との依存関係が多数あるため、再利用と保守が困難な設計が示されます。 "

結合と凝集度の概念は明確に関連しています。 ここでは、このトピックについて説明しますが、 [KKLS2000](#kkls2000)から簡単な定義を提供する以外の凝集度については説明しません。

"モジュールの凝集度は、モジュールの内部要素を互いに密に [バインドしたり](#yc79)、関連付けたりすることにより、Don と Constantine によって導入されました。 モジュールが厳密に1つのタスク [...] を表し、そのすべての要素がこの1つのタスクに寄与する場合、モジュールには強力な凝集度があります。 これらの例では、コードではなく、設計の属性として凝集度を記述し、再利用性、保守容易性、および changeability を予測するために使用できる属性を示しています。 "

## <a name="class-coupling-example"></a>クラスの結合の例

アクションのクラス結合について見てみましょう。 まず、新しいコンソールアプリケーションを作成し、いくつかのプロパティを持つ Person という名前の新しいクラスを作成した後、すぐにコードメトリックスを計算します。

![クラス結合の例1](media/class-coupling-example-1.png)

クラスの結合が0であることに注意してください。このクラスは他のクラスを使用しないためです。 ここで、Person のインスタンスを作成し、プロパティ値を設定するメソッドを使用して、"個人情報" という別のクラスを作成します。 もう一度コードメトリックスを計算します。

![クラス結合の例2](media/class-coupling-example-2.png)

クラスの結合値がどのようになるかを確認します。 また、設定したプロパティの数に関係なく、[クラス結合] の値は、他の値ではなく1だけ表示されることに注意してください。 クラス結合は、使用されている量に関係なく、このメトリックに対して各クラスを1回だけ測定します。 さらに、に1が含まれていることがわかりますが、 `DoSomething()` コンストラクターの値が0であることを確認できます `PersonStuff()` 。 現在、別のクラスを使用しているコードがコンストラクターにありません。

別のクラスを使用したコードをコンストラクターに配置した場合はどうなりますか。 次のような情報が得られます。

![クラス結合の例3](media/class-coupling-example-3.png)

コンストラクターには、別のクラスを使用するコードが明確に含まれるようになったので、クラス結合メトリックにこの事実が示されています。 ここでも、is 1 のクラス結合全体を確認でき `PersonStuff()` `DoSomething()` ます。また、1つの外部クラスを使用している内部コードの大きさに関係なく、1つの外部クラスのみが使用されていることを示しています。

次に、別の新しいクラスを作成します。 このクラスにいくつかの名前を付け、その中にいくつかのプロパティを作成します。

![クラス結合の例-新しいクラスの追加](media/class-coupling-example-add-new-class.png)

次に、クラス内のメソッドでクラスを使用 `DoSomething()` `PersonStuff` し、コードメトリックスを再度計算します。

![クラス結合の例4](media/class-coupling-example-4.png)

ご覧のように、ユーザークラスのクラス結合は2になります。クラスをドリルダウンすると、メソッドの結合が最も多いことがわかります `DoSomething()` が、コンストラクターは引き続き1つのクラスを使用します。  これらのメトリックを使用して、特定のクラスの全体の最大数を確認し、メンバーごとに詳細をドリルダウンすることができます。

## <a name="the-magic-number"></a>マジックナンバー

サイクロマティック複雑性と同様に、すべての組織に適した制限はありません。 ただし、 [S2010](#s2010) は、9の制限が最適であることを示しています。

"そのため、しきい値 [...]最も効果的です。 これらのしきい値 (1 つのメンバーの場合) は CBO = 9 [...] です。 " (強調追加)

## <a name="code-analysis"></a>コード分析

コード分析には、保守容易性ルールのカテゴリが含まれています。 詳細については、「 [保守容易性ルール](/dotnet/fundamentals/code-analysis/quality-rules/maintainability-warnings)」を参照してください。 レガシコード分析を使用する場合、拡張デザインガイドラインの規則セットには保守容易性の領域が含まれます。

![クラス結合拡張デザインガイドライン規則](media/class-coupling-extended-design-guideline-rules.png)

保守容易性領域内には、クラス結合の規則があります。

![クラス結合ルール](media/class-coupling-maintainability-area-rules.png)

このルールは、クラスの結合が過剰である場合に警告を発行します。 詳細については、「 [CA1506: 過剰なクラス結合の回避](/dotnet/fundamentals/code-analysis/quality-rules/ca1506)」を参照してください。

このルールの詳細については、アーカイブされたコード分析のブログ記事「 [チェックインポリシーとしてのコードメトリックス](/archive/blogs/codeanalysis/code-metrics-as-check-in-policy) 」と「 *80 より上位のクラスの* しきい値の説明の警告」を参照してください。  これらの値は異常に高いように見えますが、少なくとも極端に上限を指定することはできません。 この警告が表示された場合、ほぼ間違いありません。

## <a name="citations"></a>引用

### <a name="ck94"></a>CK94

Chidamber、s. R。 & Kemerer、.C。 (1994)。 オブジェクト指向設計のためのメトリックスイート (ソフトウェアエンジニアリングでの IEEE トランザクション、Vol. 20、いいえ)。 6)。 ピッツバーグ web サイトから2011年5月14日に取得されました。 [http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf](http://www.pitt.edu/~ckemerer/CK%20research%20papers/MetricForOOD_ChidamberKemerer94.pdf)

### <a name="kkls2000"></a>KKLS2000

Kabaili、H.、Keller、R.、Lustman、F.、およびサンデには、G. (2000) があります。 クラス凝集度の再検討: 産業システムの経験研究 (Object-Oriented ソフトウェアエンジニアリングにおける定量的アプローチに関するワークショップの手続き)。 Université de Montréal web サイトから2011年5月20に取得されました [http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf](http://www.iro.umontreal.ca/~sahraouh/qaoose/papers/Kabaili.pdf)

### <a name="sk2003"></a>SK2003

Subramanyam、R. & Krishnan、m. (2003). Object-Oriented 設計の複雑さに関する、パフォーマンスに関する測定基準の経験分析: ソフトウェアの不具合 (ソフトウェアエンジニアリングでの IEEE トランザクション、Vol. 29、いいえ) に対する影響。 4)。 2011年5月14日に、マサチューセッツ Dartmouth-hitchcock web サイトから取得されました [http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf](http://moosehead.cis.umassd.edu/cis580/readings/OO_Design_Complexity_Metrics.pdf)

### <a name="s2010"></a>S2010

Shatnawi、R. (2010)。 Open-Source システムの Object-Oriented メトリックで許容されるリスクレベルの定量的調査 (ソフトウェアエンジニアリングでの IEEE トランザクション、36、いいえ)。 2)。

### <a name="yc79"></a>YC79

Edward は Don と Larry Constantine を持っています。 構造化デザイン。 Prentice Hall、Englewood 崖、N.J.、1979。