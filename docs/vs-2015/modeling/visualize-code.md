---
title: コードの視覚化 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- code, understanding
- code, visualizing
- code, exploring
ms.assetid: 0dd7d438-393a-4cd3-b417-9bf37379e1b0
caps.latest.revision: 49
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 665dc76126eac964f405be06605c40b5b30cc9a5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85532939"
---
# <a name="visualize-code"></a>コードの視覚化
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio の視覚化ツールとモデリング ツールを使って、既存のコードを理解し、アプリケーションを記述することができます。 これにより、自分が実行した変更がコードにどのような影響を与えるかを理解し、その変更に起因する作業とリスクを評価することができます。 次に例を示します。

- コード内のリレーションシップを理解するには、そのリレーションシップをビジュアルにマッピングします。

- システムのアーキテクチャを記述し、デザインとコードの一貫性を維持するには、レイヤー図を作成し、それらの図と照らし合わせてコードを検証します。

- クラス構造を記述するには、クラス ダイアグラムを作成します。

- システムのさまざまな面をモデル化して通信するには、Unified Modeling Language (UML) ダイアグラムを作成します。 たとえば、システムのコンポーネント、型、相互作用、およびプロセスをモデル化することができます。

  またこれらのツールを使用すると、プロジェクトの関係者と簡単にやり取りすることができます。 たとえば、UML クラス ダイアグラムを使って、プロジェクトの関係者、ユーザー、およびチーム メンバーとシステムについて検討するための共通の用語集を作成することができます。

  各機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="what-do-you-want-to-do"></a>実行する操作

|シナリオ|[アーティクル]|
|-|-|
|**コードとそのリレーションシップについて:**<br /><br /> 特定のコード間のリレーションシップをマッピングします。<br /><br /> ソリューション全体のコード内のリレーションシップの概要を確認します。<br /><br /> **注**: Visual Studio のこのリリースでは、 *依存関係グラフ* の代わりに、 *コード マップ*という用語を使用します。|-   [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)<br />-   [コードマップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)<br />-   [コードマップアナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)<br />-   [デバッグ中に呼び出し履歴のメソッドをマップする](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)|
|**クラス構造について:**<br /><br /> コードからクラス ダイアグラムを作成することで、プロジェクト内のクラスの構造を視覚化します。|[方法: プロジェクトにクラス ダイアグラムを追加する (クラス デザイナー)](../ide/how-to-add-class-diagrams-to-projects-class-designer.md)|
|**高レベルのシステム デザインを記述し、そのデザインに対してコードを検証します:**<br /><br /> レイヤー図を作成することで、高レベルのシステム デザインと想定する依存関係を記述します。 このデザインと照らし合わせてコードを検証し、コード内の依存関係がデザインと一貫性があることを確認します。|-   [コードからレイヤー図を作成する](../modeling/create-layer-diagrams-from-your-code.md)<br />-   [レイヤー図: リファレンス](../modeling/layer-diagrams-reference.md)<br />-   [レイヤー図: ガイドライン](../modeling/layer-diagrams-guidelines.md)<br />-   [レイヤー図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)|
|**ユーザー要求とアーキテクチャをやり取りします。**<br /><br /> 次の UML 図 (アクティビティ、コンポーネント、クラス、シーケンス、使用例) を描画することで、ソフトウェア システムのユーザー要求とアーキテクチャをモデル化します。|-   [アプリのモデルを作成する](../modeling/create-models-for-your-app.md)<br />-   [ユーザー要件のモデル化](../modeling/model-user-requirements.md)<br />-   [アプリのアーキテクチャをモデル化する](../modeling/model-your-app-s-architecture.md)|

## <a name="external-resources"></a>外部リソース

|**カテゴリ**|**リンク**|
|------------------|---------------|
|**フォーラム**|-   [Visual Studio の視覚化ツールとモデリング ツール](https://social.msdn.microsoft.com/Forums/en-US/home?forum=vsarch)<br />-   [Visual Studio の視覚化およびモデリング SDK (DSL ツール)](https://social.msdn.microsoft.com/Forums/home?forum=dslvsarchx)|
|**ブログ**|[Visual Studio ALM + Team Foundation Server のブログ](https://devblogs.microsoft.com/devops/welcome-to-the-visual-studio-alm-team-foundation-server-blog/)|
|**技術記事とジャーナル**|[MSDN アーキテクチャフォーラム](https://msdn.microsoft.com/architecture/default.aspx)|

## <a name="see-also"></a>参照
 [シナリオ: 視覚化とモデリングを使用して設計を変更する](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)[アーキテクチャ分析とモデリングアーキテクチャ](../modeling/analyze-and-model-your-architecture.md)[アプリモデルのモデルを作成](../modeling/create-models-for-your-app.md)する[ユーザーの要件](../modeling/model-user-requirements.md)[モデルアプリのアーキテクチャ](../modeling/model-your-app-s-architecture.md)を[開発プロセスで使用するモデルを使用する](../modeling/use-models-in-your-development-process.md)
