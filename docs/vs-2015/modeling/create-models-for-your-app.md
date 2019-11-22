---
title: Create models for your app | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
f1_keywords:
- vs.teamarch.common.commentlink.properties
- vs.teamarch.UMLModelExplorer.dependency
- vs.teamarch.UMLModelExplorer.commentlink
- vs.teamarch.common.dependency.properties
- Microsoft.VisualStudio.Uml.Diagrams.CommentShape.IsTransparent
- vs.teamarch.common.comment.properties
- vs.teamarch.UMLModelExplorer.comment
helpviewer_keywords:
- diagrams - modeling, sequence
- software design
- diagrams - modeling, use case
- diagrams - modeling, component
- diagrams - modeling, UML component
- UML model
- diagrams - modeling, UML use case
- diagrams - modeling, class
- diagrams - modeling, activity
- diagrams - modeling, UML activity
- software modeling
- diagrams - modeling, UML sequence
- UML
- diagrams - modeling, UML
- diagrams - modeling, layer
- software, designing
- diagrams - modeling, UML class
- software, modeling
- UML diagrams
ms.assetid: b69d9d91-c7e7-4dee-8eb6-706076eecb85
caps.latest.revision: 60
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a9f20629c39bc37ca20550c3b88d8ecb2aca470f
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74300246"
---
# <a name="create-models-for-your-app"></a>アプリのモデルを生成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

モデリング図を使用すると、コードや、ソフトウェア システムで対応する必要があるユーザー要求について、効果的に理解して明確にし、アイデアを伝え合うことができます。 たとえば、ユーザー要求を記述して伝えるために、UML (Unified Modeling Language: 統一モデリング言語) のユース ケース図、アクティビティ図、クラス図、およびシーケンス図を使用できます。 システムの機能を記述して伝えるために、UML のコンポーネント図、クラス図、アクティビティ図、およびシーケンス図を使用できます。

 See [Channel 9 Video: Improve architecture through modeling](https://go.microsoft.com/fwlink/?LinkID=252078).

 このリリースでは、次の UML 図を作成できます。

|**図**|**表示される内容**|
|-----------------|---------------|
|[UML アクティビティ図: リファレンス](../modeling/uml-activity-diagrams-reference.md)|ビジネス プロセス内のアクションと参加者の間のワーク フロー|
|[UML コンポーネント図: リファレンス](../modeling/uml-component-diagrams-reference.md)|システム、そのインターフェイス、ポート、およびリレーションシップのコンポーネント|
|[UML クラス図: リファレンス](../modeling/uml-class-diagrams-reference.md)|システムとそれらのリレーションシップにおいて、データを格納して交換するために使用される型|
|[UML シーケンス図: リファレンス](../modeling/uml-sequence-diagrams-reference.md)|オブジェクト、コンポーネント、システム、またはアクターの間の相互作用の順序|
|[UML ユース ケース図: リファレンス](../modeling/uml-use-case-diagrams-reference.md)|ユーザーの目的、およびシステムでサポートするタスク|

 To see which versions of Visual Studio support each type of diagram, see [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport).

 システムまたは既存のコードのアーキテクチャを視覚化するには、次の図を作成します。

|**図**|**表示される内容**|
|-----------------|---------------|
|[レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)<br /><br /> [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)|システムのアーキテクチャの概要|
|コード マップ<br /><br /> [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)<br /><br /> [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)|既存のコード内の依存関係とその他の関係|
|コードで生成されたクラス図<br /><br /> [クラス ダイアグラムの使用 (クラス デザイナー)](../ide/working-with-class-diagrams-class-designer.md)|.NET コード内の型とその関係|

## <a name="common-tasks"></a>一般的なタスク

|**Topic**|**タスク**|
|---------------|--------------|
|[UML モデリング プロジェクトおよびダイアグラムを作成する](../modeling/create-uml-modeling-projects-and-diagrams.md)|**Create models** and add diagrams.|
|[UML モデルおよびダイアグラムの編集](../modeling/edit-uml-models-and-diagrams.md)|**Draw diagrams** to edit the model.|
|[パッケージと名前空間の定義](../modeling/define-packages-and-namespaces.md)|**Create packages** to divide a model into units that different team members can work on.|
|[UML クラス図からコードを生成する](../modeling/generate-code-from-uml-class-diagrams.md)|**Generate C# code from class diagrams** to start your implementation.|
|[プロファイルとステレオタイプを使用したモデルのカスタマイズ](../modeling/customize-your-model-with-profiles-and-stereotypes.md)|**Customize model elements** using stereotypes, to extend the standard UML model elements for specific purposes.|
|[モデル要素と作業項目とのリンク](../modeling/link-model-elements-and-work-items.md)|**Create links between model elements and work items** to help you track tasks, test cases, bugs, requirements, issues, or other kinds of work that are associated with specific parts of your model.|
|[イメージとしてダイアグラムをエクスポートする](../modeling/export-diagrams-as-images.md)|**Save your model and diagrams** so that you can share them with other users, including those who do not use [!INCLUDE[vsUltShort](../includes/vsultshort-md.md)].|

## <a name="related-tasks"></a>関連タスク

|**Topic**|**タスク**|
|---------------|--------------|
|[コードの視覚化](../modeling/visualize-code.md)|コード マップとレイヤー図を作成して、よく知らないコードの理解を深めます。|
|[ユーザー要件のモデリング](../modeling/model-user-requirements.md)|モデルを使用して、ユーザーのニーズを明確にして伝えます。|
|[アプリのアーキテクチャをモデル化する](../modeling/model-your-app-s-architecture.md)|モデルを使用して、システムの全体的な構造と動作を記述し、確実にユーザーのニーズを満たせるようにします。|
|[開発時のシステムの検証](../modeling/validate-your-system-during-development.md)|ソフトウェアがユーザーのニーズ、およびシステムのアーキテクチャ全体と一致していることを確認します。|
|[開発プロセス内でのモデルの使用](../modeling/use-models-in-your-development-process.md)<br /><br /> [Use models in Agile development](https://msdn.microsoft.com/592ac27c-3d3e-454a-9c38-b76658ed137f)|モデルを使用すると、システムの開発中に効果的にシステムを理解して変更することができます。|
|[モデリング ソリューションの構築](../modeling/structure-your-modeling-solution.md)|大規模または中規模のプロジェクトでモデルを整理します。|

## <a name="external-resources"></a>外部リソース

|**カテゴリ**|**Links**|
|------------------|---------------|
|**フォーラム**|-   [Visual Studio の視覚化ツールとモデリング ツール](https://go.microsoft.com/fwlink/?LinkId=184720)<br />-   [Visual Studio の視覚化およびモデリング SDK (DSL ツール)](https://go.microsoft.com/fwlink/?LinkId=184721)|
