---
title: Visual Studio のワークスペースファイルのコンテキスト |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 36f986db6f2c7b483b46060e1f514acc8dd9e758
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62952816"
---
# <a name="workspace-file-contexts"></a>ワークスペースファイルのコンテキスト

開いている [フォルダー](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md) のワークスペースへのすべての洞察は、インターフェイスを実装する "ファイルコンテキストプロバイダー" によって生成され <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider> ます。 これらの拡張機能では、ファイルコンテキストを定義するために必要な洞察を蓄積するために、フォルダーまたはファイル内のパターンの検索、MSBuild ファイルとメイクファイルの読み取り、パッケージの依存関係の検出などを行うことができます。 ファイルコンテキスト自体はアクションを実行しませんが、別の拡張機能が実行できるデータを提供します。

各には <xref:Microsoft.VisualStudio.Workspace.FileContext> 、 `Guid` それに含まれるデータの型を識別するが関連付けられています。 ワークスペースはこれ `Guid` を後で使用して、プロパティを通じてデータを使用する拡張機能と照合し <xref:Microsoft.VisualStudio.Workspace.FileContext.Context> ます。 ファイルコンテキストプロバイダーは、データを生成する可能性があるファイルコンテキストを識別するメタデータと共にエクスポートされ `Guid` ます。

定義されたファイルコンテキストは、ワークスペース内の任意の数のファイルまたはフォルダーに関連付けることができます。 指定されたファイルまたはフォルダーは、任意の数のファイルコンテキストに関連付けることができます。 これは多対多リレーションシップです。

ファイルコンテキストの最も一般的なシナリオは、ビルド、デバッグ、および言語サービスに関連しています。 詳細については、これらのシナリオに関連するその他のトピックを参照してください。

## <a name="file-context-lifecycle"></a>ファイルコンテキストのライフサイクル

のライフサイクル `FileContext` は非決定的です。 コンポーネントは、任意の時点で、何らかの種類のコンテキストに対して非同期に要求できます。 要求コンテキスト型の一部のサブセットをサポートするプロバイダーに対しては、クエリが実行されます。 インスタンスは、メソッドを使用して `IWorkspace` コンシューマーとプロバイダーの間の中間者として機能し <xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> ます。 コンシューマーはコンテキストを要求し、コンテキストに基づいて短期的なアクションを実行できますが、他のユーザーはコンテキストを要求し、有効期間の長い参照を維持することができます。

ファイルのコンテキストが古くなる原因となるファイルが変更される可能性があります。 プロバイダーは、でイベントを発生させて、 `FileContext` コンシューマーに更新プログラムを通知することができます。 たとえば、一部のファイルに対してビルドコンテキストが提供されていても、ディスク上の変更によってそのコンテキストが無効になった場合、元のプロデューサーはイベントを呼び出すことができます。 それを参照しているコンシューマーは `FileContext` 、新しいを再クエリでき `FileContext` ます。

>[!NOTE]
>コンシューマーにプッシュモデルはありません。 コンシューマーは、要求後にプロバイダーの新しい通知を受け取ることはありません `FileContext` 。

## <a name="expensive-file-context-computations"></a>高コストなファイルコンテキストの計算

ファイルの内容をディスクから読み取ると、特にプロバイダーがファイル間のリレーションシップを解決する必要がある場合に、コストが高くなる可能性があります。 たとえば、ソースファイルのファイルコンテキストに対してプロバイダーに対してクエリを行うことはできますが、ファイルコンテキストはプロジェクトファイルのメタデータに依存します。 プロジェクトファイルを解析したり、MSBuild で評価したりすると、コストが高くなります。 代わりに、拡張機能はをエクスポートして、 `IFileScanner` `FileDataValue` ワークスペースのインデックス作成中にデータを作成することができます。 ファイルコンテキストを要求されると、は `IFileContextProvider` そのインデックス付きデータのクエリを迅速に実行できるようになります。 インデックス作成の詳細については、「 [ワークスペースのインデックス作成](workspace-indexing.md) 」を参照してください。

