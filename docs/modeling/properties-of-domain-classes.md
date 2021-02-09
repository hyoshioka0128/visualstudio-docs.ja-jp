---
title: ドメイン クラスのプロパティ
description: アクセス修飾子やカスタム属性など、ドメインクラスのさまざまなプロパティについて説明し、二重の派生を生成します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- Domain-Specific Language, domain class
author: JoshuaPartlow
ms.author: joshuapa
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: cc86f04841a819423bc45c9220d6de80a5340b2d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99915997"
---
# <a name="properties-of-domain-classes"></a>ドメイン クラスのプロパティ
ドメインクラスには、次の表に示すプロパティがあります。 ドメインクラスの詳細については、「 [モデル、クラス、およびリレーションシップ](../modeling/understanding-models-classes-and-relationships.md)について」を参照してください。 これらのプロパティの使用方法の詳細については、「 [Domain-Specific 言語のカスタマイズと拡張](../modeling/customizing-and-extending-a-domain-specific-language.md)」を参照してください。

|プロパティ|説明|Default|
|-|-|-|
|アクセス修飾子|ドメイン クラスのアクセスのレベル (`public` または `internal`)。|`public`|
|カスタム属性|このドメインクラスから生成されるソースコードクラスに属性を追加するために使用します。|\<none>|
|2つの派生を生成します|`True`の場合、基本クラスと部分クラス (オーバーライドによるカスタマイズをサポートする) の両方が生成されます。 詳細については、「 [生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|`False`|
|カスタムコンストラクターがある|`True`の場合、カスタムコンストラクターがソースコードで提供されます。 詳細については、「 [生成されたクラスのオーバーライドと拡張](../modeling/overriding-and-extending-the-generated-classes.md)」を参照してください。|`False`|
|継承修飾子|ドメインクラス ( `none` 、または) から生成されるソースコードクラスの継承の種類について説明し `abstract` `sealed` ます。|`none`|
|基本クラス|このドメインクラスが派生している場合は、基本クラスの名前。|\<none>|
|名前|このドメインクラスの名前。|現在の名前|
|名前空間|このドメインクラスの名前空間。|現在の名前空間|
|ノート|このドメインクラスに関連付けられている非公式のメモ。|\<none>|
|説明|生成されたデザイナーの UI を文書化するために使用される説明。|\<none>|
|表示名|このドメインクラスの生成されたデザイナーに表示される名前。|\<none>|
|ヘルプ キーワード|このドメインクラスの F1 ヘルプのインデックス作成に使用される省略可能なキーワードです。|\<none>|

## <a name="see-also"></a>関連項目

- [ドメイン固有言語ツールの用語集](/previous-versions/bb126564(v=vs.100))