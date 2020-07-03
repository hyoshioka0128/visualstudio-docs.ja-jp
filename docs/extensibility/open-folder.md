---
title: Visual Studio のフォルダーの拡張機能の概要 |Microsoft Docs
ms.date: 02/21/2018
ms.topic: overview
ms.assetid: 94c3f8bf-1de3-40ea-aded-7f40c4b314c7
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: d213a7add358c46f7088f504d8c54352cda44a1c
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905979"
---
# <a name="open-folder-extensibility"></a>フォルダー拡張機能を開く

[[フォルダーを開く](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)] 機能を使用すると、ユーザーはプロジェクトファイルやソリューションファイルを使用せずに Visual Studio でコードベースを開くことができます。 [フォルダーを開く] では、Visual Studio で次のような機能を提供します。

* ソリューションエクスプローラーの統合と検索
* エディターの色づけ
* ナビゲーションに移動
* フォルダーを検索して検索

.NET や C++ 開発などのワークロードで使用する場合、ユーザーは次の情報も取得できます。

* リッチ Intellisense
* 言語固有の機能

[フォルダーを開く] を使用すると、拡張機能の作成者は任意の言語の豊富な機能を作成できます。 ユーザーのコードベース内の任意のファイルのビルド、デバッグ、およびシンボル検索をサポートする Api があります。 現在の extender では、既存の Visual Studio の機能を更新して、プロジェクトまたはソリューションをバックアップせずにコードを理解することができます。

## <a name="an-api-without-project-systems"></a>プロジェクトシステムのない API

従来、Visual Studio では、プロジェクトシステムを使用して、ソリューションとそのプロジェクト内のファイルのみを認識していました。 プロジェクトシステムは、読み込まれたプロジェクトの機能とユーザー操作を担当します。 プロジェクトに含まれるファイル、プロジェクトの内容の視覚的な表現、他のプロジェクトへの依存関係、および基になるプロジェクトファイルの変更を認識します。 これは、ユーザーに代わって他のコンポーネントが機能する、これらの階層と機能によって行われます。 すべてのコードベースがプロジェクトとソリューションの構造で適切に表されているわけではありません。 Linux 用 C++ で記述されたスクリプト言語とオープンソースコードは、良い例です。 [フォルダーを開く] を使用すると、Visual Studio では、ユーザーがソースコードと対話するための新しい方法を提供します。

Open Folder Api は名前空間の下にあり、 `Microsoft.VisualStudio.Workspace.*` 開いているフォルダー内のファイルに関連するデータまたはアクションを extender が生成して使用するために使用できます。 拡張機能では、これらの Api を使用して、次のような多くの領域に機能を提供できます。

- [ワークスペース](workspaces.md)-開いているフォルダーの機能拡張の開始点は、ワークスペースとその api です。
- ファイル[コンテキストとアクション](workspace-file-contexts.md)-ファイルコンテキストを通じて提供されるファイル固有のコードインテリジェンス。
- [インデックス作成](workspace-indexing.md)-開いているフォルダーのワークスペースに関するデータを収集して保持します。
- [言語サービス](workspace-language-services.md)-言語サービスを開いているフォルダーのワークスペースに統合します。
- [ビルド](workspace-build.md)-[フォルダーを開く] ワークスペースのビルドをサポートします。

次の種類を使用する機能では、開いているフォルダーをサポートするために新しい Api を採用する必要があります。

- `IVsHierarchy`
- `IVsProject`
- `DTE`

## <a name="feedback-comments-issues"></a>フィードバック、コメント、問題

フォルダーを開くと、 `Microsoft.VisualStudio.Workspace.*` api がアクティブな開発中になります。 予期しない動作が発生した場合は、目的のリリースに関する既知の問題を参照してください。 [開発者コミュニティ](https://developercommunity.visualstudio.com)は、投票して問題を作成するために推奨される場所です。 フィードバックごとに、問題の詳細な説明を強くお勧めします。 開発している Visual Studio のバージョン、使用している Api (実装したものと対話しているものの両方)、予想される結果、および実際の結果を含めます。 可能であれば、devenv.exe プロセスのダンプを含めます。 GitHub の問題追跡を使用して、このドキュメントおよび関連ドキュメントに関するフィードバックをお寄せください。

## <a name="next-steps"></a>次の手順

* [[ワークスペース](workspaces.md)]-[フォルダーを開く] ワークスペース API について説明します。