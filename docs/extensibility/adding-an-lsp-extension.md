---
title: 言語サーバー プロトコル拡張機能を追加する |マイクロソフトドキュメント
ms.date: 11/14/2017
ms.topic: conceptual
ms.assetid: 52f12785-1c51-4c2c-8228-c8e10316cd83
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ef2093915538f09f425fc961420c4a3078043c91
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80740236"
---
# <a name="add-a-language-server-protocol-extension"></a>言語サーバー プロトコルの拡張機能の追加

言語サーバー プロトコル (LSP) は、さまざまなコード エディターに言語サービス機能を提供するために使用される、JSON RPC v2.0 の形式で一般的なプロトコルです。 このプロトコルを使用すると、開発者は単一言語サーバーを作成して、IntelliSense、エラー診断、すべての参照の検索などの言語サービス機能を LSP をサポートするさまざまなコード エディターに提供できます。 従来、Visual Studio の言語サービスは、TextMate 文法ファイルを使用して構文の強調表示などの基本的な機能を提供したり、豊富なデータを提供するために Visual Studio の機能拡張 API の完全なセットを使用するカスタム言語サービスを作成することで追加できます。 LSP の Visual Studio のサポートでは、3 つ目のオプションがあります。

![言語サーバー プロトコル サービスの Visual Studio](media/lsp-service-in-VS.png)

## <a name="language-server-protocol"></a>言語サーバー プロトコル

![言語サーバー プロトコルの実装](media/lsp-implementation.png)

この資料では、LSP ベースの言語サーバーを使用する Visual Studio 拡張機能を作成する方法について説明します。 LSP ベースの言語サーバーを既に開発しており、それを Visual Studio に統合する必要があることを前提としています。

Visual Studio でのサポートの場合、言語サーバーは、ストリーム ベースの転送メカニズムを使用してクライアント (Visual Studio) と通信できます。

* 標準入出力ストリーム
* 名前付きパイプ
* ソケット (TCP のみ)

