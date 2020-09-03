---
title: UML シーケンス図の要素のプロパティ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
f1_keywords:
- vs.teamarch.sequencediagram.combinedfragment.properties
- vs.teamarch.sequencediagram.shapes.properties
helpviewer_keywords:
- UML sequence diagrams, properties
- sequence diagrams, properties
ms.assetid: 475c10f3-a2d2-4a1e-b366-dc28997d437e
caps.latest.revision: 22
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4d0753ea7396c9f21addcbb01ab7b90be066356a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72671421"
---
# <a name="properties-of-elements-on-uml-sequence-diagrams"></a>UML シーケンス図の要素のプロパティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UML シーケンス図では、図の各要素にプロパティが存在します。 要素のプロパティを表示するには、図または **UML モデルエクスプローラー** で要素を右クリックし、[ **プロパティ**] をクリックします。 プロパティが [ **プロパティ** ] ウィンドウに表示されます。

> [!NOTE]
> このトピックでは、UML シーケンス図の要素のプロパティについて説明します。 UML シーケンス図を読み取る方法の詳細については、「 [Uml シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md)」を参照してください。 UML アクティビティ図を描画する方法の詳細については、「 [UML Sequence Diagrams: Guidelines](../modeling/uml-sequence-diagrams-guidelines.md)」を参照してください。

## <a name="properties-of-elements"></a>要素のプロパティ

|プロパティ|Default|要素|説明|
|--------------|-------------|-------------|-----------------|
|**名前**|既定名|All|要素を指定します。|
|**修飾名**|Package :: Name|All|要素を一意に識別します。 要素を格納するパッケージの修飾名が先頭につきます。|
|**作業項目**|関連付けなし|All|この要素に関連付けられている作業項目の数。 作業項目を関連付けるには、「 [モデル要素と作業項目のリンク](../modeling/link-model-elements-and-work-items.md)」を参照してください。|
|**説明**|(空白)|All|ここに、項目に関する一般的なメモを作成できます。|
|**色**|(要素の型の既定値)|生存線、メッセージ|シェイプの色。 これは、図形が表示する要素ではなく、図形のプロパティです。|
|**Type**|(空白)|生存線|生存線を表すインスタンスの型。<br /><br /> 生存線のヘッダーに表示される参照シンボルがある場合は、このクラスまたはインターフェイスは UML モデル エクスプローラーで個別に存在していて、クラス図に表示することができます。|
|**俳優**|×|生存線|生存線は、この図の対象となるコンポーネントに対して外部となるユーザー、デバイス、またはソフトウェア コンポーネントを表すかどうかを示します。|
|**種類**|**Complete** -送信側と受信側の両方を含むメッセージ。<br /><br /> **Found** -送信者が指定されていないメッセージ。<br /><br /> **Lost** -指定されていない受信者を持つメッセージ。|Message|メッセージのどちらの終端を生存線にアタッチするかを示します。<br /><br /> このプロパティは変更できません。 これは、メッセージを作成するときに設定されます。|
|**Sort**|**AsynchCall** -非同期メッセージ。<br /><br /> **SynchCall** -同期メッセージ。<br /><br /> **Reply** -同期メッセージの戻り部分。<br /><br /> **CreateMessage** -インスタンス作成メッセージ。|Message|メッセージの種類。 このプロパティは変更できません。 メッセージの作成に使用するツールによって決定されます。|
|**操作**|(空)|Message|受信側の生存線のメッセージによって呼び出されるメソッド。<br /><br /> 受信側の生存線が、インターフェイスまたはクラスにリンクされている場合にのみ表示されます。|
|**参照先**|シーケンス図|相互作用使用|この相互作用使用によって呼び出されるシーケンス図。|
|**相互作用演算子**|[ **ブロック** の挿入] コマンドを使用したときに設定されます。|結合フラグメント|このフラグメントまたはフラグメントのコレクションが表す演算子。|
|**主催**|(空)|結合フラグメント内の相互作用オペランド|ガードが True でない限り、フラグメント内のシーケンスは発生しません。<br /><br /> 結合フラグメントの一番上のフラグメントを選択するには、フラグメントのタイトルの下をクリックします。|
|**最小、最大**|(制限なし)|ループ結合フラグメント|ループ実行回数の最小値と最大数。|
|**Messages (メッセージ)**|(空)|とを検討します。<br /><br /> 結合フラグメントの無視|このフラグメント内で検討または無視するメッセージ。|

## <a name="see-also"></a>参照
 [Uml シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md) [uml シーケンス図: ガイドライン](../modeling/uml-sequence-diagrams-guidelines.md)に [ついて uml シーケンス図のフラグメントを使用した制御フロー](../modeling/describe-control-flow-with-fragments-on-uml-sequence-diagrams.md)
