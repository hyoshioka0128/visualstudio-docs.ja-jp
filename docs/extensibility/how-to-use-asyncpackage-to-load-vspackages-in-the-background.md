---
title: AsyncPackage を使用してバックグラウンドで Vspackage を読み込む
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: dedf0173-197e-4258-ae5a-807eb3abc952
author: acangialosi
ms.author: anthc
ms.workload:
- vssdk
ms.openlocfilehash: fef717ba7ec135038dcb35348eff870d9eeb3e33
ms.sourcegitcommit: 4ae5e9817ad13edd05425febb322b5be6d3c3425
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/11/2020
ms.locfileid: "90037290"
---
# <a name="how-to-use-asyncpackage-to-load-vspackages-in-the-background"></a>方法: AsyncPackage を使用してバックグラウンドで Vspackage を読み込む
VS パッケージを読み込んで初期化すると、ディスク i/o が発生する可能性があります。 このような i/o が UI スレッドで発生した場合は、応答性の問題が発生する可能性があります。 これに対処するために、Visual Studio 2015 では、バックグラウンドスレッドでのパッケージの読み込みを有効にするクラスが導入されまし  <xref:Microsoft.VisualStudio.Shell.AsyncPackage> た。

## <a name="create-an-asyncpackage"></a>AsyncPackage を作成する
 最初に、vsix プロジェクトを作成し ([**ファイル**]  >  [**新しい**  >  **プロジェクト**] [  >  **Visual C#**]、[  >  **Extensibility**  >  **VSIX プロジェクト**])、プロジェクトに VSPackage を追加します (プロジェクトを右クリックし、[新しい項目の追加] **Add**  >  **New Item**  >  **C# 項目**  >  **拡張**  >  **visual Studio パッケージ**を追加します)。 その後、サービスを作成し、それらのサービスをパッケージに追加できます。

1. からパッケージを派生させ <xref:Microsoft.VisualStudio.Shell.AsyncPackage> ます。

2. クエリによってパッケージが読み込まれる可能性があるサービスを提供する場合:

    パッケージがバックグラウンド読み込みに対して安全であることを Visual Studio に示し、この動作を選択するには、 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 属性コンストラクターで **Allowsbackgroundloading** プロパティを true に設定する必要があります。

   ```csharp
   [PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]

   ```

    バックグラウンドスレッドでサービスをインスタンス化するのが安全であることを Visual Studio に示すには、 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttributeBase.IsAsyncQueryable%2A> コンストラクターでプロパティを true に設定する必要があり <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> ます。

   ```csharp
   [ProvideService(typeof(SMyTestService), IsAsyncQueryable = true)]

   ```

3. UI コンテキストを使用して読み込む場合は、 **PackageAutoLoadFlags.BackgroundLoad** <xref:Microsoft.VisualStudio.Shell.ProvideAutoLoadAttribute> パッケージの自動読み込みエントリの値として書き込まれたフラグにまたは値 (0x2) を指定する必要があります。

   ```csharp
   [ProvideAutoLoad(UIContextGuid, PackageAutoLoadFlags.BackgroundLoad)]

   ```

4. 非同期の初期化作業がある場合は、をオーバーライドする必要があり <xref:Microsoft.VisualStudio.Shell.AsyncPackage.InitializeAsync%2A> ます。 `Initialize()`VSIX テンプレートによって提供されるメソッドを削除します。 ( `Initialize()` **Asyncpackage** のメソッドはシールされています)。 任意のメソッドを使用し <xref:Microsoft.VisualStudio.Shell.AsyncPackage.AddService%2A> て、パッケージに非同期サービスを追加できます。

    注: を呼び出すに `base.InitializeAsync()` は、ソースコードを次のように変更します。

   ```csharp
   await base.InitializeAsync(cancellationToken, progress);
   ```

5. 非同期初期化コード ( **InitializeAsync**) から Rpc (リモートプロシージャコール) を実行しないように注意する必要があります。 これらは、 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 直接または間接的にを呼び出すと発生する可能性があります。  同期読み込みが必要な場合、UI スレッドはを使用してブロックし <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> ます。 既定のブロッキングモデルは、Rpc を無効にします。 つまり、非同期タスクから RPC を使用しようとすると、UI スレッドがパッケージの読み込みを待機している場合にデッドロックが発生します。 一般的な方法としては、必要に応じてコードを UI スレッドにマーシャリングします。これは、結合可能な **タスクファクトリ** <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> や、RPC を使用しないその他のメカニズムを使用します。  **Threadhelper. Generic. Invoke**を使用しないでください。または、通常、呼び出し元のスレッドが UI スレッドへのアクセスを待機しているときにブロックします。

    注: メソッドでは **GetService** または **QueryService** を使用しないようにしてください `InitializeAsync` 。 これらを使用する必要がある場合は、最初に UI スレッドに切り替える必要があります。 代替手段は、 <xref:Microsoft.VisualStudio.Shell.AsyncServiceProvider.GetServiceAsync%2A> (にキャストすることによって) **asyncpackage** からを使用することです <xref:Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider> 。

   C#: Asyncpackage を作成します。

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

## <a name="convert-an-existing-vspackage-to-asyncpackage"></a>既存の VSPackage を AsyncPackage に変換する
 作業の大部分は、新しい **Asyncpackage**を作成することと同じです。 上記の手順 1. ~ 5. に従います。 また、次の推奨事項により、さらに注意する必要があります。

1. `Initialize`パッケージに含まれていた上書きを忘れずに削除してください。

2. デッドロックを回避する: コードに非表示の Rpc が存在する可能性があります。 これがバックグラウンドスレッドで発生するようになりました。 RPC ( **GetService**など) を作成する場合は、(1) メインスレッドに切り替えるか、(2) API の非同期バージョン (たとえば、 **GetServiceAsync**) を使用する必要があることを確認します。

3. スレッドを頻繁に切り替えることは避けてください。 バックグラウンドスレッドで発生する可能性のある作業をローカライズして、読み込み時間を短縮します。

## <a name="querying-services-from-asyncpackage"></a>AsyncPackage からサービスを照会しています
 **Asyncpackage**は、呼び出し元に応じて非同期的に読み込まれる場合とない場合があります。 たとえば、

- 呼び出し元が **GetService** または **QueryService** (両方の同期 api) を呼び出した場合、または

- 呼び出し元が **Ivsshell:: LoadPackage** (または **IVsShell5:: LoadPackageWithContext**) を呼び出した場合、または

- 読み込みは UI コンテキストによってトリガーされますが、UI コンテキスト機構は非同期に読み込むことができます。

  その後、パッケージは同期的に読み込まれます。

  UI スレッドは、その作業の完了に対して、UI スレッドがブロックされますが、(非同期の初期化フェーズで) タスクを実行するために、パッケージには引き続き機能します。 呼び出し元が **Iasyncserviceprovider** を使用してサービスに対して非同期的にクエリを実行する場合、読み込みと初期化は、結果として得られるタスクオブジェクトですぐにブロックされないという前提で非同期に行われます。

  C#: サービスを非同期で照会する方法:

```csharp
using Microsoft.VisualStudio.Shell;
using Microsoft.VisualStudio.Shell.Interop;

IAsyncServiceProvider asyncServiceProvider = Package.GetService(typeof(SAsyncServiceProvider)) as IAsyncServiceProvider;
IMyTestService testService = await asyncServiceProvider.GetServiceAsync(typeof(SMyTestService)) as IMyTestService;
```
