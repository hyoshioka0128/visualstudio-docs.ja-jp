---
title: '方法: 非同期の Visual Studio サービスを提供する |Microsoft Docs'
description: 非同期の Visual Studio サービスを提供する方法について説明します。 この方法では、UI スレッドをブロックせずにサービスを取得できます。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: 0448274c-d3d2-4e12-9d11-8aca78a1f3f5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f9973bb86296442f4b936ddb54ff645d74d7ab74
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105074939"
---
# <a name="how-to-provide-an-asynchronous-visual-studio-service"></a>方法: 非同期の Visual Studio サービスを提供する
UI スレッドをブロックせずにサービスを取得する場合は、非同期サービスを作成し、バックグラウンドスレッドでパッケージを読み込む必要があります。 このため、ではなくを使用 <xref:Microsoft.VisualStudio.Shell.AsyncPackage> <xref:Microsoft.VisualStudio.Shell.Package> して、非同期パッケージの特別な非同期メソッドを使用してサービスを追加できます。

 同期 Visual Studio サービスの提供の詳細については、「 [方法: サービスを提供する](../extensibility/how-to-provide-a-service.md)」を参照してください。

## <a name="implement-an-asynchronous-service"></a>非同期サービスを実装する

1. Vsix プロジェクトを作成します ([**ファイル**] [新規] [プロジェクト] [  >    >    >  **Visual C#**  >  **Extensiblity**] [  >  **vsix プロジェクト**])。 プロジェクトに **Testasync** という名前を指定します。

2. VSPackage をプロジェクトに追加します。 **ソリューションエクスプローラー** でプロジェクトノードを選択し、[**追加**] [  >  **新しい項目**] [  >  **visual C# 項目**] [拡張] [  >    >  **visual Studio パッケージ**] の順にクリックします。 このファイルに「 *Testasyncpackage .cs*」という名前を指定します。

3. *Testasyncpackage .cs* で、次のようにで `AsyncPackage` はなくから継承するようにパッケージを変更します。 `Package`

    ```csharp
    public sealed class TestAsyncPackage : AsyncPackage
    ```

4. サービスを実装するには、次の3種類を作成する必要があります。

    - サービスを識別するインターフェイス。 これらのインターフェイスの多くは空です。つまり、サービスにクエリを実行するためだけに使用されるメソッドはありません。

    - サービスインターフェイスを記述するインターフェイス。 このインターフェイスには、実装するメソッドが含まれています。

    - サービスとサービスインターフェイスの両方を実装するクラス。

5. 次の例は、3種類の基本的な実装を示しています。 サービスクラスのコンストラクターは、サービスプロバイダーを設定する必要があります。 この例では、パッケージコードファイルにサービスを追加します。

6. パッケージファイルに次の using ディレクティブを追加します。

    ```csharp
    using System.Threading;
    using System.Threading.Tasks;
    using System.Runtime.CompilerServices;
    using System.IO;
    using Microsoft.VisualStudio.Threading;
    using IAsyncServiceProvider = Microsoft.VisualStudio.Shell.IAsyncServiceProvider;
    using Task = System.Threading.Tasks.Task;
    ```

7. 非同期サービスの実装を次に示します。 コンストラクターでは、同期サービスプロバイダーではなく、非同期サービスプロバイダーを設定する必要があることに注意してください。

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

## <a name="register-a-service"></a>サービスを登録する
 サービスを登録するには、 <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> サービスを提供するパッケージにを追加します。 同期サービスの登録とは異なり、パッケージとサービスの両方で非同期読み込みがサポートされていることを確認する必要があります。

- PackageRegistrationAttribute の詳細については、 **Allowsbackgroundloading = true** フィールドをに追加して、パッケージを非同期に初期化できるようにする必要があります。詳細については、 <xref:Microsoft.VisualStudio.Shell.PackageRegistrationAttribute> 「 [vspackage の登録と登録解除](../extensibility/registering-and-unregistering-vspackages.md)」を参照してください。

- サービスインスタンスを非同期に初期化できるようにするには、 **Isasyncqueryable = true** フィールドをに追加する必要があり <xref:Microsoft.VisualStudio.Shell.ProvideServiceAttribute> ます。

  `AsyncPackage`非同期サービス登録を使用したの例を次に示します。

```csharp
[ProvideService((typeof(STextWriterService)), IsAsyncQueryable = true)]
[ProvideAutoLoad(UIContextGuids80.SolutionExists, PackageAutoLoadFlags.BackgroundLoad)]
[PackageRegistration(UseManagedResourcesOnly = true, AllowsBackgroundLoading = true)]
[Guid(TestAsyncPackage.PackageGuidString)]
public sealed class TestAsyncPackage : AsyncPackage
{. . . }
```

## <a name="add-a-service"></a>サービスの追加

1. *Testasyncpackage .cs* で、メソッドを削除 `Initialize()` し、メソッドをオーバーライドし `InitializeAsync()` ます。 サービスを追加し、コールバックメソッドを追加してサービスを作成します。 サービスを追加する非同期初期化子の例を次に示します。

    ```csharp
    protected override async Task InitializeAsync(CancellationToken cancellationToken, IProgress<ServiceProgressData> progress)
    {
        await base.InitializeAsync(cancellationToken, progress);
        this.AddService(typeof(STextWriterService), CreateTextWriterService);
    }

    ```
    このサービスがこのパッケージの外部で表示されるようにするには、最後のパラメーターとして、promote フラグの値を *true* に設定します。  `this.AddService(typeof(STextWriterService), CreateTextWriterService, true);`

2. *Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll* への参照を追加します。

3. サービスを作成して返す非同期メソッドとしてコールバックメソッドを実装します。

    ```csharp
    public async Task<object> CreateTextWriterService(IAsyncServiceContainer container, CancellationToken cancellationToken, Type serviceType)
    {
        TextWriterService service = new TextWriterService(this);
        await service.InitializeAsync(cancellationToken);
        return service;
    }

    ```

## <a name="use-a-service"></a>サービスを使用する
 これで、サービスを取得し、そのメソッドを使用できるようになりました。

1. これを初期化子に示しますが、サービスを使用する任意の場所でサービスを取得することができます。

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

     忘れずに、 `userpath` コンピューター上で意味のあるファイル名とパスに変更してください。

2. コードをビルドして実行します。 Visual Studio の実験用インスタンスが表示されたら、ソリューションを開きます。 これにより、が自動生成さ `AsyncPackage` れます。 初期化子が実行されると、指定した場所にファイルがあることを確認する必要があります。

## <a name="use-an-asynchronous-service-in-a-command-handler"></a>コマンドハンドラーでの非同期サービスの使用
 メニューコマンドで非同期サービスを使用する方法の例を次に示します。 次に示す手順を使用すると、他の非同期メソッドでサービスを使用できます。

1. プロジェクトにメニューコマンドを追加します。 (**ソリューションエクスプローラー** で、プロジェクトノードを選択して右クリックし、[**追加**  >  ] を選択します。**新しい項目**  > **拡張性**  > **カスタムコマンド**。)コマンドファイルに *Testasynccommand .cs* という名前を指定します。

2. カスタムコマンドテンプレートは、 `Initialize()` コマンドを初期化するために、メソッドを *Testasyncpackage .cs* ファイルに再追加します。 メソッドで、 `Initialize()` コマンドを初期化する行をコピーします。 次のようになります。

    ```csharp
    TestAsyncCommand.Initialize(this);
    ```

     この行を `InitializeAsync()` *Asyncpackageforservice .cs* ファイルのメソッドに移動します。 これは非同期初期化であるため、を使用してコマンドを初期化する前に、メインスレッドに切り替える必要があり <xref:Microsoft.VisualStudio.Threading.JoinableTaskFactory.SwitchToMainThreadAsync%2A> ます。 その結果、次のようになります。

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

3. メソッドを削除 `Initialize()` します。

4. *Testasynccommand .cs* ファイルで、メソッドを見つけ `MenuItemCallback()` ます。 メソッドの本体を削除します。

5. Using ディレクティブを追加します。

    ```csharp
    using System.IO;
    ```

6. という名前の非同期メソッドを追加します。このメソッドは `UseTextWriterAsync()` 、サービスを取得し、そのメソッドを使用します。

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

7. メソッドからこのメソッドを呼び出し `MenuItemCallback()` ます。

    ```csharp
    private void MenuItemCallback(object sender, EventArgs e)
    {
        UseTextWriterAsync();
    }

    ```

8. ソリューションをビルドし、デバッグを開始します。 Visual Studio の実験用インスタンスが表示されたら、[ **ツール** ] メニューの [ **Testasynccommand の呼び出し** ] メニュー項目を探します。 これをクリックすると、TextWriterService は指定したファイルに書き込みます。 (コマンドを呼び出すとパッケージも読み込まれるため、ソリューションを開く必要はありません)。

## <a name="see-also"></a>こちらもご覧ください
- [サービスを使用して提供する](../extensibility/using-and-providing-services.md)
