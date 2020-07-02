---
title: アーキテクチャを分析およびモデルする
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
ms.openlocfilehash: e1db28867ea47752aa74b7898c44e797c0704594
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85544223"
---
# <a name="analyze-and-model-your-architecture"></a>アーキテクチャを分析およびモデルする

アプリを設計してモデル化するための Visual Studio アーキテクチャとモデリングツールを使用して、アプリがアーキテクチャの要件を満たしていることを確認します。

* Visual Studio を使用してコードの構造、動作、および関係を視覚化することによって、既存のプログラム コードを容易に理解できるようになります。

* アーキテクチャの依存関係を尊重する必要があることをチームに教育します。

* 開発プロセスの一部として、アプリケーション ライフサイクル全体においてさまざまな詳細レベルでモデルを作成できます。

「[シナリオ: 視覚化とモデリングを使用してデザインを変更する](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)」を参照してください。

## <a name="article-reference"></a>記事リファレンス

|シナリオ|記事|
|-|-|
|**コードの視覚化**:<br /><br />-コードマップを作成して、コードの編成と関係を確認します。 アセンブリ、名前空間、クラス、メソッドなどの間の依存関係を視覚化します。<br />-コードからクラスダイアグラムを作成して、特定のプロジェクトのクラス構造とメンバーを参照してください。<br />-コードを検証するための依存関係図を作成して、コードとそのデザインとの間の競合を検出します。|- [コードを視覚化する](../modeling/visualize-code.md)<br />- [クラスとその他の型の使用 (クラスデザイナー)](../ide/class-designer/designing-and-viewing-classes-and-types.md)<br />- [ビデオ: Visual Studio 2015 コードマップでコードのデザインを理解する](https://channel9.msdn.com/Events/Visual-Studio/Connect-event-2015/502)<br />- [ビデオ: アーキテクチャの依存関係をリアルタイムで検証する](https://sec.ch9.ms/sessions/69613110-c334-4f25-bb36-08e5a93456b5/170ValidateArchitectureDependenciesWithVisualStudio.mp4)|
|**アーキテクチャを定義する**:<br /><br />-依存関係図を作成して、コードのコンポーネント間の依存関係に対する制約を定義し、適用します。|- [ビデオ: Visual Studio を使用してアーキテクチャの依存関係を検証する (Channel 9)](https://channel9.msdn.com/Events/Connect/2016/170)|
|**要求と、必要とされる設計を照らし合わせてシステムを検証する:**<br /><br />-目的のアーキテクチャを記述する依存関係図でコードの依存関係を検証し、設計と競合する可能性のある変更を防止します。|- [ビデオ: Visual Studio を使用してアーキテクチャの依存関係を検証する (Channel 9)](https://channel9.msdn.com/Events/Connect/2016/170)|
|**モデルと図をカスタマイズする**:<br /><br />-ドメイン固有の言語を独自に作成します。|- [モデリング SDK for Visual Studio-ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)|
|**T4 テンプレートを使用してテキストを生成する**:<br /><br />-テンプレート内のテキストブロックとコントロールロジックを使用して、テキストベースのファイルを生成します。<br /> -Visual Studio に含まれる MSBuild を使用した T4 テンプレートビルド|- [コード生成と T4 テキストテンプレート](../modeling/code-generation-and-t4-text-templates.md)|
|**Team Foundation バージョン コントロールを使用してモデル、図、およびコード マップを共有する**:<br /><br />-コードマップ、プロジェクト、依存関係図を Team Foundation バージョン管理下に配置して、共有できるようにします。| |

各機能をサポートする Visual Studio のエディションについては、「[アーキテクチャツールとモデリングツールのエディションサポート](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

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

依存関係図を使用すると、アプリケーションの構造を一連のレイヤーまたは明示的な依存関係があるブロックとして定義できます。 ライブ検証では、コード内の依存関係と依存関係図に記述されている依存関係との間の競合が表示されます。

**一般的な用途:**

- アプリケーションのライフサイクルを通じて多数の変更を行うことにより、アプリケーションの構造を安定化する。
- コードへの変更をチェックインする前に、意図しない依存関係の競合を検出します。

**次を参照してください。**

- [コードからの依存関係図の作成](../modeling/create-layer-diagrams-from-your-code.md)
- [依存関係図: リファレンス](../modeling/layer-diagrams-reference.md)
- [依存関係図を使用したコードの検証](../modeling/validate-code-with-layer-diagrams.md)

### <a name="domain-specific-language-dsl"></a>ドメイン固有言語 (DSL)

DSL は、特定の目的のために設計する表記法です。 Visual Studio では、通常はグラフィカルです。

**一般的な用途:**

- アプリケーションの各部分を生成または構成する。 表記法およびツールを開発するには、作業が必要です。 これを行うと、UML のカスタマイズよりもドメインに適合する結果となることがあります。
- DSL およびそのツールの開発への投資が複数のプロジェクトでの DSL の利用という結果をもたらす大規模プロジェクトまたは製品ライン。

**次を参照してください。**

- [Modeling SDK for Visual Studio - ドメイン固有言語](../modeling/modeling-sdk-for-visual-studio-domain-specific-languages.md)

## <a name="see-also"></a>関連項目

- [Visual Studio 2017 でのモデリングの新機能](../modeling/what-s-new-for-design-in-visual-studio.md)
- [DevOps とアプリケーション ライフサイクル管理](/azure/devops/user-guide/devops-alm-overview)
