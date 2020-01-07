---
title: 言語サーバープロトコル拡張機能を追加する |Microsoft Docs
ms.date: 11/14/2017
ms.topic: conceptual
ms.assetid: 52f12785-1c51-4c2c-8228-c8e10316cd83
author: madskristensen
ms.author: madsk
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d328eb525767205eeedc5781bb93129d5b2eb7f7
ms.sourcegitcommit: 3e74ec49a54e5c3da7631f4466128cdf4384af6b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/01/2019
ms.locfileid: "68711246"
---
# <a name="add-a-language-server-protocol-extension"></a>言語サーバー プロトコルの拡張機能の追加

言語サーバープロトコル (LSP) は、JSON RPC v2.0 形式の共通プロトコルで、さまざまなコードエディターに言語サービス機能を提供するために使用されます。 開発者は、このプロトコルを使用して、1つの言語サーバーを作成して、その LSP をサポートするさまざまなコードエディターに IntelliSense、エラー診断、すべての参照の検索などの言語サービス機能を提供できます。 従来、Visual Studio の言語サービスは、TextMate 文法ファイルを使用して、構文の強調表示などの基本的な機能を提供したり、Visual Studio 機能拡張 Api の完全なセットを使用するカスタム言語サービスを作成したりすることによって追加できます。豊富なデータ。 Visual Studio で LSP をサポートしている場合は、3つ目のオプションがあります。

![Visual Studio の言語サーバープロトコルサービス](media/lsp-service-in-VS.png)

## <a name="language-server-protocol"></a>言語サーバー プロトコル

![言語サーバープロトコルの実装](media/lsp-implementation.png)

この記事では、LSP ベースの言語サーバーを使用する Visual Studio 拡張機能を作成する方法について説明します。 LSP ベースの言語サーバーを既に開発しており、それを Visual Studio に統合するだけであることを前提としています。

Visual Studio 内でのサポートのために、言語サーバーは、次のようにストリームベースの転送機構を使用してクライアント (Visual Studio) と通信できます。

* 標準入力/出力ストリーム
* 名前付きパイプ
* ソケット (TCP のみ)

