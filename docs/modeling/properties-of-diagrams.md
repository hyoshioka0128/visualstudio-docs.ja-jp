---
title: ダイアグラムのプロパティ
ms.date: 10/31/2018
ms.topic: reference
f1_keywords:
- vs.dsltools.dsldesigner.dsldiagram
helpviewer_keywords:
- Domain-Specific Language, diagram
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 762c2acb6774d7eb4949087fdd91e85c86acd6bb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75595424"
---
# <a name="properties-of-diagrams"></a>ダイアグラムのプロパティ
生成されたデザイナーでのダイアグラムの表示方法を指定するプロパティを設定できます。 たとえば、図のテキストの既定の色を指定できます。

 詳細については、「 [ドメイン固有言語を定義する方法](../modeling/how-to-define-a-domain-specific-language.md)」を参照してください。 これらのプロパティの使用方法の詳細については、「 [ドメイン固有言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

 次の表に、ダイアグラムのプロパティの一覧を示します。

|プロパティ|説明|Default|
|-|-|-|
|[塗りつぶしの色]|ダイアグラムの塗りつぶしの色。|White|
|テキストの色|ダイアグラムに表示されるテキストの色。|Black|
|アクセス修飾子|クラスのアクセス修飾子 (public または internal)。|パブリック|
|カスタム属性|生成されたコードクラスに属性を追加するために使用します。|\<none>|
|2つの派生を生成します|`True`の場合、基本クラスと部分クラス (オーバーライドによるカスタマイズをサポートする) の両方が生成されます。 詳細については、「 [オーバーライドして生成されたクラスを拡張する](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|×|
|カスタムコンストラクターがある|`True`の場合、カスタムコンストラクターがソースコードで提供されます。 詳細については、「 [クラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|×|
|継承修飾子|ダイアグラムから生成されるソースコードクラスの継承の種類 ( `none` 、 `abstract` 、または) について説明し `sealed` ます。|なし|
|基本図|このダイアグラムの基本クラス。|(なし)|
|名前|このダイアグラムの名前。|現在の名前|
|名前空間|このダイアグラムに関連付けられている名前空間。|現在の名前空間|
|クラスを表す|このダイアグラムが表すルートドメインクラス。|現在のルートクラス (該当する場合)|
|メモ|この要素に関連付けられている非公式のメモ。|\<none>|
|塗りつぶしの色をプロパティとして公開します|の場合 `True` 、ユーザーは、生成されたデザイナーのダイアグラムの塗りつぶしの色を設定できます。 このプロパティを設定するには、ダイアグラムの図形を右クリックし、[ **公開の追加**] をクリックします。|×|
|テキストの色をプロパティとして公開します|の場合 `True` 、ユーザーは、生成されたデザイナーでダイアグラムのテキストの色を設定できます。 このプロパティを設定するには、ダイアグラムの図形を右クリックし、[ **公開の追加**] をクリックします。|×|
|説明|生成されたデザイナーを文書化するために使用される説明。|\<none>|
|表示名|このダイアグラムの生成されたデザイナーに表示される名前。|\<none>|
|ヘルプ キーワード|このダイアグラムの F1 ヘルプのインデックスを作成するために使用されるキーワードです。|\<none>|

## <a name="see-also"></a>こちらもご覧ください

[ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)
