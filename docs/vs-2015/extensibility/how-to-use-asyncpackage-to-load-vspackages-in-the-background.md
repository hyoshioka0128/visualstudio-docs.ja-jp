---
title: '方法: AsyncPackage を使用してバックグラウンドで Vspackage を読み込む |Microsoft Docs'
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: dedf0173-197e-4258-ae5a-807eb3abc952
caps.latest.revision: 9
ms.author: gregvanl
ms.openlocfilehash: f59838913ed3f9bc6679336393f6db9181291e3d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204029"
---
# <a name="how-to-use-asyncpackage-to-load-vspackages-in-the-background"></a>方法: AsyncPackage を使用してバックグラウンドで VSPackage を読み込む
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VS パッケージを読み込んで初期化すると、ディスク i/o が発生する可能性があります。 このような i/o が UI スレッドで発生した場合は、応答性の問題が発生する可能性があります。 これに対処するために、Visual Studio 2015 では、バックグラウンドスレッドでのパッケージの読み込みを有効にするクラスが導入されまし  <xref:Microsoft.VisualStudio.Shell.AsyncPackage> た。  
  
## <a name="creating-an-asyncpackage"></a>AsyncPackage の作成  
 まず、VSIX プロジェクト ([ファイル]、[新規]、[プロジェクト]、[Visual C#]、[機能拡張]、[**VSIX プロジェクト**]) を作成し、プロジェクトに VSPackage を追加します (プロジェクトを右クリックし、[追加]、[新しい項目]、[C# 項目]、[拡張機能]、[ **Visual Studio パッケージ**])。 その後、サービスを作成し、それらのサービスをパッケージに追加できます。  
  
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
  
4. 非同期の初期化作業がある場合は、をオーバーライドする必要があり <xref:Microsoft.VisualStudio.Shell.AsyncPackage.InitializeAsync%2A> ます。 VSIX テンプレートによって提供される **Initialize ()** メソッドを削除します。 ( **Asyncpackage**の**Initialize ()** メソッドはシールされています)。 任意のメソッドを使用し <xref:Microsoft.VisualStudio.Shell.AsyncPackage.AddService%2A> て、パッケージに非同期サービスを追加できます。  
  
    注: **base.InitializeAsync ()** を呼び出すには、ソースコードを次のように変更します。  
  
   ```csharp  
   await base.InitializeAsync(cancellationToken, progress);  
   ```  
  
5. 非同期初期化コード ( **InitializeAsync**) から Rpc (プロシージャ呼び出しの削除) を実行しないように注意する必要があります。 これらは、 <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> 直接または間接的にを呼び出すと発生する可能性があります。  同期読み込みが必要な場合、UI スレッドはを使用してブロックし <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory> ます。 既定のブロッキングモデルは、Rpc を無効にします。 つまり、非同期タスクから RPC を使用しようとすると、UI スレッドがパッケージの読み込みを待機している場合にデッドロックが発生します。 一般的な方法としては、必要に応じてコードを UI スレッドにマーシャリングします。これは、結合可能な **タスクファクトリ** <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> や、RPC を使用しないその他のメカニズムを使用します。  **Threadhelper. Generic. Invoke**を使用しないでください。または、通常、呼び出し元のスレッドが UI スレッドへのアクセスを待機しているときにブロックします。  
  
    注: **InitializeAsync**メソッドでは**GetService**または**QueryService**を使用しないようにしてください。 これらを使用する必要がある場合は、最初に UI スレッドに切り替える必要があります。 代替手段は、 <xref:Microsoft.VisualStudio.Shell.AsyncServiceProvider.GetServiceAsync%2A> (にキャストすることによって) **asyncpackage** からを使用することです <xref:Microsoft.VisualStudio.Shell.Interop.IAsyncServiceProvider> 。  
  
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
 作業の大部分は、新しい **Asyncpackage**を作成することと同じです。 上記の手順 1 ~ 5 に従う必要があります。 さらに、次の点に注意する必要があります。  
  
1. パッケージに含まれていた **初期化** オーバーライドを削除することを忘れないでください。  
  
2. デッドロックを回避する: バックグラウンドスレッドで発生するように、コード内に非表示の Rpc が存在する可能性があります。 RPC (例: **GetService**) を作成する場合は、(1) メインスレッドに切り替えるか、(2) API の非同期バージョン (たとえば、 **GetServiceAsync**) を使用する必要があることを確認する必要があります。  
  
3. スレッドを頻繁に切り替えることは避けてください。 バックグラウンドスレッドで発生する可能性のある作業をローカライズしてみてください。 これにより、読み込み時間が短縮されます。  
  
## <a name="querying-services-from-asyncpackage"></a>AsyncPackage からサービスを照会しています  
 **Asyncpackage**は、呼び出し元に応じて非同期的に読み込まれる場合とない場合があります。 たとえば、  
  
- 呼び出し元が **GetService** または **QueryService** (両方の同期 api) を呼び出した場合、または  
  
- 呼び出し元が **Ivsshell:: LoadPackage** (または **IVsShell5:: LoadPackageWithContext**) を呼び出した場合、または  
  
- 読み込みは UI コンテキストによってトリガーされますが、UI コンテキスト機構は非同期に読み込むことができます。  
  
  その後、パッケージは同期的に読み込まれます。  
  
  UI スレッドは、その作業の完了に対して UI スレッドがブロックされるのに、UI スレッドからの処理を実行するために (非同期の初期化フェーズで)、パッケージにはまだ含まれていることに注意してください。 呼び出し元が **Iasyncserviceprovider** を使用してサービスに対して非同期的にクエリを実行する場合、読み込みと初期化は、結果として得られるタスクオブジェクトですぐにブロックされないという前提で非同期に行われます。  
  
  C#: サービスを非同期で照会する方法:  
  
```csharp  
using Microsoft.VisualStudio.Shell;   
using Microsoft.VisualStudio.Shell.Interop;   
  
IAsyncServiceProvider asyncServiceProvider = Package.GetService(typeof(SAsyncServiceProvider)) as IAsyncServiceProvider;   
IMyTestService testService = await ayncServiceProvider.GetServiceAsync(typeof(SMyTestService)) as IMyTestService;  
```
