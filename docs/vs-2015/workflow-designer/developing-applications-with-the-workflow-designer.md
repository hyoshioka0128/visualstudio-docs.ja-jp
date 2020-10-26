---
title: ワークフローデザイナー | を使用したアプリケーションの開発Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-workflow-designer
ms.topic: reference
f1_keywords:
- DefaultWorkflowDesigner
- DefaultWorkflowDesigner.UI
helpviewer_keywords:
- Visual Studio 2010 Workflow Designer [WFD], overview
- Workflow Designer [WFD]
- Visual Studio 2010 Workflow Designer [WFD]
- Workflow Designer [WFD], overview
ms.assetid: 4cd062b1-b496-4668-bbc1-ee85545e066d
caps.latest.revision: 17
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 848300c54800e229ee1f487fc415bad45d982a6c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72656823"
---
# <a name="developing-applications-with-the-workflow-designer"></a>ワークフロー デザイナーを使用したアプリケーションの開発
[!INCLUDE[wfd1](../includes/wfd1-md.md)]は、[!INCLUDE[wf](../includes/wf-md.md)] 開発環境内でホストされる [!INCLUDE[netfx40_long](../includes/netfx40-long-md.md)] 内の [!INCLUDE[vs2010](../includes/vs2010-md.md)] アプリケーションをグラフィカルに作成してデバッグするためのビジュアルなデザイナーおよびデバッガーです。 テンプレートおよびアクティビティ デザイナーを使用して、複合ワークフロー アプリケーション、アクティビティ ライブラリ、または [!INCLUDE[indigo1](../includes/indigo1-md.md)] サービスを作成できます。 [!INCLUDE[crabout](../includes/crabout-md.md)] ワークフローについては、 [Windows Workflow Foundation &#91; .NET Framework 4&#93;](https://msdn.microsoft.com/library/9a23ea6b-d600-483e-89cd-8889cfec5f66)を参照してください。

 以前のバージョンの[!INCLUDE[wfd2](../includes/wfd2-md.md)]に追加された、この新バージョンの[!INCLUDE[wfd2](../includes/wfd2-md.md)]のデザイン機能を次に示します。

- [!INCLUDE[wfd2](../includes/wfd2-md.md)]は、[!INCLUDE[avalon1](../includes/avalon1-md.md)] を使用して構築されています。 これにより、アクティビティ デザイナーのエクスペリエンスが向上し、大規模で複雑なワークフローに対するパフォーマンスが改善されます。

- カスタム アクティビティを、[!INCLUDE[avalon2](../includes/avalon2-md.md)] で XAML を使用してデザインできます。また、アクティビティ デザイナーを作成するためのプログラミング モデルが単純化されています。

- Flowchart アクティビティの実装により、一般的なフローチャート モデル化スタイルを使用して、プログラム フローを視覚的に表現できます。

- [!INCLUDE[wfd2](../includes/wfd2-md.md)]の新しい変数デザイナーにより、ワークフロー内の変数を宣言してスコープを設定し、アクティビティにバインドできます。

- [!INCLUDE[vs2010](../includes/vs2010-md.md)] では、[!INCLUDE[wfd2](../includes/wfd2-md.md)] ワークフロー内で Visual Basic 式を作成するときに、[!INCLUDE[netfx40_short](../includes/netfx40-short-md.md)]で IntelliSense の機能をすべて利用できます。

- デバッグ用の機能が XAML にも拡張されているため、XAML ワークフロー定義にブレークポイントを設定して、実行時に XAML コードにステップ インすることができます。ここでは、マネージド コードを扱う場合と同じように操作できます。

- [!INCLUDE[wfd2](../includes/wfd2-md.md)] の外側での[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]の再ホストが、以前のバージョンに比べて大幅に簡略化され、数行のコードのみになりました。

- 新しい <xref:System.Activities.Statements.Flowchart> アクティビティとその [フローチャート](../workflow-designer/flowchart-activity-designer.md) を使用すると、使い慣れたフローチャートモデリングスタイルを使用してプログラムフローを視覚化できます。

- メッセージング アクティビティが強化されているため、完全な宣言型の (コードなし) [!INCLUDE[indigo1](../includes/indigo1-md.md)] サービスを記述できます。

- サービス参照の追加.. **.** 機能を使用すると、Web サービスにアクセスするアクティビティを自動的に生成できます。

## <a name="in-this-section"></a>このセクションの内容
 [ワークフローデザイナーの使用](../workflow-designer/using-the-workflow-designer.md) 組み込みのデザイナーを使用して新しいアクティビティおよびワークフロープロジェクトを作成する方法と、デザイナーによって提供される他のツールを使用して引数、変数、式、インポート、および階層リンクナビゲーションを処理する方法を示します。

 [アクティビティデザイナーの使用](../workflow-designer/using-the-activity-designers.md) システムによって提供されるアクティビティ、テンプレート、およびそのデザイナーのカテゴリについて説明します。

 [ワークフローデザイナーを使用したワークフローのデバッグ](../workflow-designer/debugging-workflows-with-the-workflow-designer.md) 従来のデバッグ手順を実行する方法と、XAML と式をデバッグする方法について説明します。

 [ワークフローデザイナー UI のヘルプ](../workflow-designer/workflow-designer-ui-help.md) によって提供されるダイアログボックスの状況依存のヘルプトピック、 [!INCLUDE[wfd1](../includes/wfd1-md.md)] およびデザイナーシェル機能、キーボードショートカット、およびエラーメッセージに関するガイダンスが含まれています。

 [.Net 3.0 または .net 3.5 Framework を対象とするワークフローアプリケーションの開発](../workflow-designer/developing-workflow-applications-targeting-the-dotnet-3-0-or-dotnet-3-5-framework.md) またはを対象とする従来のデザイナーの使用に関するガイダンスが含まれてい [!INCLUDE[netfx35_long](../includes/netfx35-long-md.md)] [!INCLUDE[vstecwinfx](../includes/vstecwinfx-md.md)] ます。

 [デザイナーのホスト &#91;WF サンプル&#93;](https://msdn.microsoft.com/library/b676ad31-5f64-4d84-9a36-b4d7113a2f4d) このサンプルでは、デザイナーを含む WPF レイアウトを作成する方法を示します。

 [カスタムアクティビティデザイナー](https://msdn.microsoft.com/library/dcf14dca-ce6d-4278-96ba-062f0a679075) このセクションには、ワークフローデザイナーでの表示にカスタムデザイナーを使用するアクティビティサンプルが含まれています。