>[!WARNING]
>他に `FileContext` も、計算に負荷がかかる可能性がある点に注意してください。 一部の UI 操作は同期的であり、大量の要求に依存してい `FileContext` ます。 たとえば、[エディター] タブを開いて **ソリューションエクスプローラー** ショートカットメニューを開くことができます。 これらのアクションは、多くのビルドコンテキスト型要求を行います。

## <a name="file-context-related-apis"></a>ファイルコンテキスト関連の Api

- <xref:Microsoft.VisualStudio.Workspace.FileContext> データとメタデータを保持します。
- <xref:Microsoft.VisualStudio.Workspace.IFileContextProvider><xref:Microsoft.VisualStudio.Workspace.IFileContextProvider`1>ファイルコンテキストを作成します。
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextProviderAttribute> ファイルコンテキストプロバイダーをエクスポートします。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspace.GetFileContextsAsync%2A> は、コンシューマーがファイルコンテキストを取得するために使用されます。
- <xref:Microsoft.VisualStudio.Workspace.Build.BuildContextTypes> 開いているフォルダーが使用するビルドコンテキストの種類を定義します。

## <a name="file-context-actions"></a>ファイルコンテキストアクション

`FileContext`自体はいくつかのファイルに関するデータにすぎませんが、は <xref:Microsoft.VisualStudio.Workspace.IFileContextAction> そのデータを表現して操作する方法です。 `IFileContextAction` は柔軟に使用できます。 最も一般的な2つのケースは、ビルドとデバッグです。

## <a name="reporting-progress"></a>進行状況を報告する

<xref:Microsoft.VisualStudio.Workspace.IFileContextActionBase.ExecuteAsync%2A>メソッドは渡され `IProgress<IFileContextActionProgressUpdate>` ますが、引数をその型として使用することはできません。 `IFileContextActionProgressUpdate` は空のインターフェイスであり、を呼び出すと `IProgress<IFileContextActionProgressUpdate>.Report(IFileContextActionProgressUpdate)` スローされる可能性があり `NotImplementedException` ます。 代わりに、では、 `IFileContextAction` シナリオに応じて、引数を別の型にキャストする必要があります。

Visual Studio によって提供される型の詳細については、各シナリオのドキュメントを参照してください。

## <a name="file-context-action-related-apis"></a>ファイルコンテキストアクション関連 Api

- <xref:Microsoft.VisualStudio.Workspace.IFileContextAction> に基づいていくつかの動作を実行 `FileContext` します。
- <xref:Microsoft.VisualStudio.Workspace.IFileContextActionProvider> のインスタンスを作成 `IFileContextAction` します。
- <xref:Microsoft.VisualStudio.Workspace.ExportFileContextActionProviderAttribute> 型をエクスポート `IWorkspaceProviderFactory<IFileContextActionProvider>` します。

## <a name="file-watching"></a>ファイルの監視

ワークスペースは、ファイルの変更通知をリッスンし、via を提供し <xref:Microsoft.VisualStudio.Workspace.IFileWatcherService> <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetFileWatcherService%2A> ます。 "ExcludedItems" 設定に一致するファイルは、ファイル通知イベントを生成しません。 イベント間のしきい値は、通知の簡略化と重複除去に使用されます。 ファイルの変更に対処する必要がある場合は、このサービスをサブスクライブする必要があります。

>[!TIP]
>ワークスペースの [インデックスサービス](workspace-indexing.md) は、既定でファイルイベントをサブスクライブします。 ファイルの追加と変更により、関連 `IFileScanner` するイベントがそのファイルの新しいデータに対して呼び出されます。 ファイルの削除によってインデックス付きデータが削除されます。 ファイル監視サービスに対してをサブスクライブする必要はありません `IFileScanner` 。

## <a name="next-steps"></a>次の手順

* [インデックス作成](workspace-indexing.md) -ワークスペースのインデックス作成は、ワークスペースに関する情報を収集して保持します。
* [ワークスペース-ワーク](workspaces.md) スペースの概念と設定のストレージを確認します。
