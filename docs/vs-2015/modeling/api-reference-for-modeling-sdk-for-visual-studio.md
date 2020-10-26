---
title: モデリング SDK の API リファレンス
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
ms.assetid: 590c9a69-4e22-4841-bb23-f32e80ec1e76
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 65f8703597d6297afde6e2685594784fdd1d755c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672842"
---
# <a name="api-reference-for-modeling-sdk-for-visual-studio"></a>Modeling SDK for Visual Studio の API リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の視覚化およびモデリング SDK には、ドメイン固有言語 (DSL) と UML ツールがビルドされるプラットフォームが用意されています。

> [!NOTE]
> UML モデリング API の詳細については、「 [Uml モデリング機能拡張の Api リファレンス](../modeling/api-reference-for-uml-modeling-extensibility.md)」を参照してください。 テキスト変換の詳細については、「 [T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)」を参照してください。

 このセクションには、名前が "VisualStudio" で始まる名前空間の参照資料が含まれています。

|名前空間|Content|
|---------------|-------------|
|<xref:Microsoft.VisualStudio.Modeling?displayProperty=fullName>|ModelElement などのクラス。 DSL で定義するすべてのドメインクラスの基本クラスです。|
|<xref:Microsoft.VisualStudio.Modeling.Design?displayProperty=fullName>|DSL 定義の一部を形成するクラス。|
|<xref:Microsoft.VisualStudio.Modeling.Diagnostics?displayProperty=fullName>|モデルストアビューアーとパフォーマンス測定ツール。|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams?displayProperty=fullName>|[図形] 要素などのクラスは、DSL で定義したすべての図形の基本クラスです。|
|<xref:Microsoft.VisualStudio.Modeling.Diagrams.ExtensionEnablement?displayProperty=fullName>|ジェスチャと選択のメソッド。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition?displayProperty=fullName>|DSL 定義デザイナーの API。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.Design?displayProperty=fullName>|DSL 定義デザイナーの内部クラス。|
|<xref:Microsoft.VisualStudio.Modeling.DslDefinition.ExtensionEnablement?displayProperty=fullName>|コマンド、ジェスチャ、および検証を使用して DSL デザイナーを拡張できる属性。|
|<xref:Microsoft.VisualStudio.Modeling.Extensibility?displayProperty=fullName>|DSL 拡張を実装する ModelElement の拡張メソッド。|
|<xref:Microsoft.VisualStudio.Modeling.ExtensionEnablement?displayProperty=fullName>|拡張属性|
|<xref:Microsoft.VisualStudio.Modeling.Immutability?displayProperty=fullName>|モデルの一部を読み取り専用にすることができます。|
|[VisualStudio の統合](/previous-versions/ee904412(v=vs.140))|Modelbus API。さまざまなモデルを統合するのに役立ちます。|
|[VisualStudio を選択します。](/previous-versions/ee904394(v=vs.140))|ユーザーがモデルおよび要素に移動して Modelbus 参照を作成できるダイアログボックス。|
|`Microsoft.VisualStudio.Modeling.Integration.Picker.Hosting`|ピッカーサービス。|
|[VisualStudio を作成します。](/previous-versions/ee869435(v=vs.140))|の modelbus アダプターフレームワーク [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。|
|[VisualStudio を選択してください。](/previous-versions/ee886769(v=vs.140))|ユーザーがモデルと要素に移動して Modelbus 参照を作成できるようにする [ピッカー] ダイアログボックス。|
|<xref:Microsoft.VisualStudio.Modeling.Shell?displayProperty=fullName>|Dsl との間のインターフェイス [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 。|
|<xref:Microsoft.VisualStudio.Modeling.Shell.ExtensionEnablement?displayProperty=fullName>|ショートカット (コンテキスト) メニューコマンドを定義できます。|
|<xref:Microsoft.VisualStudio.Modeling.Validation?displayProperty=fullName>|検証制約を定義できます。|

## <a name="see-also"></a>関連項目

- [UML モデリング機能拡張の API リファレンス](../modeling/api-reference-for-uml-modeling-extensibility.md)
- [T4 テキスト変換のカスタマイズ](../modeling/customizing-t4-text-transformation.md)
