---
title: '方法: 非同期パッケージを使用して VS パッケージをバックグラウンドで読み込む |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: dedf0173-197e-4258-ae5a-807eb3abc952
author: acangialosi
ms.author: anthc
ms.workload:
- vssdk
ms.openlocfilehash: 77690a1947f82f97c4aa12809a80ea61335d216d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710614"
---
# <a name="how-to-use-asyncpackage-to-load-vspackages-in-the-background"></a>方法: 非同期パッケージを使用して VS パッケージをバックグラウンドで読み込む
VS パッケージのロードと初期化は、ディスク I/O の原因となる可能性があります。 このような I/O が UI スレッドで発生すると、応答性の問題が発生する可能性があります。 これに対処するために、Visual Studio 2015<xref:Microsoft.VisualStudio.Shell.AsyncPackage>では、バックグラウンド スレッドでパッケージの読み込みを有効にするクラスが導入されました。

## <a name="create-an-asyncpackage"></a>非同期パッケージを作成する
 まず、VSIX プロジェクト (**ファイル** > **新しい** > **プロジェクト** > **Visual C#** > **機能拡張** > **VSIX プロジェクト**) を作成し、VSPackage をプロジェクトに追加します (プロジェクトを右クリックし、**新しい項目** > **C# 項目** > **を追加** > **Add** > する機能拡張 Visual Studio**パッケージ**)。 その後、サービスを作成し、それらのサービスをパッケージに追加できます。

1. からパッケージを派生<xref:Microsoft.VisualStudio.Shell.AsyncPackage>します。

2. クエリによってパッケージが読み込まれる可能性のあるサービスを提供する場合は、次の手順を実行します。

    パッケージがバックグラウンドで読み込まれるために安全であることを Visual Studio に示し、この<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>動作をオプトインするには、属性コンストラクターで **"許可BackgroundLoading/背景の読み込み"** プロパティを true に設定する必要があります。

   ```csharp
   [PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]

   ```

    バックグラウンド スレッドでサービスをインスタンス化しても安全であることを Visual Studio に示すには、コンストラクターで<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttributeBase.IsAsyncQueryable%2A>プロパティを true<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>に設定する必要があります。

   ```csharp
   [ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]

   ```

3. UI コンテキストを使用して読み込む場合は、<xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute>パッケージの自動読み込みエントリの値として書き込まれたフラグに値 (0x2) を OR に対して**PackageAutoLoadFlags.BackgroundLoad**を指定する必要があります。

   ```csharp
   [ProvideAutoLoad(UIContextGuid, PackageAutoLoadFlags.BackgroundLoad)]

   ```

4. 非同期の初期化作業を行う場合は、 を<xref:Microsoft.VisualStudio.Shell.AsyncPackage.InitializeAsync%2A>オーバーライドする必要があります。 VSIX`Initialize()`テンプレートによって提供されるメソッドを削除します。 (`Initialize()`**非同期パッケージ**のメソッドはシールされています)。 任意のメソッドを<xref:Microsoft.VisualStudio.Shell.AsyncPackage.AddService%2A>使用して、非同期サービスをパッケージに追加できます。

    注 :`base.InitializeAsync()`を呼び出すために、ソース コードを次のコードに変更できます。

   ```csharp
   await base.InitializeAsync(cancellationToken, progress);
   ```

5. 非同期初期化コード **(InitializeAsync)** から RPC (リモート プロシージャ コール) を作成しないように注意する必要があります。 これらは、直接または間接的に<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>呼び出すときに発生する可能性があります。  同期の読み込みが必要な場合、UI<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory>スレッドは を使用してブロックします。 デフォルトのブロック モデルでは、RPC が無効になります。 つまり、非同期タスクから RPC を使用しようとすると、UI スレッド自体がパッケージの読み込みを待機している場合にデッドロックが発生します。 一般的な代替手段として、**必要**<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>に応じてコードを UI スレッドにマーシャリングする方法があります。  **ThreadHelper.Generic.Invoke**を使用しないか、通常は UI スレッドに到達するのを待機している呼び出しスレッドをブロックします。

    注: メソッドで**GetService**または**クエリサービス**を`InitializeAsync`使用することは避けてください。 これらの機能を使用する必要がある場合は、まず UI スレッドに切り替える必要があります。 別の方法は、(にキャストして **)AsyncPackage**から<xref:Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider>使用<xref:Microsoft.VisualStudio.Shell.AsyncServiceProvider.GetServiceAsync%2A>することです。

   C#: 非同期パッケージを作成します。

```csharp
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]
public sealed class TestPackage : AsyncPackage
{
    protected override Task InitializeAsync(System.Threading.CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        this.AddService(typeof(SMyTestService), CreateService, true);
        return Task.FromResult<object>(null);
    }
}
```

## <a name="convert-an-existing-vspackage-to-asyncpackage"></a>既存の VS パッケージを非同期パッケージに変換する
 作業の大半は、新しい**AsyncPackage**を作成するのと同じです。 上記の手順 1 ~ 5 に従います。 また、次の推奨事項にも注意する必要があります。

1. パッケージ内の`Initialize`オーバーライドを必ず削除してください。

2. デッドロックを回避する: コード内に隠し RPC が存在する可能性があります。 これはバックグラウンドスレッドで発生します。 RPC を作成する場合 (**たとえば GetService**) は、(1) メイン スレッドに切り替えるか、(2) 存在する場合は非同期バージョンの API を使用する必要があります ( **GetServiceAsync**など ) 。

3. スレッド間の切り替え頻度が高すぎないようにしてください。 バックグラウンド スレッドで発生する可能性のある作業をローカライズして、読み込み時間を短縮します。

## <a name="querying-services-from-asyncpackage"></a>非同期パッケージからサービスを照会する
 **AsyncPackage**は、呼び出し元に応じて非同期に読み込む場合と読み込まれない場合があります。 たとえば、

- 呼び出し元が**GetService**または**クエリサービス**(両方の同期 API) を呼び出した場合、

- 呼び出し元が**IVsShell::ロードパッケージ**(または**IVsShell5::読み込みパッケージウィズコンテキスト**) を呼び出した場合、

- 読み込みは UI コンテキストによってトリガーされますが、UI コンテキスト メカニズムを指定していない場合は、非同期的に読み込むことができます

  その後、パッケージが同期的に読み込まれます。

  パッケージには、UI スレッドの処理を (非同期の初期化フェーズで) 行う機会が残っていますが、その作業の完了に対して UI スレッドはブロックされます。 呼び出し元がサービスのクエリを非同期に実行するために**IAsyncServiceProvider**を使用する場合、読み込みと初期化は、結果のタスク オブジェクトですぐにブロックされない場合に非同期的に実行されます。

  C# : サービスを非同期でクエリする方法:

```csharp
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;

IAsyncServiceProvider asyncServiceProvider = Package.GetService(typeof(SAsyncServiceProvider)) as IAsyncServiceProvider;
IMyTestService testService = await asyncServiceProvider.GetServiceAsync(typeof(SMyTestService)) as IMyTestService;
```
