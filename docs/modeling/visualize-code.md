---
title: コードの視覚化
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- code, understanding
- code, visualizing
- code, exploring
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 56b938321c2b6d1161052ac2358547d72a6bf4e7
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75593994"
---
# <a name="visualize-code"></a>コードの視覚化

Visual Studio の視覚化ツールとモデリング ツールを使って、既存のコードを理解し、アプリケーションを記述することができます。 これにより、自分が実行した変更がコードにどのような影響を与えるかを理解し、その変更に起因する作業とリスクを評価することができます。 例:

- コード内のリレーションシップを理解するには、そのリレーションシップをビジュアルにマッピングします。

- システムのアーキテクチャを記述し、コードの設計との一貫性を維持するには、依存関係図を作成し、これらの図に対してコードを検証します。

- クラス構造を記述するには、クラス ダイアグラムを作成します。

またこれらのツールを使用すると、プロジェクトの関係者と簡単にやり取りすることができます。

各機能をサポートする Visual Studio のエディションについては、「[アーキテクチャツールとモデリングツールのエディションサポート](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

## <a name="what-do-you-want-to-do"></a>作業内容

|||
|-|-|
|**コードとその関係について説明します。**<br /><br /> 特定のコード間のリレーションシップをマッピングします。<br /><br /> ソリューション全体のコード内のリレーションシップの概要を確認します。|[ソリューション間の依存関係をマップ - に](../modeling/map-dependencies-across-your-solutions.md)は<br />[コードマップを使用してアプリケーションをデバッグ - には](../modeling/use-code-maps-to-debug-your-applications.md)<br />[コードマップアナライザーを使用して潜在的な問題を検出](../modeling/find-potential-problems-using-code-map-analyzers.md)- には<br />[デバッグ中に呼び出し履歴のメソッドを - マップする](../debugger/map-methods-on-the-call-stack-while-debugging-in-visual-studio.md)|
|**クラス構造について:**<br /><br /> コードからクラス ダイアグラムを作成することで、プロジェクト内のクラスの構造を視覚化します。|[方法: プロジェクトにクラス ダイアグラムを追加する (クラス デザイナー)](../ide/class-designer/how-to-add-class-diagrams-to-projects.md)|
|**高レベルのシステム設計について説明し、この設計に対してコードを検証します。**<br /><br /> 依存関係図を作成して、システム設計の概要とその依存関係を記述します。 このデザインと照らし合わせてコードを検証し、コード内の依存関係がデザインと一貫性があることを確認します。|[コードから依存関係図を作成 - に](../modeling/create-layer-diagrams-from-your-code.md)は<br />- [依存関係図: リファレンス](../modeling/layer-diagrams-reference.md)<br />- [依存関係図: ガイドライン](../modeling/layer-diagrams-guidelines.md)<br />[依存関係図を使用してコードを検証 - に](../modeling/validate-code-with-layer-diagrams.md)は|

## <a name="see-also"></a>関連項目

- [シナリオ: 視覚化およびモデリングを使用したデザインの変更](../modeling/scenario-change-your-design-using-visualization-and-modeling.md)
- [分析とモデルのアーキテクチャ](../modeling/analyze-and-model-your-architecture.md)
- [アプリのアーキテクチャをモデル化する](../modeling/model-your-app-s-architecture.md)
- [開発プロセス内でのモデルの使用](../modeling/use-models-in-your-development-process.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
