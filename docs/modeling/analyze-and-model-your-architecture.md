---
title: アーキテクチャを分析およびモデルする
description: Visual Studio アーキテクチャおよびモデリング ツールを使用してアプリを設計およびモデル化し、アプリがアーキテクチャ要件を満たすようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: overview
helpviewer_keywords:
- diagrams - modeling
- architecture
- code visualization
- application design
- code exploration
- modeling
- application architecture
- architecture [Visual Studio ALM], modeling
- application modeling
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 71296b9ccb2e442d1bd9bc13865e0086821bf030
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97361158"
---
# <a name="analyze-and-model-your-architecture"></a>アーキテクチャを分析およびモデルする

Visual Studio アーキテクチャおよびモデリング ツールを使用してアプリを設計およびモデル化することによって、アーキテクチャ要件を満たすアプリを作成できます。

* Visual Studio を使用してコードの構造、動作、および関係を視覚化することによって、既存のプログラム コードを容易に理解できるようになります。

* アーキテクチャの依存関係を尊重する必要があることをチームに教育します。

* 開発プロセスの一部として、アプリケーション ライフサイクル全体においてさまざまな詳細レベルでモデルを作成できます。

「[シナリオ: 視覚化およびモデリングを使用したデザインの変更](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)」を参照してください。

## <a name="article-reference"></a>記事リファレンス

|シナリオ|[アーティクル]|
|-|-|
|**コードの視覚化**:<br /><br />- コード マップを作成して、コードの編成や関係を調べます。 アセンブリ、名前空間、クラス、メソッドなどの間の依存関係を視覚化します。<br />- コードからクラス図を作成して、特定のプロジェクトの構造とメンバーを調べます。<br />- 依存関係図を作成して、コードと設計の間の競合を見つけ、コードを検証します。|- [コードの視覚化](../modeling/visualize-code.md)<br />- [クラスと他の型の使用 (クラス デザイナー)](../ide/class-designer/designing-and-viewing-classes-and-types.md)<br />- [ビデオ: Visual Studio 2015 コード マップを使用してコードからのデザインを理解する](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2015/502)<br />- [ビデオ: アーキテクチャの依存関係をリアルタイムで検証する](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)|
|**アーキテクチャを定義する**:<br /><br />- 依存関係図を作成し、コードのコンポーネント間の依存関係に対する制約を定義して適用します。|- [ビデオ: Visual Studio を使用してアーキテクチャの依存関係を検証する (Channel 9)](https://channel9.msdn.com/Events/Connect/2016/170)|
|**要求と、必要とされる設計を照らし合わせてシステムを検証する:**<br /><br />- 目的のアーキテクチャが記述された依存関係図を使用してコードの依存関係を検証し、設計と競合する可能性がある変更を防止します。|- [ビデオ: Visual Studio を使用してアーキテクチャの依存関係を検証する (Channel 9)](https://channel9.msdn.com/Events/Connect/2016/170)|
|**モデルと図をカスタマイズする**:<br /><br />- 独自のドメイン固有言語を作成します。|- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**T4 テンプレートを使用してテキストを生成する**:<br /><br />- テンプレート内部のテキスト ブロックと制御ロジックを使用して、テキスト ベースのファイルを生成します。<br /> - Visual Studio に含まれている MSBuild を使用した T4 テンプレートのビルド|- [コード生成と T4 テキスト テンプレート](../modeling/code-generation-and-t4-text-templates.md)|
|**Team Foundation バージョン コントロールを使用してモデル、図、およびコード マップを共有する**:<br /><br />- コード マップ、プロジェクト、依存関係図を Team Foundation のバージョン管理下に置き、共有できるようにします。| |

各機能がサポートされる Visual Studio のバージョンを確認するには、「[アーキテクチャとモデリング ツールのエディション サポート](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください

## <a name="types-of-models-and-typical-uses"></a>モデルの種類と一般的な用途

### <a name="code-maps"></a>コード マップ

コード マップは、コードの編成や関係を理解するために役立ちます。

**一般的な用途:**

- コードの構造と依存関係および更新方法の理解を深め、提案された変更のコストを見積もることができるように、プログラム コードを調べます。

**次を参照してください。**

- [ソリューション間の依存関係をマップする](../modeling/map-dependencies-across-your-solutions.md)
- [コード マップを使用してアプリケーションをデバッグする](../modeling/use-code-maps-to-debug-your-applications.md)
- [コード マップ アナライザーを使用して潜在的な問題を検索する](../modeling/find-potential-problems-using-code-map-analyzers.md)

### <a name="dependency-diagrams"></a>依存関係図

依存関係図を使用すると、アプリケーションの構造を一連のレイヤーまたは明示的な依存関係があるブロックとして定義できます。 ライブ検証では、コードの依存関係と依存関係図に記述されている依存関係との競合が表示されます。

**一般的な用途:**

- アプリケーションのライフサイクルを通じて多数の変更を行うことにより、アプリケーションの構造を安定化する。
- コードへの変更をチェックインする前に、意図しない依存関係の競合を検出します。

**次を参照してください。**

- [コードからの依存関係図の作成](../modeling/create-layer-diagrams-from-your-code.md)
- [依存関係図: リファレンス](../modeling/layer-diagrams-reference.md)
- [依存関係図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)

### <a name="domain-specific-language-dsl"></a>ドメイン固有言語 (DSL)

DSL は、特定の目的のために設計する表記法です。 Visual Studio では、通常、グラフィックです。

**一般的な用途:**

- アプリケーションの各部分を生成または構成する。 表記法およびツールを開発するには、作業が必要です。 これを行うと、UML のカスタマイズよりもドメインに適合する結果となることがあります。
- DSL およびそのツールの開発への投資が複数のプロジェクトでの DSL の利用という結果をもたらす大規模プロジェクトまたは製品ライン。

**次を参照してください。**

- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

## <a name="see-also"></a>関連項目

- [Visual Studio 2017 のモデリングの新機能](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps とアプリケーション ライフサイクル管理](/azure/devops/user-guide/devops-alm-overview)
