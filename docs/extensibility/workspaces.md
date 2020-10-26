---
title: Visual Studio のワークスペース |Microsoft Docs
ms.date: 02/21/2018
ms.topic: conceptual
author: vukelich
ms.author: svukel
manager: viveis
ms.workload:
- vssdk
ms.openlocfilehash: 011781b434c4d005e473c5f97c60a9269dc5d034
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62952764"
---
# <a name="workspaces"></a>Workspaces

ワークスペースは、Visual Studio が開いている [フォルダー](../ide/develop-code-in-visual-studio-without-projects-or-solutions.md)内のファイルのコレクションをどのように表すかを示します。これは型によって表され <xref:Microsoft.VisualStudio.Workspace.IWorkspace> ます。 ワークスペースは、フォルダー内のファイルに関連するコンテンツや機能を理解していません。 代わりに、他のユーザーが操作できるデータを生成して使用するための、機能と拡張機能のための一般的な Api のセットが用意されています。 プロデューサーは、さまざまなエクスポート属性を使用して [Managed Extensibility Framework](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md) (MEF) を介して構成されます。

## <a name="workspace-providers-and-services"></a>ワークスペースプロバイダーとサービス

ワークスペースプロバイダーとサービスは、ワークスペースのコンテンツに応答するためのデータと機能を提供します。 コンテキストファイル情報、ソースファイル内のシンボル、またはビルド機能を提供する場合があります。

