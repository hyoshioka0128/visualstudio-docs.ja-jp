---
title: ドメイン リレーションシップのプロパティ
description: アクセス修飾子、Custome 属性など、ドメイン relationshop に関連付けられているプロパティについて説明し、二重の派生を生成します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain relationships
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 88c5db50432947b99a2667280fe7861e7acd95ac
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97362458"
---
# <a name="properties-of-domain-relationships"></a>ドメイン リレーションシップのプロパティ
次の表のプロパティは、ドメインリレーションシップに関連付けられています。 ドメインリレーションシップの詳細については、「 [モデル、クラス、およびリレーションシップ](../modeling/understanding-models-classes-and-relationships.md)について」を参照してください。 これらのプロパティの使用方法の詳細については、「 [Domain-Specific 言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

|プロパティ|説明|Default|
|-|-|-|
|アクセス修飾子|ドメインリレーションシップのアクセスレベル ( `public` または `internal` )。|`public`|
|カスタム属性|ドメインリレーションシップから生成されるソースコードクラスに属性を追加するために使用します。|\<none>|
|2つの派生を生成します|`True`の場合、基本クラスと部分クラスの両方 (オーバーライドによるカスタマイズをサポートするため) が生成されます。 詳細については、「 [生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|`False`|
|カスタムコンストラクターがある|`True`の場合、カスタムコンストラクターがソースコードに指定されていることを示します。 詳細については、「 [生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|`False`|
|継承修飾子|ドメインリレーションシップ ( `none` 、または) から生成されるソースコードクラスの継承の種類について説明し `abstract` `sealed` ます。|\<none>|
|重複を許可|の場合 `True` 、同じ2つの要素間にドメインリレーションシップの重複するリンクを作成できます。|`False`|
|基本リレーションシップ|ドメインリレーションシップが派生している場合は、ドメインリレーションシップの基本関係。|\<none>|
|埋め込み|の場合 `True` 、ドメインリレーションシップは埋め込みリレーションシップです。 の場合 `False` 、リレーションシップは参照リレーションシップです。|\<both>|
|名前|ドメインリレーションシップの名前。|現在の名前|
|名前空間|ドメインリレーションシップに関連付けられている名前空間。|現在の名前空間|
|メモ|ドメインリレーションシップに関連付けられている非公式のメモ。|\<none>|
|説明|コードをドキュメント化するために使用される説明。生成されたデザイナーの UI で使用されます。|\<none>|
|表示名|ドメインリレーションシップの生成されたデザイナーに表示される名前。|\<none>|
|ヘルプ キーワード|ドメインリレーションシップの F1 ヘルプのインデックスを作成するために使用される省略可能なキーワードです。|\<none>|

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))