LSP の目的と Visual Studio でのサポートは、Visual Studio 製品の一部ではない言語サービスをオンボードすることです。 Visual Studio の既存の言語サービス (C# など) を拡張することを目的としたものではありません。 既存の言語を拡張するには、言語サービスの機能拡張ガイド[("Roslyn" .NET コンパイラ プラットフォーム](../extensibility/dotnet-compiler-platform-roslyn-extensibility.md)など) を参照するか、「[エディターサービスと言語サービスの拡張](../extensibility/extending-the-editor-and-language-services.md)」を参照してください。

プロトコル自体の詳細については、こちらのドキュメントを参照[してください](https://github.com/Microsoft/language-server-protocol)。

サンプル言語サーバーを作成する方法、または既存の言語サーバーを Visual Studio Code に統合する方法の詳細については、[こちら](https://code.visualstudio.com/docs/extensions/example-language-server)のドキュメントを参照してください。

## <a name="language-server-protocol-supported-features"></a>言語サーバー プロトコルでサポートされる機能

次の表は、Visual Studio でサポートされている LSP 機能を示しています。

Message | Visual Studio でサポートを受けています
--- | ---
initialize | 可
初期化済み | 可
shutdown | 可
exit | 可
$/キャンセルリクエスト | 可
ウィンドウ/ショーメッセージ | 可
ウィンドウ/ショーメッセージリクエスト | 可
ウィンドウ/ログメッセージ | 可
テレメトリ/イベント |
クライアント/登録機能 |
クライアント/登録解除機能 |
ワークスペース/変更構成 | 可
ワークスペース/ファイルを変更 | 可
ワークスペース/シンボル | 可
ワークスペース/実行コマンド | 可
ワークスペース/適用編集 | 可
テキストドキュメント/公開診断 | 可
テキストドキュメント/データを開く | 可
テキストドキュメント/ディディチェンジ | 可
テキストドキュメント/ウィル保存 |
テキストドキュメント/ウィルセーブウェイトまで |
テキストドキュメント/保存 | 可
テキストドキュメント/終了閉じる | 可
テキスト ドキュメント/コンプリート | 可
完了/解決 | 可
テキストドキュメント/ホバー | 可
テキストドキュメント/署名ヘルプ | 可
テキストドキュメント/リファレンス | 可
テキストドキュメント/ドキュメントハイライト | 可
テキストドキュメント/ドキュメントシンボル | 可
テキストドキュメント/書式設定 | 可
テキスト文書/範囲書式 | 可
テキストドキュメント/オンタイプフォーマット |
テキストドキュメント/定義 | 可
テキストドキュメント/コードアクション | 可
ドキュメント/コードレンズ |
コードレンズ/解決 |
テキストドキュメント/ドキュメントリンク |
ドキュメントリンク/解決 |
テキスト ドキュメント/名前の変更 | 可

## <a name="get-started"></a>はじめに

> [!NOTE]
> Visual Studio 2017 バージョン 15.8 以降、共通言語サーバー プロトコルのサポートは、Visual Studio に組み込まれています。 プレビュー[言語サーバー クライアント VSIX](https://marketplace.visualstudio.com/items?itemName=vsext.LanguageServerClientPreview)バージョンを使用して LSP 拡張機能をビルドした場合、バージョン 15.8 以降にアップグレードすると、その拡張機能は動作を停止します。 LSP 拡張機能を再び機能させるためには、次の操作を行う必要があります。
>
> 1. をアンインストールします。
>
>    バージョン 15.8 以降、Visual Studio でアップグレードを実行するたびに、プレビュー VSIX が自動的に検出され、削除されます。
>
> 2. Nuget の参照を[、LSP パッケージ](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)の最新の非プレビュー バージョンに更新します。
>
> 3. VSIX マニフェストで、Visual Studio 言語サーバー プロトコル プレビュー VSIX への依存関係を削除します。
>
> 4. VSIX が Visual Studio 2017 バージョン 15.8 プレビュー 3 をインストール ターゲットの下限として指定していることを確認します。
>
> 5. リビルドして再デプロイします。

### <a name="create-a-vsix-project"></a>VSIX プロジェクトを作成する

LSP ベースの言語サーバーを使用して言語サービス拡張機能を作成するには、まず、VS のインスタンスに**Visual Studio 拡張機能開発**ワークロードがインストールされていることを確認します。

次に、**ファイル** > の新しいプロジェクト > **の Visual C#** > **機能** > 拡張 VSIX プロジェクトに移動して **、新しい****VSIX プロジェクトを**作成します。

![vsix プロジェクトを作成する](media/lsp-vsix-project.png)

### <a name="language-server-and-runtime-installation"></a>言語サーバーおよびランタイムのインストール

既定では、Visual Studio で LSP ベースの言語サーバーをサポートするために作成された拡張機能には、言語サーバー自体や、その実行に必要なランタイムは含まれていません。 拡張機能の開発者は、必要な言語サーバーとランタイムを配布する責任があります。 これを行うには、いくつかの方法があります。

* 言語サーバーは、コンテンツ ファイルとして VSIX に埋め込むことができます。
* 言語サーバーや必要なランタイムをインストールするための MSI を作成します。
* ランタイムおよび言語サーバーの入手方法をユーザーに知らせる Marketplace の指示を提供します。

### <a name="textmate-grammar-files"></a>テキストメイト文法ファイル

LSP には、言語にテキストの色付けを提供する方法に関する仕様は含まれていません。 Visual Studio で言語にカスタム色付けを提供するために、拡張機能の開発者は TextMate 文法ファイルを使用できます。 カスタム TextMate 文法またはテーマ ファイルを追加するには、次の手順を実行します。

1. 拡張子内に 「Grammars」 という名前のフォルダーを作成します (または、任意の名前を選択することもできます)。

2. *[文法*] フォルダーには、カスタムの色付けを行う*\*.tmlanguage* * \*、.plist* * \*、.tmtheme*、または*\*.json*のいずれかのファイルを含めます。

   > [!TIP]
   > *tmtheme*ファイルは、スコープを Visual Studio 分類 (名前付きカラー キー) にマップする方法を定義します。 ガイダンスについては *、%ProgramFiles(x86)%\Microsoft\\\<Visual Studio バージョン>\\ \<SKU>\Common7\IDE\CommonExtensions\マイクロソフト\TextMate\スターターキット\テーマ*ディレクトリのグローバル *.tmtheme*ファイルを参照できます。

3. *pkgdef*ファイルを作成し、次のような行を追加します。

    ```
    [$RootKey$\TextMate\Repositories]
    "MyLang"="$PackageFolder$\Grammars"
    ```

4. ファイルを右クリックし、[**プロパティ ]** を選択します。 **[ビルド**] アクションを **[コンテンツ]** に変更し **、[VSIX に含める**] プロパティを **[true]** に変更します。

前の手順を完了すると、パッケージのインストール ディレクトリに、'MyLang' という名前のリポジトリ ソースとして*Grammars*フォルダが追加されます ('MyLang' はあいまいさ解消の名前であり、任意の文字列を指定できます)。 このディレクトリ内のすべての文法 *(.tmlanguage*ファイル) とテーマ ファイル *(.tmtheme*ファイル) はポテンシャルとして取り上げられ、TextMate に付属する組み込みの文法に取って代わるものです。 文法ファイルの宣言された拡張子が開かれているファイルの拡張子と一致する場合、TextMate はステップインします。

## <a name="create-a-simple-language-client"></a>単純な言語クライアントを作成する

### <a name="main-interface---ilanguageclient"></a>メインインターフェイス - [ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)

VSIX プロジェクトを作成したら、次の NuGet パッケージをプロジェクトに追加します。

* [クライアント](https://www.nuget.org/packages/Microsoft.VisualStudio.LanguageServer.Client)

> [!NOTE]
> 前の手順を完了した後に NuGet パッケージに依存関係を取る場合は、Newtonsoft.Json パッケージと StreamJsonRpc パッケージもプロジェクトに追加されます。 **これらのパッケージは、拡張機能が対象とするバージョンの Visual Studio にインストールされることを確信していない限り、更新しないでください**。 アセンブリは VSIX に含まれません。代わりに、Visual Studio のインストール ディレクトリから取得されます。 ユーザーのコンピューターにインストールされているバージョンよりも新しいバージョンのアセンブリを参照している場合、拡張機能は機能しません。

次に、LSP ベースの言語サーバーに接続する言語クライアントに必要なメイン インターフェイスである[ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)インターフェイスを実装する新しいクラスを作成できます。

サンプルを次に示します。

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

実装する必要がある主なメソッドは[、OnLoadedAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017)と[ActivateAsync です](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017)。 [OnLoadedAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.onloadedasync?view=visualstudiosdk-2017)は、Visual Studio が拡張機能を読み込み、言語サーバーを起動する準備ができたときに呼び出されます。 このメソッドでは[、StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017)デリゲートをすぐに呼び出して、言語サーバーを起動する必要があることを知らせるか、追加のロジックを実行して後で[StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017)を呼び出すことができます。 **言語サーバーをアクティブにするには、ある時点で StartAsync を呼び出す必要があります。**

[アクティブ化メソッド](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.activateasync?view=visualstudiosdk-2017)は、最終的に[StartAsync](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient.startasync?view=visualstudiosdk-2017)デリゲートを呼び出すことによって呼び出されるメソッドです。 言語サーバーを起動し、そのサーバーへの接続を確立するためのロジックが含まれています。 サーバーへの書き込みとサーバーからの読み取り用のストリームを含む接続オブジェクトを返す必要があります。 ここでスローされた例外は、Visual Studio の情報バー メッセージを介してキャッチされ、ユーザーに表示されます。

### <a name="activation"></a>アクティブ化

言語クライアント クラスを実装したら、Visual Studio に読み込んでアクティブ化する方法を定義するために、2 つの属性を定義する必要があります。

```csharp
  [Export(typeof(ILanguageClient))]
  [ContentType("bar")]
```

### <a name="mef"></a>MEF

Visual Studio では、その機能拡張ポイントを管理するために[MEF](https://github.com/Microsoft/vs-mef/blob/master/doc/index.md) (マネージ機能拡張フレームワーク) を使用します。 [エクスポート](/dotnet/api/system.componentmodel.composition.exportattribute)属性は、このクラスが拡張ポイントとして選択され、適切なタイミングで読み込まれる必要があることを Visual Studio に示します。

MEF を使用するには、VSIX マニフェストで MEF をアセットとして定義する必要があります。

VSIX マニフェスト デザイナーを開き、[**資産**] タブに移動します。

![MEF アセットの追加](media/lsp-add-asset.png)

[**新規**] をクリックして、新しいアセットを作成します。

![MEF 資産の定義](media/lsp-define-asset.png)

* **タイプ**:
* **ソース**: 現在のソリューション内のプロジェクト
* **プロジェクト**: [プロジェクト]

### <a name="content-type-definition"></a>コンテンツ タイプの定義

現在、LSP ベースの言語サーバー拡張機能を読み込む唯一の方法は、ファイルのコンテンツタイプです。 つまり[、(ILanguageClient](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclient?view=visualstudiosdk-2017)を実装する)言語クライアントクラスを定義する際に、開いたときに拡張機能が読み込まれるファイルの種類を定義する必要があります。 定義したコンテンツ タイプに一致するファイルが開かれていない場合、拡張機能は読み込まれません。

これは、1 つ以上`ContentTypeDefinition`のクラスを定義することによって行われます。

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

前の例では *、.bar*ファイル拡張子で終わるファイルに対してコンテンツ タイプ定義が作成されます。 コンテンツ タイプ定義には "bar" という名前が付けられており、[から](/dotnet/api/microsoft.visualstudio.languageserver.client.coderemotecontentdefinition.coderemotecontenttypename?view=visualstudiosdk-2017)派生する必要があります。

コンテンツ タイプ定義を追加した後、言語クライアント クラスで言語クライアント拡張機能を読み込むタイミングを定義できます。

```csharp
    [ContentType("bar")]
    [Export(typeof(ILanguageClient))]
    public class BarLanguageClient : ILanguageClient
    {
    }
```

LSP 言語サーバーのサポートを追加する必要はありません、Visual Studio で独自のプロジェクト システムを実装する必要はありません。 お客様は、言語サービスの使用を開始するために、Visual Studio で 1 つのファイルまたはフォルダーを開くことができます。 実際、LSP 言語サーバーのサポートは、オープン フォルダ/ファイルのシナリオでのみ機能するように設計されています。 カスタム プロジェクト システムが実装されている場合、一部の機能 (設定など) は機能しません。

## <a name="advanced-features"></a>高度な機能

### <a name="settings"></a>設定

カスタム言語サーバー固有の設定のサポートは利用可能ですが、まだ改善中です。 設定は、言語サーバーがサポートする内容に固有のものであり、通常は言語サーバーがデータを出力する方法を制御します。 たとえば、言語サーバーには、報告されるエラーの最大数の設定が含まれる場合があります。 拡張機能の作成者は既定値を定義し、ユーザーは特定のプロジェクトに対して変更できます。

LSP 言語サービス拡張機能に設定のサポートを追加するには、次の手順に従います。

1. 設定とその既定値を含む JSON ファイル (*たとえば、MockLanguageExtensionSettings.json)* をプロジェクトに追加します。 次に例を示します。

    ```json
    {
        "foo.maxNumberOfProblems": -1
    }
    ```

2. JSON ファイルを右クリックし、[**プロパティ ]** を選択します。 **ビルド**アクションを "コンテンツ" に変更し、"VSIX に含める" プロパティを**true**に変更します。

3. 構成セクションを実装し、JSON ファイルで定義されている設定のプレフィックスの一覧を返します (Visual Studio Code では、これは package.json の構成セクション名にマップされます)。

    ```csharp
    public IEnumerable<string> ConfigurationSections
    {
        get
        {
            yield return "foo";
        }
    }
    ```

4. プロジェクトに .pkgdef ファイルを追加します (新しいテキスト ファイルを追加し、ファイル拡張子を .pkgdef に変更します)。 pkgdef ファイルには、次の情報が含まれている必要があります。

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\[settings-name]]
    @="$PackageFolder$\[settings-file-name].json"
    ```

    サンプル:

    ```
    [$RootKey$\OpenFolder\Settings\VSWorkspaceSettings\MockLanguageExtension]
    @="$PackageFolder$\MockLanguageExtensionSettings.json"
    ```

5. pkgdef ファイルを右クリックし、[**プロパティ ]** をクリックします。 **[ビルド**アクション] を **[コンテンツ]** に **、[VSIX に含める**] プロパティを**true**に変更します。

6. *source.extension.vsixmanifest*ファイルを開き、[アセット] タブで**アセット**を追加します。

   ![vspackage アセットの編集](media/lsp-add-vspackage-asset.png)

   * **タイプ**:
   * **ソース**: ファイル・システム上のファイル
   * **パス**: *[.pkgdef*ファイルへのパス]

### <a name="user-editing-of-settings-for-a-workspace"></a>ワークスペースの設定のユーザー編集

1. ユーザーは、サーバーが所有するファイルを含むワークスペースを開きます。
2. ユーザーは *、VSWorkspaceSettings.json*という名前の *.vs*フォルダーにファイルを追加します。
3. ユーザーは、サーバーが提供する設定の行を*VSWorkspaceSettings.json*ファイルに追加します。 次に例を示します。

    ```json
    {
        "foo.maxNumberOfProblems": 10
    }
    ```

### <a name="enable-diagnostics-tracing"></a>診断トレースを有効にする

診断トレースを有効にして、クライアントとサーバーの間のすべてのメッセージを出力できます。 診断トレースを有効にするには、次の手順を実行します。

1. ワークスペース設定ファイル*VSWorkspaceSettings.json*を開くか作成します (「ワークスペースの設定のユーザー編集」を参照)。
2. 設定 json ファイルに次の行を追加します。

```json
{
    "foo.trace.server": "Off"
}
```

トレースの詳細には、次の 3 つの値が考えられます。

* "オフ": トレースが完全にオフに
* "メッセージ": トレースはオンになっていますが、メソッド名と応答 ID のみがトレースされます。
* "詳細": トレースがオンになっています。rpc メッセージ全体がトレースされます。

トレースがオンの場合、コンテンツは *%temp%\VisualStudio\LSP*ディレクトリ内のファイルに書き込まれます。 ログは名前付け形式 *[言語クライアント名]-[日付時刻スタンプ].log に従います*。 現在、トレースは開いているフォルダーのシナリオに対してのみ有効にできます。 言語サーバーをアクティブ化するために単一のファイルを開く場合、診断トレースはサポートされません。

### <a name="custom-messages"></a>カスタム メッセージ

標準言語サーバー プロトコルに含まれていない言語サーバーとの間でメッセージを送受信するための API が用意されています。 カスタム メッセージを処理するには、言語クライアント クラスで[ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)インターフェイスを実装します。 [VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md)ライブラリは、言語クライアントと言語サーバー間でカスタム メッセージを送信するために使用されます。 LSP 言語クライアント拡張機能は他の Visual Studio 拡張機能と同様であるため、カスタム メッセージを使用して拡張機能に (LSP でサポートされていない) 追加機能を Visual Studio に追加できます (他の Visual Studio API を使用)。

#### <a name="receive-custom-messages"></a>カスタム メッセージを受信する

言語サーバーからカスタム メッセージを受信するには[、ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.custommessagetarget?view=visualstudiosdk-2017) [ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)のプロパティを実装し、カスタム メッセージを処理する方法を知っているオブジェクトを返します。 以下の例:

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

#### <a name="send-custom-messages"></a>カスタム メッセージを送信する

カスタム メッセージを言語サーバーに送信するには、[メソッド](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)[を実装](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.attachforcustommessageasync?view=visualstudiosdk-2017)します。 このメソッドは、言語サーバーが起動し、メッセージを受信する準備ができたときに呼び出されます。 [JsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/src/StreamJsonRpc/JsonRpc.cs)オブジェクトはパラメーターとして渡され[、VS-StreamJsonRpc](https://github.com/Microsoft/vs-streamjsonrpc/blob/master/doc/index.md) API を使用して言語サーバーにメッセージを送信できます。 以下の例:

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

拡張機能の開発者が、言語サーバーとの間で送受信される LSP メッセージを傍受する必要がある場合があります。 たとえば、拡張機能の開発者は、特定の LSP メッセージに対して送信されるメッセージ パラメータを変更したり、LSP 機能の言語サーバーから返される結果 (完了など) を変更したりできます。 この必要がある場合、拡張機能の開発者は、MiddleLayer API を使用して LSP メッセージをインターセプトできます。

各 LSP メッセージには、インターセプト用の独自の中間層インターフェイスがあります。 特定のメッセージをインターセプトするには、そのメッセージの中間層インターフェイスを実装するクラスを作成します。 次に、言語クライアント クラスで[ILanguageClientCustomMessage](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage?view=visualstudiosdk-2017)インターフェイスを実装し、[中層](/dotnet/api/microsoft.visualstudio.languageserver.client.ilanguageclientcustommessage.middlelayer?view=visualstudiosdk-2017)プロパティでオブジェクトのインスタンスを返します。 以下の例:

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

中間層の機能はまだ開発中であり、まだ包括的ではありません。

## <a name="sample-lsp-language-server-extension"></a>LSP 言語サーバー拡張のサンプル

Visual Studio で LSP クライアント API を使用してサンプル拡張機能のソース コードを参照してくださいVSSDK-拡張性-サンプル[LSP サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples/tree/master/LanguageServerProtocol)。

## <a name="faq"></a>よく寄せられる質問

**カスタム プロジェクト システムを構築して、LSP 言語サーバーを補完して Visual Studio での機能のサポートを充実させたいのです。**

Visual Studio での LSP ベースの言語サーバーのサポートは[、フォルダーを開く機能](https://devblogs.microsoft.com/visualstudio/open-any-folder-with-visual-studio-15-preview/)に依存し、カスタム プロジェクト システムを必要としないように設計されています。 独自のカスタム プロジェクト システムは[、ここで](https://github.com/Microsoft/VSProjectSystem)説明する手順に従ってビルドできますが、設定などの一部の機能が機能しない場合があります。 LSP 言語サーバーの既定の初期化ロジックでは、現在開かれているフォルダーのルート フォルダーの場所を渡すため、カスタム プロジェクト システムを使用する場合は、言語サーバーが正常に起動できるように、初期化時にカスタム ロジックを指定する必要があります。

**デバッガーのサポートを追加する方法**

今後のリリースで[、共通のデバッグ プロトコル](https://code.visualstudio.com/docs/extensionAPI/api-debugging)のサポートを提供する予定です。

**VS サポートされている言語サービス (たとえば、JavaScript) がインストールされている場合、追加機能 (linting など) を提供する LSP 言語の拡張機能をインストールすることはできますか?**

はい、しかし、すべての機能が正常に動作するわけではありません。 LSP 言語サーバー拡張機能の最終的な目標は、Visual Studio でネイティブにサポートされていない言語サービスを有効にすることです。 LSP 言語サーバーを使用して追加のサポートを提供する拡張機能を作成できますが、一部の機能 (IntelliSense など) はスムーズなエクスペリエンスではありません。 一般に、LSP 言語のサーバー拡張は、既存の言語を拡張せず、新しい言語エクスペリエンスを提供するために使用することをお勧めします。

**完成した LSP 言語サーバー VSIX を発行する場所**

マーケットプレイスの手順は[こちらをご覧ください](walkthrough-publishing-a-visual-studio-extension.md)。

## <a name="see-also"></a>関連項目

- [Visual Studio エディターの他の言語のサポートの追加](../ide/adding-visual-studio-editor-support-for-other-languages.md)
