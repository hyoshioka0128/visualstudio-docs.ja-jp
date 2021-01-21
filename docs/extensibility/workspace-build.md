---
title: Visual Studio でのワークスペースビルド |Microsoft Docs
description: 開いているフォルダーのシナリオをサポートするために、ワークスペースのインデックス付きおよびファイルコンテキストデータを提供するエクステンダーについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: e44c2398b873bbca95c971ae1b44ac3de831b2ae
ms.sourcegitcommit: 0c9155e9b9408fb7481d79319bf08650b610e719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2021
ms.locfileid: "97877105"
---
# <a name="workspace-build"></a>ワークスペースビルド

[フォルダーを開く](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)シナリオでのビルドサポートには、実行するビルドアクションだけでなく、[ワークスペース](workspaces.md)の[インデックス付き](workspace-indexing.md)および[ファイルコンテキスト](workspace-file-contexts.md)データを提供するエクステンダーが必要です。

拡張機能に必要なものの概要を次に示します。

## <a name="build-file-context"></a>ビルドファイルコンテキスト

- プロバイダーファクトリ
  - `ExportFileContextProviderAttribute`の `supportedContextTypeGuids` すべての適用可能な定数としての属性 `string``BuildContextTypes`
  - `IWorkspaceProviderFactory<IFileContextProvider>` を実装します
  - ファイルコンテキストプロバイダー
    - `FileContext`ビルド操作ごとにを返し、サポートされる構成
      - <xref:Microsoft.VisualStudio.Workspace.Build.BuildContextTypes> からの `contextType`
      - `context` は、 <xref:Microsoft.VisualStudio.Workspace.Build.IBuildConfigurationContext> `Configuration` プロパティをビルド構成として実装し `"Debug|x86"` ます ( `"ret"` `null` 該当しない場合は、、、など)。 または、のインスタンスを使用し <xref:Microsoft.VisualStudio.Workspace.Build.BuildConfigurationContext> ます。 構成値は、インデックス付きのファイルデータ値の構成と一致して **いる必要があり** ます。

## <a name="indexed-build-file-data-value"></a>インデックス付きビルドファイルのデータ値

- プロバイダーファクトリ
  - `ExportFileScannerAttribute``IReadOnlyCollection<FileDataValue>`サポートされる型としての属性
  - `IWorkspaceProviderFactory<IFileScanner>` を実装します
- ファイルスキャナーをオンにする `ScanContentAsync<T>`
  - が型引数の場合にデータを返します `FileScannerTypeConstants.FileDataValuesType`
  - 次のように構築された各構成のファイルデータ値を返します。
    - `type` as `BuildConfigurationContext.ContextTypeGuid`
    - `context` ビルド構成 ( `"Debug|x86"` `"ret"` 該当しない場合は、、など `null` )。 この値は、ファイルコンテキストの構成と一致して **いる必要があり** ます。

## <a name="build-file-context-action"></a>ビルドファイルコンテキストアクション

- プロバイダーファクトリ
  - `ExportFileContextActionProvider`の `supportedContextTypeGuids` すべての適用可能な定数としての属性 `string``BuildContextTypes`
  - `IWorkspaceProviderFactory<IFileContextActionProvider>` を実装します
- のアクションプロバイダー `IFileContextActionProvider.GetActionsAsync`
  - `IFileContextAction`指定された値と一致するを返します。 `FileContext.ContextType`
- ファイルコンテキストアクション
  - `IFileContextAction`とを実装します。<xref:Microsoft.VisualStudio.Workspace.Extensions.VS.IVsCommandItem>
  - `CommandGroup` プロパティの戻り値 `16537f6e-cb14-44da-b087-d1387ce3bf57`
  - `CommandId``0x1000`ビルド用、 `0x1010` リビルド用、または `0x1020` クリーン用

>[!NOTE]
>は `FileDataValue` インデックスを作成する必要があるため、ワークスペースを開く間隔と、完全なビルド機能のためにファイルをスキャンするポイントの間には、一定の時間がかかります。 以前にキャッシュされたインデックスが存在しないため、フォルダーを最初に開いたときに遅延が発生します。

## <a name="reporting-messages-from-a-build"></a>ビルドからのメッセージの報告

ビルドでは、次の2つの方法のいずれかで、情報、警告、およびエラーメッセージをユーザーに通知できます。 単純な方法は、を使用 <xref:Microsoft.VisualStudio.Workspace.Build.IBuildMessageService> し、次のようにを提供することです <xref:Microsoft.VisualStudio.Workspace.Build.BuildMessage> 。

```csharp
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Build;

private static void OutputBuildMessage(IWorkspace workspace)
{
    IBuildMessageService buildMessageService = workspace.GetBuildMessageService();

    if (buildMessageService != null)
    {
      // Example error build message. See the documentation for BuildMessage for more information.
      var message = new BuildMessage()
      {
          Type = BuildMessage.TaskType.Error,
          Code = "MY1001",
          TaskText = "This is a sample error",
          ProjectFile = "buildfile.bld",
          File = "sourcefile.src"
          LogMessage = $"This is sample text that will only go to the Build output window pane.\n"

          // And any other properties to set
      };

      buildMessageService.ReportBuildMessages(new BuildMessage[] { message });
    }
}
```

`BuildMessage.Type` また、 `BuildMessage.LogMessage` ユーザーに情報が表示される場所の動作を制御します。 `BuildMessage.TaskType`以外の値を `None` 指定すると、指定した詳細を含む **エラー一覧** エントリが生成されます。 `LogMessage`は常に **出力** ツールウィンドウの [**ビルド**] ペインに出力されます。

また、拡張機能は、 **エラー一覧** または **ビルド** ペインと直接対話できます。 Visual Studio 2017 バージョン15.7 より前のバージョンに `pszProjectUniqueName` は、の引数が無視されるバグが存在し <xref:Microsoft.VisualStudio.Shell.Interop.IVsOutputWindowPane2.OutputTaskItemStringEx2*> ます。

>[!WARNING]
>の呼び出し元 `IFileContextAction.ExecuteAsync` は、引数の基になる任意の実装を提供でき `IProgress<IFileContextActionProgressUpdate>` ます。 直接呼び出すことはできません `IProgress<IFileContextActionProgressUpdate>.Report(IFileContextActionProgressUpdate)` 。 現在、この引数を使用するための一般的なガイドラインはありませんが、これらのガイドラインは変更される可能性があります。

## <a name="build-related-apis"></a>ビルド関連の Api

- <xref:Microsoft.VisualStudio.Workspace.Build.IBuildConfigurationContext> ビルド構成の詳細を提供します。
- <xref:Microsoft.VisualStudio.Workspace.Build.IBuildMessageService><xref:Microsoft.VisualStudio.Workspace.Build.BuildMessage>ユーザーに s を表示します。

## <a name="tasksvsjson-and-launchvsjson"></a>On と launch.vs.jsの tasks.vs.js

ファイルの tasks.vs.jsを作成する方法、またはファイルに launch.vs.jsする方法については、「 [ビルドタスクとデバッグタスクのカスタマイズ](../ide/customize-build-and-debug-tasks-in-visual-studio.md)」を参照してください。

## <a name="next-steps"></a>次のステップ

* [言語サーバープロトコル](language-server-protocol.md) -言語サーバーを Visual Studio に統合する方法について説明します。