---
title: '方法: 非同期サービスを提供する |Microsoft Docs'
ms.date: 11/15/2016
ms.topic: conceptual
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 0c58b0be10bf10a21b783a48d52806bf769381ee
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204099"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>方法: Visual Studio の非同期サービスを提供する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

UI スレッドをブロックせずにサービスを取得する場合は、非同期サービスを作成し、バックグラウンドスレッドでパッケージを読み込む必要があります。 このため、ではなくを使用 <xref:Microsoft.VisualStudio.Shell.AsyncPackage> <xref:Microsoft.VisualStudio.Shell.Package> して、非同期パッケージの特別な非同期メソッドを使用してサービスを追加することができます。

 同期 Visual Studio サービスの提供の詳細については、「 [方法: サービスを提供する](../extensibility/how-to-provide-a-service.md)」を参照してください。

## <a name="implementing-an-asynchronous-service"></a>非同期サービスの実装

1. VSIX プロジェクトを作成します ([ファイル]、[新規作成]、[プロジェクト]、[Visual C#]、[Extensiblity]、[**Vsix プロジェクト**])。 プロジェクトに **Testasync**という名前を指定します。

2. VSPackage をプロジェクトに追加します。 **ソリューションエクスプローラー**でプロジェクトノードを選択し、[追加]、[新しい項目]、[Visual C# 項目]、[機能拡張]、[ **visual Studio パッケージ**] の順にクリックします。 このファイルに **TestAsyncPackage.cs**という名前を指定します。

3. TestAsyncPackage.cs で、パッケージではなく AsyncPackage から継承するようにパッケージを変更します。

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. サービスを実装するには、次の3種類を作成する必要があります。

    - サービスを説明するインターフェイス。 これらのインターフェイスの多くは空です。つまり、メソッドがありません。

    - サービスインターフェイスを記述するインターフェイス。 このインターフェイスには、実装するメソッドが含まれています。

    - サービスとサービスインターフェイスの両方を実装するクラス。

5. 次の例は、3種類の基本的な実装を示しています。 サービスクラスのコンストラクターは、サービスプロバイダーを設定する必要があります。 この例では、パッケージコードファイルにサービスを追加します。

6. 次の using ステートメントをパッケージファイルに追加します。

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    ```

7. 非同期サービスの実装を次に示します。 コンストラクターでは、同期サービスプロバイダーではなく、非同期サービスプロバイダーを設定する必要があることに注意してください。

    ```
    public class TextWriterService : STextWriterService, ITextWriterService
    {
        private Microsoft.VisualStudio.Shell.IAsyncServiceProvider serviceProvider;
        public TextWriterService(Microsoft.VisualStudio.Shell.IAsyncServiceProvider provider)
        {
            serviceProvider = provider;
        }
        public async System.Threading.Tasks.Task WriteLineAsync(string path, string line)
        {
            StreamWriter writer = new StreamWriter(path);
            await writer.WriteLineAsync(line);
            writer.Close();
        }
        public TaskAwaiter GetAwaiter()
        {
            return new TaskAwaiter();
        }
    }
    public interface STextWriterService
    {
    }
    public interface ITextWriterService
    {
        System.Threading.Tasks.Task WriteLineAsync(string path, string line);
        TaskAwaiter GetAwaiter();
    }
    ```

## <a name="registering-a-service"></a>サービスの登録
 サービスを登録するには、 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> サービスを提供するパッケージにを追加します。 同期サービスの登録には、次の2つの違いがあります。

- パッケージを自動読み込みする場合は、backgroundload 値を属性に追加する必要があり <xref:Microsoft.VisualStudio.Shell.PackageAutoLoadFlags> ます。 自動読み込み Vspackage の詳細については、「 [vspackage の読み込み](../extensibility/loading-vspackages.md)」を参照してください。

- **Allowsbackgroundloading = true**フィールドをに追加する必要があり <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> ます。 PackageRegistrationAttribute の詳細については、「 [vspackage の登録と登録解除](../extensibility/registering-and-unregistering-vspackages.md)」を参照してください。

  非同期サービス登録を使用した AsyncPackage の例を次に示します。

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="adding-a-service"></a>サービスの追加

1. TestAsyncPackage.cs で、メソッドを削除 `Initialize()` し、メソッドをオーバーライドし `InitializeAsync()` ます。 サービスを追加し、コールバックメソッドを追加してサービスを作成します。 サービスを追加する非同期初期化子の例を次に示します。

    ```
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        this.AddService(typeof(STextWriterService), CreateService);

        await base.InitializeAsync(cancellationToken, progress);
    }

    ```

2. Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll への参照を追加します。

3. サービスを作成して返す非同期メソッドとしてコールバックメソッドを実装します。

    ```csharp
    public async System.Threading.Tasks.Task<object> CreateService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)
    {
        STextWriterService service = null;
        await System.Threading.Tasks.Task.Run(() => {
                    service = new TextWriterService(this);
             });

        return service;
    }

    ```

## <a name="using-a-service"></a>サービスの使用
 これで、サービスを取得し、そのメソッドを使用できるようになりました。

1. これを初期化子に示しますが、サービスを使用する任意の場所でサービスを取得することができます。

    ```csharp
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        this.AddService(typeof(STextWriterService), CreateService);

        ITextWriterService textService = await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;

        await writer.WriteLineAsync(<userpath>), "this is a test");

        await base.InitializeAsync(cancellationToken, progress);
    }

    ```

     忘れずに、 *\<userpath>* コンピューター上で意味のあるファイル名とパスに変更してください。

2. コードをビルドして実行します。 Visual Studio の実験用インスタンスが表示されたら、ソリューションを開きます。 これにより、AsyncPackage が自動生成されます。 初期化子が実行されると、指定した場所にファイルがあることを確認する必要があります。

## <a name="using-an-asynchronous-service-in-a-command-handler"></a>コマンドハンドラーでの非同期サービスの使用
 メニューコマンドで非同期サービスを使用する方法の例を次に示します。 次に示す手順を使用すると、他の非同期メソッドでサービスを使用できます。

1. プロジェクトにメニューコマンドを追加します。 ( **ソリューションエクスプローラー**で、プロジェクトノードを選択して右クリックし、[追加]、[新しい項目]、[拡張機能]、[ **カスタムコマンド**] の順に選択します)。コマンドファイルに TestAsyncCommand.cs という名前を指定 **します。**

2. カスタムコマンドテンプレートは、 `Initialize()` コマンドを初期化するために、TestAsyncPackage.cs ファイルにメソッドを再度追加します。 Initialize () メソッドで、コマンドを初期化する行をコピーします。 次のようになります。

    ```
    TestAsyncCommand.Initialize(this);
    ```

     この行を `InitializeAsync()` AsyncPackageForService.cs ファイル内のメソッドに移動します。 これは非同期初期化であるため、を使用してコマンドを初期化する前に、メインスレッドに切り替える必要があり <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> ます。 その結果、次のようになります。

    ```csharp

    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync();
        TestAsyncCommand.Initialize(this);

        this.AddService(typeof(STextWriterService), CreateService);

        ITextWriterService textService =
           await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;

        await writer.WriteLineAsync((<userpath>, "this is a test");

        await base.InitializeAsync(cancellationToken, progress);
    }

    ```

3. メソッドを削除 `Initialize()` します。

4. TestAsyncCommand.cs ファイルで、メソッドを見つけ `MenuItemCallback()` ます。 メソッドの本体を削除します。

5. using ステートメントを追加します。

    ```
    using System.IO;
    ```

6. という名前の非同期メソッドを追加します。このメソッドは `GetAsyncService()` 、サービスを取得し、そのメソッドを使用します。

    ```csharp
    private async System.Threading.Tasks.Task GetAsyncService()
    {
        ITextWriterService textService =
           this.ServiceProvider.GetService(typeof(STextWriterService))
              as ITextWriterService;
        // don’t forget to change <userpath> to a local path
        await writer.WriteLineAsync((<userpath>),"this is a test");
       }

    ```

7. メソッドからこのメソッドを呼び出し `MenuItemCallback()` ます。

    ```
    private void MenuItemCallback(object sender, EventArgs e)
    {
        GetAsyncService();
    }

    ```

8. ソリューションをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されたら、[ **ツール** ] メニューの [ **Testasynccommand の呼び出し** ] メニュー項目を探します。 これをクリックすると、TextWriterService は指定したファイルに書き込みます。 (コマンドを呼び出すとパッケージも読み込まれるため、ソリューションを開く必要はありません)。

## <a name="see-also"></a>参照
 [サービスの使用と提供](../extensibility/using-and-providing-services.md)
