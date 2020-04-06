---
title: '方法 : 非同期の Visual Studio サービスを提供する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 65362e465beec5465903083beca069104a48166b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710764"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>方法: 非同期の Visual Studio サービスを提供する
UI スレッドをブロックせずにサービスを取得する場合は、非同期サービスを作成し、パッケージをバックグラウンド スレッドに読み込む必要があります。 このため、ではなく<xref:Microsoft.VisualStudio.Shell.AsyncPackage><xref:Microsoft.VisualStudio.Shell.Package>を使用し、非同期パッケージの特殊な非同期メソッドを使用してサービスを追加できます。

 同期 Visual Studio サービスの提供については、「[方法 : サービスを提供する](../extensibility/how-to-provide-a-service.md)」を参照してください。

## <a name="implement-an-asynchronous-service"></a>非同期サービスの実装

1. VSIX プロジェクトを作成する (**ファイル** > **新しい** > **プロジェクト** > **Visual C#** > **拡張** > **VSIX プロジェクト**)。 プロジェクトに**TestAsync という名前を付けます**。

2. VSPackage をプロジェクトに追加します。 **ソリューション エクスプローラー**でプロジェクト ノードを選択し、[**新しい項目** > の**追加** > **] Visual C# アイテム** > **機能拡張** > **Visual Studio パッケージ**] をクリックします。 このファイルに名前*TestAsyncPackage.cs*付けます。

3. TestAsyncPackage.cs *TestAsyncPackage.cs*で、パッケージを`Package`から`AsyncPackage`継承するのではなくに変更します。

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. サービスを実装するには、次の 3 つのタイプを作成する必要があります。

    - サービスを識別するインターフェイス。 これらのインターフェイスの多くは空であり、サービスのクエリにのみ使用されるため、メソッドはありません。

    - サービス インターフェイスを記述するインターフェイス。 このインターフェイスには、実装するメソッドが含まれています。

    - サービスとサービス インターフェイスの両方を実装するクラス。

5. 次の例は、3 つの型の非常に基本的な実装を示しています。 サービス クラスのコンストラクターは、サービス プロバイダーを設定する必要があります。 この例では、サービスをパッケージ コード ファイルに追加します。

6. 次の using ディレクティブをパッケージ ファイルに追加します。

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    using Microsoft.VisualStudio.Threading;
    using IAsyncServiceProvider = Microsoft.VisualStudio.Shell.IAsyncServiceProvider;
    using Task = System.Threading.Tasks.Task;
    ```

7. 非同期サービスの実装を次に示します。 コンストラクタで同期サービスプロバイダではなく、非同期サービスプロバイダを設定する必要があります。

    ```csharp
    public class TextWriterService : STextWriterService, ITextWriterService
    {
        private IAsyncServiceProvider asyncServiceProvider;

        public TextWriterService(IAsyncServiceProvider provider)
        {
            // constructor should only be used for simple initialization
            // any usage of Visual Studio service, expensive background operations should happen in the
            // asynchronous InitializeAsync method for best performance
            asyncServiceProvider = provider;
        }

        public async Task InitializeAsync(CancellationToken cancellationToken)
        {
            await TaskScheduler.Default;
            // do background operations that involve IO or other async methods

            await ThreadHelper.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);
            // query Visual Studio services on main thread unless they are documented as free threaded explicitly.
            // The reason for this is the final cast to service interface (such as IVsShell) may involve COM operations to add/release references.

            IVsShell vsShell = this.asyncServiceProvider.GetServiceAsync(typeof(SVsShell)) as IVsShell;
            // use Visual Studio services to continue initialization
        }

        public async Task WriteLineAsync(string path, string line)
        {
            StreamWriter writer = new StreamWriter(path);
            await writer.WriteLineAsync(line);
            writer.Close();
        }
    }

    public interface STextWriterService
    {
    }

    public interface ITextWriterService
    {
        System.Threading.Tasks.Task WriteLineAsync(string path, string line);
    }
    ```

## <a name="register-a-service"></a>サービスの登録
 サービスを登録するには、サービスを<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>提供するパッケージに を追加します。 同期サービスの登録とは異なり、パッケージとサービスの両方が非同期読み込みをサポートしていることを確認する必要があります。

- パッケージを非同期的<xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute>に初期化できるようにするために **、"プロパティの読み込みと**登録解除" の詳細については、「 VSPackages の[登録と登録解除](../extensibility/registering-and-unregistering-vspackages.md)」を参照してください。

- サービス インスタンスを非同期的に初期化できるようにするには、<xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute>**に IsAsyncQueryable = true**フィールドを追加する必要があります。

  非同期サービス登録を使用する`AsyncPackage`例を次に示します。

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="add-a-service"></a>サービスの追加

1. *TestAsyncPackage.cs*でメソッドを`Initialize()`削除し、メソッド`InitializeAsync()`をオーバーライドします。 サービスを追加し、コールバック メソッドを追加してサービスを作成します。 サービスを追加する非同期初期化子の例を次に示します。

    ```csharp
    protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);
    }

    ```
    このパッケージの外部でこのサービスを表示するには、最後のパラメーターとして昇格フラグの値を*true*に設定します。`this.AddService(typeof(STextWriterService), CreateTextWriterService, true);`

2. *への参照*を追加します。

3. サービスを作成して返す非同期メソッドとしてコールバック メソッドを実装します。

    ```csharp
    public async Task<object> CreateTextWriterService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)
    {
        TextWriterService service = new TextWriterService(this);
        await service.InitializeAsync(cancellationToken);
        return service;
    }

    ```

## <a name="use-a-service"></a>サービスを使用する
 これで、サービスを取得して、そのメソッドを使用できます。

1. 初期化子ではこれを示しますが、サービスを使用する任意の場所でサービスを取得できます。

    ```csharp
    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);

        ITextWriterService textService = await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;
        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");
    }

    ```

     マシン上で意味のあるファイル`userpath`名とパスに変更することを忘れないでください!

2. コードをビルドして実行します。 Visual Studio の実験用インスタンスが表示されたら、ソリューションを開きます。 これにより、自動`AsyncPackage`ロードが行ないます。 初期化子が実行されると、指定した場所にファイルが見つかるはずです。

## <a name="use-an-asynchronous-service-in-a-command-handler"></a>コマンド ハンドラーで非同期サービスを使用する
 メニュー コマンドで非同期サービスを使用する方法の例を次に示します。 ここで示す手順を使用して、他の非同期以外のメソッドでサービスを使用できます。

1. プロジェクトにメニュー コマンドを追加します。 (ソリューション**エクスプローラー**で、プロジェクト ノードを選択し、右クリックして [**新しい項目** > **の機能** > 拡張**カスタム コマンド**の**追加** > ] を選択します)。コマンド ファイルに名前*をTestAsyncCommand.cs。*

2. カスタム コマンド テンプレートは、コマンド`Initialize()`を初期化するために*メソッドをTestAsyncPackage.cs*ファイルに再追加します。 メソッドで`Initialize()`、コマンドを初期化する行をコピーします。 次のようになります。

    ```csharp
    TestAsyncCommand.Initialize(this);
    ```

     この行を*AsyncPackageForService.cs* `InitializeAsync()`ファイル内のメソッドに移動します。 これは非同期の初期化であるため、コマンドを初期化する前にメイン スレッドに切り替える必要<xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A>があります。 その結果、次のようになります。

    ```csharp

    protected override async System.Threading.Tasks.Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);

        ITextWriterService textService =
           await this.GetServiceAsync(typeof(STextWriterService)) as ITextWriterService;
        
        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");

        await this.JoinableTaskFactory.SwitchToMainThreadAsync(cancellationToken);
        TestAsyncCommand.Initialize(this);
    }

    ```

3. メソッドを`Initialize()`削除します。

4. *TestAsyncCommand.cs*ファイルで、メソッドを`MenuItemCallback()`見つけます。 メソッドの本体を削除します。

5. using ディレクティブを追加します。

    ```csharp
    using System.IO;
    ```

6. サービスを取得し、`UseTextWriterAsync()`そのメソッドを使用する、 という名前の非同期メソッドを追加します。

    ```csharp
    private async System.Threading.Tasks.Task UseTextWriterAsync()
    {
        // Query text writer service asynchronously to avoid a blocking call.
        ITextWriterService textService =
           await AsyncServiceProvider.GlobalProvider.GetServiceAsync(typeof(STextWriterService))
              as ITextWriterService;

        string userpath = @"C:\MyDir\MyFile.txt";
        await textService.WriteLineAsync(userpath, "this is a test");
       }

    ```

7. メソッドからこのメソッドを`MenuItemCallback()`呼び出します。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        UseTextWriterAsync();
    }

    ```

8. ソリューションをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されたら、[**ツール]** メニューに移動し **、[TestAsyncCommand の呼び出し**] メニュー項目を探します。 クリックすると、指定したファイルに TextWriter サービスが書き込まれます。 (コマンドを呼び出すとパッケージも読み込まれるため、ソリューションを開く必要はありません)。

## <a name="see-also"></a>関連項目
- [サービスの使用と提供](../extensibility/using-and-providing-services.md)
