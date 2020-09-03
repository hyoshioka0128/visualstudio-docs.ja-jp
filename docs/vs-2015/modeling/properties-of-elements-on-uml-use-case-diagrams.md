---
title: UML ユースケース図の要素のプロパティ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.usecasediagram.artifact.properties
- vs.teamarch.usecasediagram.shapes.properties
helpviewer_keywords:
- use case diagrams, properties
ms.assetid: 2728fb26-a275-4fce-8a2c-5a78af6bee04
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: db3dc649d979c87960a42d38ffa211e352be175b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671413"
---
# <a name="properties-of-elements-on-uml-use-case-diagrams"></a>UML ユース ケース図の要素のプロパティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML ユース ケース図では、図の各要素にプロパティが存在します。 要素のプロパティを表示するには、図または **UML モデルエクスプローラー** で要素を右クリックし、[ **プロパティ**] をクリックします。 プロパティが [ **プロパティ** ] ウィンドウに表示されます。

> [!NOTE]
> このトピックでは、UML ユース ケース図の要素のプロパティについて説明します。 UML アクティビティ図を読み取る方法の詳細については、「 [Uml ユースケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md)」を参照してください。 UML アクティビティ図を描画する方法の詳細については、「 [Uml ユースケース図: ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)」を参照してください。

## <a name="properties-of-elements"></a>要素のプロパティ

|プロパティ|Default|要素|説明|
|--------------|-------------|-------------|-----------------|
|**名前**|既定名|All|要素を指定します。|
|**修飾名**|Package :: Name|All|要素を一意に識別します。 要素を格納するパッケージの修飾名が先頭につきます。|
|**作業項目**|関連付けなし|All|この要素に関連付けられている作業項目の数。 作業項目を関連付けるには、「 [モデル要素と作業項目のリンク](../modeling/link-model-elements-and-work-items.md)」を参照してください。|
|**説明**|(なし)|All|ここに、要素に関する一般的なメモを作成できます。|
|**色**|(既定値)。|All|シェイプの色。 他のプロパティとは異なり、これは図形が表示する要素のプロパティではありません。|
|**［イメージ パス］**|(なし)|Actor|既定のアクター アイコンの代わりに使われるイメージのファイル パス。 このアイコンは、Visual Studio プロジェクト内のリソース ファイルである必要があります。|
|**件名**|(なし)|ユース ケース|ユース ケースを所有するサブシステムまたは他の型。<br /><br /> 図のサブシステムにユース ケースを配置することで、設定できます。|
|**可視性**|パブリック|ユース ケース、アクター、サブシステム|**Public** -グローバルに表示されます。<br /><br /> **パッケージ-パッケージ** 内に表示されます。|
|**IsAbstract**|×|ユース ケース、アクター、サブシステム|True の場合、型をインスタンス化することはできません。型は他の定義による特殊化のベースとして使われることを意図しています。|
|**間接的にインスタンス化**|○|Subsystem|サブシステムは、設計の成果物としてのみ存在します。 実行時には、そのパートのみ存在します。|
|**ハイパーリンク**|(なし)|アーティファクト|成果物からのリンクが設定された図またはドキュメントの URL またはファイル パス。|

 関連付けのプロパティの一覧については、「 [UML クラス図の関連付けのプロパティ](../modeling/properties-of-associations-on-uml-class-diagrams.md)」を参照してください。

## <a name="see-also"></a>参照
 [Uml ユースケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md) [Uml ユースケース図: ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)
