---
title: UML モデリング機能拡張の API リファレンス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: reference
helpviewer_keywords:
- UML - extending
- UML API
- UML model, API
ms.assetid: 2b2ffe93-c358-4d28-a5e5-3d0474629b58
caps.latest.revision: 11
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: e48bf723b8b1cb77cc1f7f4de9cfb562caccde84
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72672808"
---
# <a name="api-reference-for-uml-modeling-extensibility"></a>UML モデリング機能拡張の API リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プログラム コードを記述して、Visual Studio を使用して作成したモデルを読み取ったり、変更したりすることができます。 API リファレンスには、この操作を実行するために役に立つ、特定のクラスに関する情報が掲載されています。 タスク指向の詳細については、「 [UML モデルと図の拡張](../modeling/extend-uml-models-and-diagrams.md)」のトピックを参照してください。 UML モデルをサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="assemblies"></a>アセンブリ

|アセンブリ|実行できる操作|
|--------------|--------------------------------|
|Microsoft.VisualStudio.Uml.Interfaces.dll|-IUseCase、IAssociation などのモデル要素の読み取りと変更を行います。<br />-要素間のリレーションシップをナビゲートします。<br /><br /> 名前空間と型は、UML 仕様で定義されたものに対応しています。|
|Microsoft.VisualStudio.ArchitectureTools.Extensibility.dll|-モデル要素の新しいインスタンスを作成します<br />-図形と図にアクセスして変更します。|

## <a name="see-also"></a>参照
 [UML モデルと図を拡張](../modeling/extend-uml-models-and-diagrams.md)する [Visual STUDIO のモデリング SDK の API リファレンス](../modeling/api-reference-for-modeling-sdk-for-visual-studio.md)
