---
title: Validate your system during development | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- layer diagrams
ms.assetid: c9dafb47-7b1d-4c72-9432-d43be3db1799
caps.latest.revision: 39
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 4fec3595ba7886f5ba979c35e9441ab108174726
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74301338"
---
# <a name="validate-your-system-during-development"></a>開発時のシステムの検証
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio を使用すると、ソフトウェアがユーザーの要件とシステムのアーキテクチャに合致した状態を維持することができます。

 これらの各機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="key-tasks"></a>主なタスク
 ソフトウェアを検証するには、次のタスクを使用します。

|**タスク**|**関連するトピック**|
|---------------|---------------------------|
|**Make sure your model is consistent:**<br /><br /> プロジェクトでのモデルの使用方法および解釈方法によっては、いくつかの要素の組み合わせを許可しないようにすると効果的です。 たとえば、必ず [!INCLUDE[TLA2#tla_net](../includes/tla2sharptla-net-md.md)]に準拠した名前を使用するように UML クラスを制限することができます。 そのような制約は [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の拡張機能で定義できます。|-   [Validate your UML model](../modeling/validate-your-uml-model.md)<br />-   [Define validation constraints for UML models](../modeling/define-validation-constraints-for-uml-models.md)|
|**ソフトウェアがユーザーの要件を満たしているか確認する**:<br /><br /> システムとそのコンポーネントのテストを編成する際に、要件モデルとアーキテクチャ モデルを使用できます。 こうすることで、ユーザーやその他の利害関係者にとって重要な要求をテストしやすくなり、要求が変更された場合にすばやくテストを更新することができます。|-   [Develop tests from a model](../modeling/develop-tests-from-a-model.md)|
|**ソフトウェアが、意図されたシステム設計に合致した状態を保っているか確認する:**<br /><br /> レイヤー図は、アプリケーションのコンポーネント間の、意図された依存関係を表します。 開発中に、コード内の実際の依存関係が、意図された設計に準拠しているか検証できます。|-   [Create layer diagrams from your code](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [Validate code with layer diagrams](../modeling/validate-code-with-layer-diagrams.md)|

## <a name="external-resources"></a>外部リソース

|**カテゴリ**|**Links**|
|------------------|---------------|
|**ビデオ**|![link to video](../data-tools/media/playvideo.gif "PlayVideo") [Channel 9: Doug Seven: Code Understanding and System Design with Visual Studio 2010](https://go.microsoft.com/fwlink/?LinkId=216100)<br /><br /> ![link to video](../data-tools/media/playvideo.gif "PlayVideo") [Channel 9: Architecting an Application using a Layer Diagram](https://go.microsoft.com/fwlink/?LinkID=201117)<br /><br /> ![link to video](../data-tools/media/playvideo.gif "PlayVideo") [MSDN How Do I Series: How to Validate Code using Layer Diagrams](https://go.microsoft.com/fwlink/?LinkID=214405)|
|**フォーラム**|-   [Visual Studio の視覚化ツールとモデリング ツール](https://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio の視覚化およびモデリング SDK (DSL ツール)](https://go.microsoft.com/fwlink/?LinkId=184721)|
|**ブログ**|-   [Visual Studio ALM + Team Foundation Server のブログ](https://go.microsoft.com/fwlink/?LinkID=201340)|
|**技術記事とジャーナル**|[MSDN アーキテクチャ センター](https://go.microsoft.com/fwlink/?LinkId=201343)|

## <a name="see-also"></a>参照
 [Testing the application](https://msdn.microsoft.com/library/796b7d6d-ad45-4772-9719-55eaf5490dac) [Extend UML models and diagrams](../modeling/extend-uml-models-and-diagrams.md) [Model user requirements](../modeling/model-user-requirements.md) [Analyzing and Modeling Architecture](../modeling/analyze-and-model-your-architecture.md)
