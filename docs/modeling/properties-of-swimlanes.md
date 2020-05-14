---
title: スイムレーンのプロパティ
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.swimlane
helpviewer_keywords:
- Domain-Specific Language, swimlane
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 0cceeacab44f17eb30184c90f1128b8d2c3528bb
ms.sourcegitcommit: f3f668ecaf11b4c2738ebc91923c6b5e38e74670
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2020
ms.locfileid: "76115367"
---
# <a name="properties-of-swimlanes"></a>スイムレーンのプロパティ
スイムレーンを図に追加できます。 スイムレーンは、図を垂直方向または水平方向の領域に分割します。 スイムレーン内に表示される他の図形を定義できます。 詳細については、「[ドメイン固有言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。 これらのプロパティの使用方法の詳細については、「[ドメイン固有言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

 スイムレーンには、次の表に示すプロパティがあります。

|property|説明|[既定値]|
|-|-|-|
|本文の塗りつぶしの色|スイムレーンの本体の塗りつぶしの色。|白|
|ヘッダーの塗りつぶしの色|スイムレーンのヘッダーの塗りつぶしの色。|濃い灰色|
|区切り記号の色|区切り線の色。|グレー灰色|
|区切り線のスタイル|区切り線のスタイル (`Solid`、`Dash`、`Dot`、`DashDot`、`DashDotDot`、`Custom`)。|`Dash`|
|区切り線の太さ|区切り線の太さ (インチ単位)。|0.03125|
|テキストの色|このスイムレーンに関連付けられているテキストデコレーターに使用される色です。|黒|
|アクセス修飾子|クラスのアクセスレベル (`public` または `internal`)。|Public|
|カスタム属性|このスイムレーンから生成されたコードクラスに属性を追加するために使用します。|\<none>|
|2つの派生を生成します|`True`場合、基本クラスと部分クラス (オーバーライドによるカスタマイズをサポートする) の両方が生成されます。 詳細については、「[生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|[False]|
|カスタムコンストラクターがある|`True`すると、カスタムコンストラクターがソースコードに提供されます。 詳細については、「[生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|[False]|
|継承修飾子|スイムレーン (`none`、`abstract` または `sealed`) から生成されるソースコードクラスの継承の種類について説明します。|none|
|ベーススイムレーン|このスイムレーンの基本クラス。|(なし)|
|[名前]|このスイムレーンの名前。|現在の名前|
|名前空間|このスイムレーンに関連する名前空間。|現在の名前空間|
|ツールヒントの種類|ツールヒントの定義方法 (`fixed`、`variable`、または `none`)。 `fixed`の場合、`Fixed Tooltip Text` プロパティの値が使用されます。`variable`した場合、ツールヒントはカスタムコードで定義されます。|\<none>|
|メモ|このスイムレーンに関連付けられている非公式のメモ。|\<none>|
|アラインメント|水平方向または垂直方向の配置。|Vertical|
|初期の高さ|このスイムレーンの初期の高さ (インチ単位)。 水平スイムレーンにのみ適用されます。|0|
|初期の幅|このスイムレーンの初期の幅 (インチ単位)。 縦方向のスイムレーンにのみ適用されます。|0|
|テキストの色を公開します|`True`した場合、ユーザーは生成されたデザイナーでスイムレーンの色を設定できます。 これを設定するには、スイムレーン図形を右クリックし、 **[公開の追加]** をクリックします。|[False]|
|説明|生成されたデザイナーを文書化するために使用します。|\<none>|
|[表示名]|このスイムレーンクラスを参照するために生成されたデザイナーに表示される名前。|\<none>|
|固定ツールヒントのテキスト|固定のツールヒントに使用されるテキスト。|\<none>|
|ヘルプ キーワード|このスイムレーンの F1 ヘルプのインデックス作成に使用されるキーワードです。|\<none>|

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