どちらの概念も [ファクトリパターン](https://en.wikipedia.org/wiki/Factory_method_pattern) を使用し、ワークスペースによって MEF を介してインポートされます。 すべてのエクスポート属性 `IProviderMetadataBase` はまたは `IWorkspaceServiceFactoryMetadata` を実装しますが、拡張機能がエクスポートされた型に使用する具象型があります。

プロバイダーとサービスの違いの1つは、ワークスペースとの関係です。 ワークスペースには特定の種類のプロバイダーを多数含めることができますが、特定の種類のサービスはワークスペースごとに1つだけ作成されます。 たとえば、ワークスペースには多くのファイルスキャナープロバイダーがありますが、ワークスペースにはワークスペースごとに1つのインデックスサービスしかありません。

もう1つの重要な違いは、プロバイダーとサービスからのデータの消費です。 ワークスペースは、いくつかの理由でプロバイダーからデータを取得するためのエントリポイントです。 まず、プロバイダーは、通常、作成するデータの一部を絞り込んでいます。 データは、C# ソースファイルまたは _CMakeLists.txt_ ファイルのビルドファイルコンテキストのシンボルである場合があります。 ワークスペースは、コンシューマーの要求を、メタデータが要求と一致するプロバイダーに対して照合します。 2つ目のシナリオでは、多くのプロバイダーが要求に寄与する可能性がありますが、他のシナリオでは、最も優先順位の高いプロバイダーが使用されます。

これに対して、拡張機能では、のインスタンスを取得し、ワークスペースサービスと直接やり取りできます。 の拡張メソッド `IWorkspace` は、Visual Studio によって提供されるサービス (など) で使用でき <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetFileWatcherService%2A> ます。 拡張機能は、拡張機能内のコンポーネント、または他の拡張機能を使用するために、ワークスペースサービスを提供する場合があります。 コンシューマー <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetServiceAsync%2A> は、または型で指定した拡張メソッドを使用する必要があり `IWorkspace` ます。

>[!WARNING]
> Visual Studio と競合するサービスは作成しないでください。 予期しない問題が発生する可能性があります。

## <a name="disposal-on-workspace-closure"></a>ワークスペースのクロージャでの破棄

ワークスペースのクロージャでは、エクステンダーが非同期コードを破棄する必要がある場合があります。 <xref:Microsoft.VisualStudio.Threading.IAsyncDisposable>このインターフェイスは、このコードを簡単に記述できるようにするために用意されています。

## <a name="related-types"></a>関連する型

- <xref:Microsoft.VisualStudio.Workspace.IWorkspace> 開いているフォルダーのような、開いているワークスペースの中心的なエンティティです。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspaceProviderFactory`1> インスタンス化されたワークスペースごとにプロバイダーを作成します。
- <xref:Microsoft.VisualStudio.Workspace.IWorkspaceServiceFactory> インスタンス化されたワークスペースごとにサービスを作成します。
- <xref:Microsoft.VisualStudio.Threading.IAsyncDisposable> は、破棄中に非同期コードを実行する必要があるプロバイダーおよびサービスに実装する必要があります。
- <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper> 既知のサービスまたは任意のサービスにアクセスするためのヘルパーメソッドを提供します。

## <a name="workspace-settings"></a>ワークスペースの設定

ワークスペースには、 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager> ワークスペースに対するシンプルで強力な制御機能を備えたサービスがあります。 設定の基本的な概要については、「 [ビルドおよびデバッグタスクのカスタマイズ](../ide/customize-build-and-debug-tasks-in-visual-studio.md)」を参照してください。

ほとんどの種類の設定 `SettingsType` は、 _VSWorkspaceSettings.json_や_tasks.vs.json_などの_json_ファイルです。

ワークスペースの設定の機能は、ワークスペース内の単なるパスである "スコープ" を中心にしています。 コンシューマーがを呼び出すと <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager.GetAggregatedSettings%2A> 、要求されたパスと設定の種類を含むすべてのスコープが集計されます。 スコープの集計の優先順位は次のとおりです。

1. "ローカル設定"。通常は、ワークスペースのルートの `.vs` ディレクトリです。
1. 要求されたパス自体。
1. 要求されたパスの親ディレクトリ。
1. ワークスペースルートまでのすべての親ディレクトリ。
1. "グローバル設定" は、ユーザーディレクトリにあります。

結果はのインスタンスになり <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings> ます。 このオブジェクトは、特定の型の設定を保持し、として格納されているキー名を設定するためにクエリを実行でき `string` ます。 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings.GetProperty%2A>メソッドと <xref:Microsoft.VisualStudio.Workspace.Settings.WorkspaceSettingsExtensions> 拡張メソッドは、呼び出し元が要求する設定値の型を認識することを想定しています。 ほとんどの設定ファイルは、 _json_ ファイルとして保存されますが、多くの呼び出しでは `string` 、 `bool` `int` これらの型の、、、およびの各配列が使用されます。 オブジェクトの種類もサポートされています。 そのような場合は、 `IWorkspaceSettings` それ自体を型引数として使用できます。 次に例を示します。

```json
{
  "intValue": 1,
  "stringValue": "s",
  "boolValue": true,
  "stringArray": [
    "s1",
    "s2"
  ],
  "nestedIWorkspaceSettings": {
    "nestedString": "ns"
  }
}
```

これらの設定がユーザーの _VSWorkspaceSettings.js_であると仮定すると、データには次のようにアクセスできます。

```csharp
using System.Collections.Generic;
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Settings;

private static void ReadSettings(IWorkspace workspace)
{
    IWorkspaceSettingsManager settingsManager = workspace.GetSettingsManager();
    IWorkspaceSettings settings = settingsManager.GetAggregatedSettings(SettingsTypes.Generic);

    // result == WorkspaceSettingsResult.Success
    WorkspaceSettingsResult result = settings.GetProperty("intValue", out int intValue);
    result = settings.GetProperty("stringValue", out string stringValue);
    result = settings.GetProperty("boolValue", out bool boolValue);
    result = settings.GetProperty("stringArray", out string[] stringArray);
    result = settings.GetProperty("nestedIWorkspaceSettings", out IWorkspaceSettings nestedIWorkspaceSettings);
    result = nestedIWorkspaceSettings.GetProperty("nestedString", out string nestedString);

    // Extension method alternative using default values.
    int intValueOrDefault = settings.Property("intValue", /* default */ 42);

    // Missing key. result == WorkspaceSettingsResult.Undefined
    result = settings.GetProperty("missing", out string missing);

    // Wrong type for a key. result == WorkspaceSettingsResult.Error
    result = settings.GetProperty("intValue", out IWorkspaceSettings notSettings);

    // Special ability to union "stringArray" across all scopes.
    IEnumerable<string> allStringArray = settings.UnionPropertyArray<string>("stringArray");
}
```

>[!NOTE]
>これらの設定 Api は、名前空間で使用できる Api とは無関係 `Microsoft.VisualStudio.Settings` です。 ワークスペースの設定は、ホストに依存せず、ワークスペース固有の設定ファイルまたは動的設定プロバイダーを使用します。

### <a name="providing-dynamic-settings"></a>動的設定の提供

拡張機能はを提供でき <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsProvider> ます。 これらのメモリ内プロバイダーを使用すると、拡張機能で設定を追加したり、他のものを上書きしたりできます。

のエクスポート `IWorkspaceSettingsProvider` は、他のワークスペースプロバイダーとは異なります。 ファクトリはではなく、 `IWorkspaceProviderFactory` 特別な属性の型はありません。 代わりに、を実装 <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsProviderFactory> して使用し `[Export(typeof(IWorkspaceSettingsProviderFactory))]` ます。

```csharp
// Common workspace provider factory pattern
[ExportFeatureProvider(some, args, to, export)]
internal class MyProviderFactory : IWorkspaceProviderFactory<IFeatureProvider>
{
     IFeatureProvider CreateProvider(IWorkspace workspace) => new Provider(workspace);
}

// IWorkspaceSettingsProvider pattern
[Export(typeof(IWorkspaceSettingsProviderFactory))]
internal class MySettingsProviderFactory : IWorkspaceSettingsProviderFactory
{
    // 100 is typically the value used by built-in settings providers. Lower value is higher priority.
    int Priority => 100;

    IWorkspaceSettingsProvider CreateSettingsProvider(IWorkspace workspace) => new MySettingsProvider(workspace);
}
```

>[!TIP]
>`IWorkspaceSettingsSource`(など) を返すメソッドを実装する場合 `IWorkspaceSettingsProvider.GetSingleSettings` 、ではなくのインスタンスを返し `IWorkspaceSettings` `IWorkspaceSettingsSource` ます。 `IWorkspaceSettings` 設定の集計時に役立つ詳細情報を提供します。

### <a name="settings-related-apis"></a>設定関連 Api

- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager> ワークスペースの設定を読み取り、集計します。
- <xref:Microsoft.VisualStudio.Workspace.WorkspaceServiceHelper.GetSettingsManager%2A>`IWorkspaceSettingsManager`ワークスペースのを取得します。
- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettingsManager.GetAggregatedSettings%2A> 重複するすべてのスコープで集計された特定のスコープの設定を取得します。
- <xref:Microsoft.VisualStudio.Workspace.Settings.IWorkspaceSettings> 特定のスコープの設定が含まれます。

## <a name="workspace-suggested-practices"></a>ワークスペースの推奨されるプラクティス

- `IWorkspaceProviderFactory.CreateProvider`作成時にコンテキストを記憶する api または同様の api からオブジェクトを返し `Workspace` ます。 プロバイダーインターフェイスは、このオブジェクトが作成時に保持されることを想定して書き込まれます。
- ワークスペース固有のキャッシュまたは設定を、ワークスペースの "ローカル設定" パス内に保存します。 Visual Studio 2017 バージョン15.6 以降のを使用して、ファイルのパスを作成し `Microsoft.VisualStudio.Workspace.WorkspaceHelper.MakeRootedUnderWorkingFolder` ます。 バージョン15.6 より前のバージョンの場合は、次のスニペットを使用します。

```csharp
using System.IO;
using Microsoft.VisualStudio.Workspace;
using Microsoft.VisualStudio.Workspace.Settings;

private static string MakeRootedUnderWorkingFolder(IWorkspace workspace, string relativePath)
{
    string workingFolder = workspace.GetSettingsManager().GetAggregatedSettings(SettingsTypes.WorkspaceControlSettings).Property<string>("WorkingFolder");
    return Path.Combine(workingFolder, relativePath);
}
```

## <a name="solution-events-and-package-auto-load"></a>ソリューションイベントとパッケージの自動読み込み

読み込まれたパッケージは `IVsSolutionEvents7` 、を実装して呼び出すことができ `IVsSolution.AdviseSolutionEvents` ます。 これには、Visual Studio でフォルダーを開いたり閉じたりするイベントが含まれます。

UI コンテキストを使用すると、パッケージを自動的に読み込むことができます。 値は `4646B819-1AE0-4E79-97F4-8A8176FDD664`です。

## <a name="troubleshooting"></a>トラブルシューティング

### <a name="the-sourceexplorerpackage-package-did-not-load-correctly"></a>SourceExplorerPackage パッケージが正しく読み込まれませんでした

ワークスペースの拡張性は MEF ベースであるため、構成エラーが発生すると、開いているフォルダーをホストしているパッケージの読み込みに失敗します。 たとえば、拡張機能がを使用して型をエクスポートするときに、 `ExportFileContextProviderAttribute` 型がのみを実装している場合、 `IWorkspaceProviderFactory<IFileContextActionProvider>` Visual Studio でフォルダーを開こうとするとエラーが発生します。

::: moniker range="vs-2017"

エラーの詳細については、 _%localappdata%\microsoft\visualstudio\15. 0_id \componentmodelcache\microsoft.visualstudio.default.err_を参照してください。 拡張機能によって実装された型のエラーをすべて解決します。

::: moniker-end

::: moniker range=">=vs-2019"

エラーの詳細については、 _%localappdata%\microsoft\visualstudio\16. 0_id \componentmodelcache\microsoft.visualstudio.default.err_を参照してください。 拡張機能によって実装された型のエラーをすべて解決します。

::: moniker-end

## <a name="next-steps"></a>次の手順

* [ファイル](workspace-file-contexts.md) コンテキスト-ファイルコンテキストプロバイダーは、開いているフォルダーワークスペースのコードインテリジェンスを提供します。
* [インデックス作成](workspace-indexing.md) -ワークスペースのインデックス作成は、ワークスペースに関する情報を収集して保持します。
