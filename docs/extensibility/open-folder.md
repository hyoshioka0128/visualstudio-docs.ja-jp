---
title: Visual Studio の [フォルダーを開く] 機能拡張の概要 | Microsoft Docs
ms.date: 02/21/2018
ms.topic: overview
ms.assetid: 94c3f8bf-1de3-40ea-aded-7f40c4b314c7
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 964b360806f6f834aa57c475d2117c124f2cf8af
ms.sourcegitcommit: 8a0d0f4c4910e2feb3bc7bd19e8f49629df78df5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/18/2020
ms.locfileid: "97668639"
---
# <a name="open-folder-extensibility"></a>[フォルダーを開く] 機能拡張

[[フォルダーを開く]](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) 機能を使用すると、ユーザーはプロジェクトやソリューション ファイルを使用しなくても、Visual Studio で任意のコードベースを開くことができます。 "フォルダーを開く" では、Visual Studio のユーザーに期待される次のような機能を提供します。

* ソリューション エクスプローラーの統合と検索
* エディターの色設定
* [移動] ナビゲーション
* 対象を指定して検索

.NET や C++ 開発などのワークロードで使用すると、ユーザーは次の機能も利用できます。

* 機能豊富な Intellisense
* 言語固有の機能

[フォルダーを開く] を使用すると、拡張機能の作成者は任意の言語向けに豊富な機能を作成できます。 ユーザーのコードベース内の任意のファイルに対してビルド、デバッグ、シンボル検索がサポートされる API があります。 現在のエクステンダーを使用すると、既存の Visual Studio 機能を更新して、プロジェクトやソリューションを利用しなくてもコードを理解できます。

## <a name="an-api-without-project-systems"></a>プロジェクト システムなしの API

従来、Visual Studio では、プロジェクト システムを使用して、ソリューションとそのプロジェクトのファイルのみを認識していました。 プロジェクト システムは、読み込まれたプロジェクトの機能とユーザー操作を担当します。 プロジェクトに含まれるファイル、プロジェクトの内容の視覚的な表現、他のプロジェクトへの依存関係、および基になるプロジェクト ファイルの変更が認識されます。 これらの階層と機能を使用して、他のコンポーネントがユーザーに代わって機能します。 すべてのコードベースがプロジェクトおよびソリューション構造で適切に表現されているわけではありません。 C++ for Linux で記述されたスクリプト言語とオープンソース コードが良い例です。 [フォルダーを開く] を使用すると、Visual Studio ではソース コードを操作する新しい方法が提供されます。

[フォルダーを開く] API は `Microsoft.VisualStudio.Workspace.*` 名前空間以下にあり、[フォルダーを開く] 内のファイルに関するデータまたはアクションをエクステンダーで生成および使用するために使用できます。 拡張機能ではこれらの API を使用して、次のような多くの領域に機能を提供できます。

- [ワークスペース](workspaces.md) - [フォルダーを開く] 機能拡張の開始点は、このワークスペースとその API です。
- [ファイル コンテキストとアクション](workspace-file-contexts.md) - ファイル コンテキストを通じて提供されるファイル固有のコード インテリジェンス。
- [インデックス作成](workspace-indexing.md) - [フォルダーを開く] ワークスペースに関するデータを収集して保持します。
- [言語サービス](workspace-language-services.md) - 言語サービスを [フォルダーを開く] ワークスペースに統合します。
- [ビルド](workspace-build.md) - [フォルダーを開く] ワークスペースのビルド サポート。

次の種類を使用する機能では、[フォルダーを開く] がサポートされる新しい API を採用する必要があります。

- `IVsHierarchy`
- `IVsProject`
- `DTE`

## <a name="feedback-comments-issues"></a>フィードバック、コメント、イシュー

[フォルダーを開く] と `Microsoft.VisualStudio.Workspace.*` API は、積極的に開発中です。 予期しない動作が発生した場合は、対象のリリースの既知の問題を確認してください。 [開発者コミュニティ](https://aka.ms/feedback/suggest?space=8)は、イシューに投票し、作成する場合にお勧めの場所です。 フィードバックごとに、イシューを詳しく説明することを強くお勧めします。 開発の対象とする Visual Studio バージョン、使用している API (実装したものと対話している相手の両方)、予想される結果、および実際の結果を含めます。 可能であれば、devenv.exe プロセスのダンプを含めます。 GitHub のイシュー追跡を使用して、このドキュメントおよび関連ドキュメントに関するフィードバックを提供してください。

## <a name="next-steps"></a>次のステップ

* [ワークスペース](workspaces.md) - [フォルダーを開く] ワークスペース API について確認します。