Visual Studio での LSP とそのサポートの目的は、Visual Studio 製品に含まれていない言語サービスをオンボードすることです。 これは、Visual Studio で既存の言語サービス ( C#など) を拡張するためのものではありません。 既存の言語を拡張するには、言語サービスの拡張ガイド (たとえば["Roslyn" .NET Compiler Platform](../extensibility/dotnet-compiler-platform-roslyn-extensibility.md)) を参照するか、「[エディターと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

プロトコル自体の詳細については、[こちら](https://github.com/Microsoft/language-server-protocol)のドキュメントを参照してください。

サンプル言語サーバーを作成する方法、または既存の言語サーバーを Visual Studio Code に統合する方法の詳細については、[こちら](https://code.visualstudio.com/docs/extensions/example-language-server)のドキュメントを参照してください。

## <a name="language-server-protocol-supported-features"></a>言語サーバープロトコルでサポートされる機能

次の表は、Visual Studio でサポートされている LSP 機能を示しています。

Message | Visual Studio でのサポートがある
--- | ---
化 | 可
初期化済み | 可
シャットダウン | 可
終了 | 可
$/cancelRequest | 可
window/showMessage | 可
window/showMessageRequest | 可
window/logMessage | 可
テレメトリ/イベント |
client/registerCapability |
client/unregisterCapability |
workspace/didChangeConfiguration | 可
workspace/didChangeWatchedFiles | 可
ワークスペース/シンボル | 可
workspace/executeCommand | 可
workspace/applyEdit | 可
textDocument/publishDiagnostics | 可
textDocument/didOpen | 可
textDocument/didChange | 可
textDocument/willSave |
textDocument/willSaveWaitUntil |
textDocument/didSave | 可
textDocument/didClose | 可
textDocument/補完機能 | 可
完了/解決 | 可
textDocument/hover | 可
textDocument/signatureHelp | 可
textDocument/references | 可
textDocument/documentHighlight | 可
textDocument/documentSymbol | 可
textDocument/書式設定 | 可
textDocument/rangeFormatting | 可
textDocument/onTypeFormatting 設定 |
textDocument/definition | 可
textDocument/codeAction | 可
textDocument/codeLens |
codeLens/resolve |
textDocument/documentLink |
documentLink/resolve |
textDocument/rename | 可

## <a name="get-started"></a>作業開始

> [!NOTE]
> Visual Studio 2017 バージョン15.8 以降では、共通言語サーバープロトコルのサポートが Visual Studio に組み込まれています。 プレビュー[言語サーバークライアントの VSIX](https://marketplace.visualstudio.com/items?itemName=vsext.LanguageServerClientPreview)バージョンを使用して LSP 拡張機能をビルドした場合、バージョン15.8 以降にアップグレードすると、その拡張機能が動作しなくなります。 LSP 拡張機能を再び動作させるには、次の手順を実行する必要があります。
>
> 1. Microsoft Visual Studio Language Server Protocol Preview VSIX をアンインストールします。
>
>    バージョン15.8 以降では、Visual Studio でアップグレードを実行するたびに、プレビュー VSIX が自動的に検出され、削除されます。
>
> 2. Nuget の参照を、 [LSP パッケージ](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)のプレビュー版以外の最新バージョンに更新します。
>
> 3. VSIX マニフェストの Microsoft Visual Studio Language Server Protocol Preview VSIX への依存関係を削除します。
>
> 4. VSIX で、インストールターゲットの下限として Visual Studio 2017 バージョン 15.8 Preview 3 が指定されていることを確認します。
>
> 5. リビルドと再デプロイ。

### <a name="create-a-vsix-project"></a>VSIX プロジェクトを作成する

LSP ベースの言語サーバーを使用して言語サービス拡張機能を作成するには、まず、VS のインスタンス用に**Visual Studio 拡張機能の開発**ワークロードがインストールされていることを確認します。

次に、[**ファイル** > ] [**新しいプロジェクト** >   > ] [**ビジュアルC#** **機能拡張** > ] [**vsix プロジェクト**] の順に移動して、新しい VSIX プロジェクトを作成します。

![vsix プロジェクトの作成](media/lsp-vsix-project.png)

### <a name="language-server-and-runtime-installation"></a>言語サーバーとランタイムのインストール

既定では、Visual Studio で LSP ベースの言語サーバーをサポートするために作成される拡張機能には、言語サーバー自体や、それらを実行するために必要なランタイムは含まれていません。 拡張機能の開発者は、必要な言語サーバーとランタイムの配布を担当します。 これを行うには、いくつかの方法があります。

* 言語サーバーは、VSIX にコンテンツファイルとして埋め込むことができます。
* 言語サーバーや必要なランタイムをインストールするための MSI を作成します。
* ランタイムと言語サーバーを取得する方法をユーザーに通知する、Marketplace の手順を提供します。

### <a name="textmate-grammar-files"></a>TextMate 文法ファイル

LSP には、言語のテキストの色付け方法に関する仕様は含まれていません。 拡張機能の開発者は、Visual Studio の言語に対してカスタムの色付けを提供するために、TextMate 文法ファイルを使用できます。 カスタムの TextMate 文法またはテーマファイルを追加するには、次の手順を実行します。

1. 拡張機能内に "文法" という名前のフォルダーを作成します (または、任意の名前を選択します)。

2. *文法*フォルダー内に、カスタムの色付けを提供する、任意 *\*の tmlanguage*、  *\*plist*、  *\*tmlanguage*、または *\*json*ファイルを含めます。

   > [!TIP]
   > *Tmtheme*ファイルは、スコープが Visual Studio 分類 (名前付きの色キー) にどのようにマップされるかを定義します。 ガイダンスについては、 *% ProgramFiles (x86)% \ Microsoft Visual Studio\\\<バージョン >\\\<SKU > \Common7\IDE\CommonExtensions\Microsoft\ で、グローバルな tmtheme ファイルを参照できます。TextMate\Starterkit\Themesg*ディレクトリ。

3. *Pkgdef*ファイルを作成し、次のような行を追加します。

    ```
    [$RootKey$\TextMate\Repositories]
    "MyLang"="$PackageFolder$\Grammars"
    ```

4. ファイルを右クリックし、[**プロパティ**] を選択します。 [**ビルド**] アクションを [**コンテンツ**] に変更し、[ **VSIX に含める**] プロパティを [ **true**] に変更します。

前の手順を完了すると、' MyLang ' という名前のリポジトリソースとして*文法*フォルダーがパッケージのインストールディレクトリに追加されます (' mylang ' はあいまいさを解消するための名前であり、任意の一意の文字列にすることができます)。 このディレクトリ内のすべての文法 (*tmlanguage*ファイル) とテーマファイル (*tmlanguage*ファイル) は、チャンスとして取得され、textmate で提供される組み込みの文法を置き換えます。 文法ファイルの宣言された拡張子が、開いているファイルの拡張子と一致する場合、TextMate がステップインします。

## <a name="create-a-simple-language-client"></a>単純な言語クライアントを作成する

### <a name="main-interface---ilanguageclientdotnetapimicrosoftvisualstudiolanguageserverclientilanguageclientviewvisualstudiosdk-2017"></a>Main インターフェイス- [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)

VSIX プロジェクトを作成したら、次の NuGet パッケージをプロジェクトに追加します。

* [Microsoft.VisualStudio.LanguageServer.Client](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)

> [!NOTE]
> 前の手順を完了した後に NuGet パッケージに対する依存関係を取得すると、Newtonsoft. Json および StreamJsonRpc パッケージもプロジェクトに追加されます。 **拡張機能が対象とする Visual Studio のバージョンに新しいバージョンがインストールされることが確実である場合を除き、これらのパッケージは更新しないで**ください。 アセンブリは VSIX に含まれません。代わりに、Visual Studio のインストールディレクトリから選択されます。 ユーザーのコンピューターにインストールされているものより新しいバージョンのアセンブリを参照している場合、拡張機能は機能しません。

次に、 [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)インターフェイスを実装する新しいクラスを作成できます。これは、LSP ベースの言語サーバーに接続する言語クライアントに必要な主要なインターフェイスです。

次に例を示します。

```csharp
namespace MockLanguageExtension
{
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
        public string Name => "Bar Language Extension";

        public IEnumerable<string> ConfigurationSections => null;

        public object InitializationOptions => null;

        public IEnumerable<string> FilesToWatch => null;

        public event AsyncEventHandler<EventArgs> StartAsync;
        public event AsyncEventHandler<EventArgs> StopAsync;

        public async Task<Connection> ActivateAsync(CancellationToken token)
        {
            await Task.Yield();

            ProcessStartInfo info = new ProcessStartInfo();
            info.FileName = Path.Combine(Path.GetDirectoryName(Assembly.GetExecutingAssembly().Location), "Server", @"MockLanguageServer.exe");
            info.Arguments = "bar";
            info.RedirectStandardInput = true;
            info.RedirectStandardOutput = true;
            info.UseShellExecute = false;
            info.CreateNoWindow = true;

            Process process = new Process();
            process.StartInfo = info;

            if (process.Start())
            {
                return new Connection(process.StandardOutput.BaseStream, process.StandardInput.BaseStream);
            }

            return null;
        }

        public async Task OnLoadedAsync()
        {
            await StartAsync.InvokeAsync(this, EventArgs.Empty);
        }

        public Task OnServerInitializeFailedAsync(Exception e)
        {
            return Task.CompletedTask;
        }

        public Task OnServerInitializedAsync()
        {
            return Task.CompletedTask;
        }
    }
}
```

実装する必要のある主なメソッドは、 [Onロード async](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017)と[アクティブ非同期](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017)です。 [Onloaded async](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017)は、Visual Studio によって拡張機能が読み込まれ、言語サーバーを開始する準備ができたときに呼び出されます。 このメソッドでは、[StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017) をすぐに呼び出して、言語サーバーを開始する必要があることを通知することも、追加のロジックを実行して後で [StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017) を起動することもできます。 **言語サーバーをアクティブ化するには、ある時点で StartAsync 呼び出す必要があります。**

"[アクティブな非同期](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017)" は、[StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017) デリゲートを呼び出すことによって、最終的に呼び出されるメソッドです。 言語サーバーを起動して接続を確立するロジックが含まれています。 サーバーへの書き込みとサーバーからの読み取りのためのストリームを含む接続オブジェクトを返す必要があります。 ここでスローされた例外は、Visual Studio の情報バーメッセージを使用してキャッチされ、ユーザーに表示されます。

### <a name="activation"></a>アクティベーション

言語クライアントクラスが実装されたら、それに対して2つの属性を定義して、Visual Studio への読み込み方法とアクティブ化方法を定義する必要があります。

```csharp
  [Export(typeof(ILanguageClient))]
  [ContentType("bar")]
```

### <a name="mef"></a>MEF

Visual Studio は[MEF](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md) (Managed Extensibility Framework) を使用して、その機能拡張ポイントを管理します。 [Export](/dotnet/api/system.componentmodel.composition.exportattribute)属性は、このクラスが拡張ポイントとして取得され、適切なタイミングで読み込まれる必要があることを Visual Studio に示します。

MEF を使用するには、VSIX マニフェストで、MEF を資産として定義する必要もあります。

VSIX マニフェストデザイナーを開き、[**アセット**] タブに移動します。

![MEF アセットの追加](media/lsp-add-asset.png)

新しい資産を作成するには、[**新規**] をクリックします。

![MEF 資産の定義](media/lsp-define-asset.png)

* **種類**:Microsoft.VisualStudio.MefComponent
* **ソース**:現在のソリューション内のプロジェクト
* **プロジェクト**: [プロジェクト]

### <a name="content-type-definition"></a>コンテンツタイプの定義

現在、LSP ベースの言語サーバー拡張機能を読み込む唯一の方法は、ファイルのコンテンツタイプです。 つまり、言語クライアントクラス ( [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)を実装) を定義する場合は、ファイルの種類を定義する必要があります。このクラスを開くと、拡張機能が読み込まれます。 定義されているコンテンツの種類に一致するファイルが開かれていない場合、拡張機能は読み込まれません。

これを行うには、1つ`ContentTypeDefinition`または複数のクラスを定義します。

```csharp
namespace MockLanguageExtension
{
    public class BarContentDefinition
    {
        [Export]
        [Name("bar")]
        [BaseDefinition(CodeRemoteContentDefinition.CodeRemoteContentTypeName)]
        internal static ContentTypeDefinition BarContentTypeDefinition;

        [Export]
        [FileExtension(".bar")]
        [ContentType("bar")]
        internal static FileExtensionToContentTypeDefinition BarFileExtensionDefinition;
    }
}
```

前の例では、 *. bar*ファイル拡張子で終わるファイルに対して、コンテンツの種類の定義が作成されています。 コンテンツの種類の定義には "bar" という名前が付けられ、 [CodeRemoteContentTypeName](/dotnet/api/microsoft.visualstudio.languageserver.client.coderemotecontentdefinition.coderemotecontenttypename?view=visualstudiosdk-2017)から派生する必要があります。

コンテンツタイプの定義を追加した後、言語クライアントの拡張機能をどのような場合に言語クライアントクラスに読み込むかを定義できます。

```csharp
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
    }
```

LSP 言語サーバーのサポートを追加する場合、Visual Studio で独自のプロジェクトシステムを実装する必要はありません。 お客様は、Visual Studio で1つのファイルまたはフォルダーを開いて、言語サービスの使用を開始できます。 実際、LSP 言語サーバーのサポートは、開いているフォルダーやファイルのシナリオでのみ機能するように設計されています。 カスタムプロジェクトシステムが実装されている場合、一部の機能 (設定など) は機能しません。

## <a name="advanced-features"></a>高度な機能

### <a name="settings"></a>設定

カスタム言語サーバー固有の設定はサポートされていますが、引き続き改善されています。 設定は言語サーバーがサポートする内容に固有であり、通常は言語サーバーがデータを出力する方法を制御します。 たとえば、言語サーバーには、報告されるエラーの最大数の設定が含まれている場合があります。 拡張機能の作成者は、特定のプロジェクトのユーザーが変更できる既定値を定義します。

次の手順に従って、LSP 言語サービス拡張機能に設定のサポートを追加します。

1. 設定とその既定値を含む JSON ファイル (たとえば、 *MockLanguageExtensionSettings*) をプロジェクトに追加します。 例えば:

    ```json
    {
        "foo.maxNumberOfProblems": -1
    }
    ```

2. JSON ファイルを右クリックし、[**プロパティ**] を選択します。 **ビルド**アクションを "Content" に、"VSIX に含める" プロパティを**true**に変更します。

3. ConfigurationSections を実装し、JSON ファイルで定義されている設定のプレフィックスの一覧を返します (Visual Studio Code では、これは、パッケージの構成セクション名にマップされます)。

    ```csharp
    public IEnumerable<string> ConfigurationSections
    {
        get
        {
            yield return "foo";
        }
    }
    ```

4. Pkgdef ファイルをプロジェクトに追加し (新しいテキストファイルを追加し、ファイル拡張子を pkgdef に変更します)。 .Pkgdef ファイルには、次の情報が含まれている必要があります。

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\[settings-name]]
    @="$PackageFolder$\[settings-file-name].json"
    ```

    サンプル:

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\MockLanguageExtension]
    @="$PackageFolder$\MockLanguageExtensionSettings.json"
    ```

5. Pkgdef ファイルを右クリックし、[**プロパティ**] を選択します。 [**ビルド**アクション] を [**コンテンツ**] に、[ **VSIX に含める**] プロパティを [ **true**] に変更します。

6. *Source.extension.vsixmanifest*ファイルを開き、[**資産**] タブに資産を追加します。

   ![vspackage asset の編集](media/lsp-add-vspackage-asset.png)

   * **種類**:VisualStudio. VsPackage
   * **ソース**:ファイルシステム上のファイル
   * **パス**: [ *Pkgdef*ファイルのパス]

### <a name="user-editing-of-settings-for-a-workspace"></a>ワークスペースの設定をユーザーが編集する

1. ユーザーは、サーバーが所有しているファイルが含まれているワークスペースを開きます。
2. ユーザーは、 *vsworkspacesettings.json*という名前の*vs*フォルダーにファイルを追加します。
3. ユーザーは、サーバーが提供する設定の*vsworkspacesettings.json*ファイルに行を追加します。 例えば:

    ```json
    {
        "foo.maxNumberOfProblems": 10
    }
    ```

### <a name="enable-diagnostics-tracing"></a>診断トレースを有効にする

診断トレースを有効にすると、クライアントとサーバー間のすべてのメッセージを出力できます。これは、問題をデバッグするときに役立ちます。 診断トレースを有効にするには、次の手順を実行します。

1. ワークスペース設定ファイル*vsworkspacesettings.json*を開くか作成します (「ワークスペースの設定をユーザーが編集する」を参照してください)。
2. 設定の json ファイルに次の行を追加します。

```json
{
    "foo.trace.server": "Off"
}
```

トレースの詳細には、次の3つの値を指定できます。

* オフ: トレースは完全にオフ
* "Messages": トレースが有効になっていますが、メソッド名と応答 ID のみがトレースされています。
* "Verbose": トレースが有効になります。rpc メッセージ全体がトレースされます。

トレースが有効になっている場合、コンテンツは *%temp%\VisualStudio\LSP*ディレクトリ内のファイルに書き込まれます。 このログは、 *[LanguageClientName]-[Datetime スタンプ] .log*という名前の形式に従います。 現時点では、トレースは、開いているフォルダーのシナリオに対してのみ有効にすることができます。 1つのファイルを開いて言語サーバーをアクティブ化する場合、診断トレースはサポートされません。

### <a name="custom-messages"></a>カスタムメッセージ

標準言語サーバープロトコルに含まれていない言語サーバーとのメッセージの送受信を容易にする Api が用意されています。 カスタムメッセージを処理するには、言語クライアントクラスで[ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)インターフェイスを実装します。 [VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md)ライブラリは、言語クライアントと言語サーバーの間でカスタムメッセージを転送するために使用されます。 LSP 言語のクライアント拡張機能は他の Visual Studio 拡張機能と同じであるため、拡張機能のカスタムメッセージを使用して、(他の Visual Studio Api を使用して) Visual Studio に追加機能を追加することもできます。

#### <a name="receive-custom-messages"></a>カスタムメッセージを受信する

言語サーバーからカスタムメッセージを受信するには、 [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)に[custommessagetarget](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.custommessagetarget?view=visualstudiosdk-2017)プロパティを実装し、カスタムメッセージの処理方法を認識するオブジェクトを返します。 次に例を示します。

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public object CustomMessageTarget
    {
        get;
        set;
    }

    public class CustomTarget
    {
        public void OnCustomNotification(JToken arg)
        {
            // Provide logic on what happens OnCustomNotification is called from the language server
        }

        public string OnCustomRequest(string test)
        {
            // Provide logic on what happens OnCustomRequest is called from the language server
        }
    }
}
```

#### <a name="send-custom-messages"></a>カスタムメッセージを送信する

言語サーバーにカスタムメッセージを送信するには、 [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)に[AttachForCustomMessageAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.attachforcustommessageasync?view=visualstudiosdk-2017)メソッドを実装します。 このメソッドは、言語サーバーが開始され、メッセージを受信する準備ができたときに呼び出されます。 [Jsonrpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/src/StreamJsonRpc/JsonRpc.cs)オブジェクトはパラメーターとして渡されます。これにより、 [VS streamjsonrpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) api を使用して、メッセージを言語サーバーに送信することができます。 次に例を示します。

```csharp
internal class MockCustomLanguageClient : MockLanguageClient, ILanguageClientCustomMessage
{
    private JsonRpc customMessageRpc;

    public MockCustomLanguageClient() : base()
    {
        CustomMessageTarget = new CustomTarget();
    }

    public async Task AttachForCustomMessageAsync(JsonRpc rpc)
    {
        await Task.Yield();

        this.customMessageRpc = rpc;
    }

    public async Task SendServerCustomNotification(object arg)
    {
        await this.customMessageRpc.NotifyWithParameterObjectAsync("OnCustomNotification", arg);
    }

    public async Task<string> SendServerCustomMessage(string test)
    {
        return await this.customMessageRpc.InvokeAsync<string>("OnCustomRequest", test);
    }
}
```

### <a name="middle-layer"></a>中間層

拡張機能の開発者が、言語サーバーとの間で送受信された LSP メッセージを傍受する場合があります。 たとえば、拡張機能の開発者は、特定の LSP メッセージに送信されるメッセージパラメーターを変更したり、LSP 機能の言語サーバーから返された結果を変更したりすることができます (入力候補など)。 これが必要な場合、拡張機能の開発者は MiddleLayer API を使用して LSP メッセージをインターセプトできます。

各 LSP メッセージには、傍受のための独自の中間層インターフェイスがあります。 特定のメッセージをインターセプトするには、そのメッセージの中間層インターフェイスを実装するクラスを作成します。 次に、言語クライアントクラスに[ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)インターフェイスを実装し、 [MiddleLayer](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.middlelayer?view=visualstudiosdk-2017)プロパティにオブジェクトのインスタンスを返します。 次に例を示します。

```csharp
public class MockLanguageClient: ILanguageClient, ILanguageClientCustomMessage
{
    public object MiddleLayer => MiddleLayerProvider.Instance;

    private class MiddleLayerProvider : ILanguageClientWorkspaceSymbolProvider
    {
        internal readonly static MiddleLayerProvider Instance = new MiddleLayerProvider();

        private MiddleLayerProvider()
        {
        }

        public async Task<SymbolInformation[]> RequestWorkspaceSymbols(WorkspaceSymbolParams param, Func<WorkspaceSymbolParams, Task<SymbolInformation[]>> sendRequest)
        {
            // Send along the request as given
            SymbolInformation[] symbols = await sendRequest(param);

            // Only return symbols that are "files"
            return symbols.Where(sym => string.Equals(new Uri(sym.Location.Uri).Scheme, "file", StringComparison.OrdinalIgnoreCase)).ToArray();
        }
    }
}
```

中間層機能はまだ開発中であり、まだ包括的ではありません。

## <a name="sample-lsp-language-server-extension"></a>サンプル LSP 言語サーバー拡張機能

Visual Studio で LSP クライアント API を使用してサンプル拡張機能のソースコードを表示するには、「VSSDK-拡張性-サンプル[LSP サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/LanguageServerProtocol)」を参照してください。

## <a name="faq"></a>FAQ

**Visual Studio の豊富な機能がサポートする LSP 言語サーバーを補足するカスタム プロジェクト システムを構築したいのですが、どうしたらよいでしょうか。**

Visual Studio での LSP ベースの言語サーバーのサポートは、[フォルダーを開く機能](https://devblogs.microsoft.com/visualstudio/open-any-folder-with-visual-studio-15-preview/)に依存しており、カスタムプロジェクトシステムを必要としないように設計されています。 [ここで](https://github.com/Microsoft/VSProjectSystem)説明する手順に従って独自のカスタムプロジェクトシステムを構築できますが、設定などの一部の機能が動作しない場合があります。 LSP 言語サーバーの既定の初期化ロジックは、現在開かれているフォルダーのルートフォルダーの場所を渡すことです。したがって、カスタムプロジェクトシステムを使用する場合は、初期化時にカスタムロジックを提供して、言語サーバーが正常に起動します。

**デバッガーサポートを追加操作方法には**

[共通デバッグプロトコル](https://code.visualstudio.com/docs/extensionAPI/api-debugging)のサポートは、今後のリリースで提供される予定です。

**VS でサポートされている言語サービス (たとえば、JavaScript など) が既にインストールされている場合、LSP 言語サーバー拡張機能のインストール (lint 処理) などをインストールすることはできますか？**

はい、できますが、すべての機能が正しく動作するわけではありません。 LSP 言語サーバー拡張機能の最終的な目標は、Visual Studio でネイティブにサポートされていない言語サービスを有効にすることです。 LSP 言語サーバーを使用して追加のサポートを提供する拡張機能を作成することができますが、一部の機能 (IntelliSense) などはスムーズな体験にはなりません。一般に、LSP 言語サーバー拡張機能は、既存のものを拡張するのではなく、新しい言語のエクスペリエンスを提供するために使用することをお勧めします。

**完成した LSP 言語サーバー VSIX を発行するにはどうすればよいですか。**

Marketplace の手順については、[こちら](walkthrough-publishing-a-visual-studio-extension.md)を参照してください。

## <a name="see-also"></a>関連項目

- [他の言語の Visual Studio エディターのサポートを追加する](../ide/adding-visual-studio-editor-support-for-other-languages.md)
