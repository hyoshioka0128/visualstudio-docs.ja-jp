---
title: UML コンポーネント図の要素のプロパティ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.componentdiagram.shapes.properties
helpviewer_keywords:
- component diagrams, properties
- UML, element properties
ms.assetid: fa0a9460-6675-4642-aa00-50f8719a892d
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 39350a9e1d340651f8e15de109ecf61eb98996bb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671456"
---
# <a name="properties-of-elements-on-uml-component-diagrams"></a>UML コンポーネント図の要素のプロパティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML コンポーネント図の各要素には、プロパティがあります。 要素のプロパティを表示するには、図または **UML モデルエクスプローラー** で要素を右クリックし、[ **プロパティ**] をクリックします。 プロパティが [ **プロパティ** ] ウィンドウに表示されます。

> [!NOTE]
> このトピックでは、UML コンポーネント図の要素のプロパティについて説明します。 UML コンポーネント図を読み取る方法の詳細については、「 [Uml コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)」を参照してください。 UML コンポーネント図を描画する方法の詳細については、「 [Uml コンポーネント図: ガイドライン](../modeling/uml-component-diagrams-guidelines.md)」を参照してください。

## <a name="properties-of-elements"></a>要素のプロパティ

|プロパティ|Default|要素|説明|
|--------------|-------------|-------------|-----------------|
|**名前**|既定名|All|要素を指定します。|
|**修飾名**|名前空間 :: 名前|All|要素を一意に識別します。<br /><br /> コンポーネントまたは型の名前に、要素を格納するパッケージの修飾名がプレフィックスとして付けられます。<br /><br /> パートまたはポートの名前に、要素を所有するコンポーネントの修飾名がプレフィックスとして付けられます。|
|**作業項目**|関連付けなし|All|この要素に関連付けられている作業項目の数。 作業項目を関連付けるには、「 [モデル要素と作業項目のリンク](../modeling/link-model-elements-and-work-items.md)」を参照してください。|
|**説明**|(なし)|All|ここに、要素に関する一般的なメモを作成できます。|
|**色**|(型の既定値)|コンポーネント、パート、委譲、パート アセンブリ|シェイプの色。 他のプロパティとは異なり、これはシェイプに表示されるモデル要素ではなく、シェイプの色です。|
|**間接的にインスタンス化**|True|コンポーネント|コンポーネントは設計の成果物としてのみ存在します。 実行時には、そのパートのみ存在します。|
|**抽象型**|×|コンポーネント|コンポーネント定義は、他のコンポーネントを特化できる汎化としてのみ使用できます。|
|**可視性**|パブリック|コンポーネント、パート、ポート|**Public** -グローバルに表示されます。<br /><br /> **パッケージ-パッケージ** 内に表示されます。<br /><br /> **プライベート** : 所有コンポーネント内で参照できます。<br /><br /> **Protected** -所有者から派生したコンポーネントから参照できます。|
|**Type**|作成時の型|パーツ<br /><br /> Port|パートの型はコンポーネントまたはクラスです。<br /><br /> ポートの型はインターフェイスです。|
|**カーディナリティ**|1|パーツ<br /><br /> Port|親コンポーネントの一部を構成する指定された型のインスタンスの数を示します。<br /><br /> `1` -1 つ。<br /><br /> `0..1` -1 または none。<br /><br /> `*` -任意の数のコレクション。<br /><br /> `n..m` -n から m のインスタンスのコレクション。|
|**振る舞い**|×|Port|true の場合、このポートへのメッセージは、コンポーネントの一部として (そのパートではなく) 記述されるアクティビティまたは操作で処理されます。|
|**サービス**|×|Port|true の場合、このポートはこのコンポーネントの発行されたインターフェイスの一部です。|
|**LinkedPackage**|モデル|ダイアグラム|この図に追加された要素の既定の名前空間。|

## <a name="see-also"></a>参照
 [Uml ユースケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md) [Uml ユースケース図: ガイドライン](../modeling/uml-use-case-diagrams-guidelines.md)
