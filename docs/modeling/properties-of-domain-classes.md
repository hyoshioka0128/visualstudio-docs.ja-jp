---
title: ドメイン クラスのプロパティ
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain class
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 2865e6a6d410d661bc628fd9c7f1947516485018
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544184"
---
# <a name="properties-of-domain-classes"></a>ドメイン クラスのプロパティ
ドメインクラスには、次の表に示すプロパティがあります。 ドメインクラスの詳細については、「[モデル、クラス、およびリレーションシップ](../modeling/understanding-models-classes-and-relationships.md)について」を参照してください。 これらのプロパティの使用方法の詳細については、「[ドメイン固有言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

|プロパティ|説明|Default|
|-|-|-|
|アクセス修飾子|ドメイン クラスのアクセスのレベル (`public` または `internal`)。|`public`|
|カスタム属性|このドメインクラスから生成されるソースコードクラスに属性を追加するために使用します。|\<none>|
|2つの派生を生成します|`True`の場合、基本クラスと部分クラス (オーバーライドによるカスタマイズをサポートする) の両方が生成されます。 詳細については、「[生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|`False`|
|カスタムコンストラクターがある|`True`の場合、カスタムコンストラクターがソースコードで提供されます。 詳細については、「[生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|`False`|
|継承修飾子|ドメインクラス ( `none` 、または) から生成されるソースコードクラスの継承の種類について説明し `abstract` `sealed` ます。|`none`|
|基本クラス|このドメインクラスが派生している場合は、基本クラスの名前。|\<none>|
|名前|このドメインクラスの名前。|現在の名前|
|名前空間|このドメインクラスの名前空間。|現在の名前空間|
|メモ|このドメインクラスに関連付けられている非公式のメモ。|\<none>|
|説明|生成されたデザイナーの UI を文書化するために使用される説明。|\<none>|
|表示名|このドメインクラスの生成されたデザイナーに表示される名前。|\<none>|
|ヘルプ キーワード|このドメインクラスの F1 ヘルプのインデックス作成に使用される省略可能なキーワードです。|\<none>|

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](https://msdn.microsoft.com/ca5e84cb-a315-465c-be24-76aa3df276aa)