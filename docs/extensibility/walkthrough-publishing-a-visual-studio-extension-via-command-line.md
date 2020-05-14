---
title: コマンド ラインを使用して拡張機能を公開する
ms.date: 07/12/2018
ms.topic: conceptual
helpviewer_keywords:
- publishing extensions
- extension, publishing
ms.assetid: 6ff9efc4-919d-4071-a80d-6dbdd2ceb2f8
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 40be0252218f39b4ff98b58caedd7f9f20ce6d5d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697124"
---
# <a name="walkthrough-publishing-a-visual-studio-extension-via-command-line"></a>チュートリアル: コマンド ラインを使用して Visual Studio 拡張機能を発行します。

このチュートリアルでは、コマンド ラインを使用して Visual Studio 拡張機能を Visual Studio マーケットプレースに発行する方法を示します。 Marketplace に拡張機能を追加すると、開発者は[**[拡張機能と更新プログラム**](../ide/finding-and-using-visual-studio-extensions.md)] ダイアログを使用して、新しい拡張機能と更新された拡張機能を参照できます。

VsixPublisher.exe は、マーケットプレースに Visual Studio 拡張機能を発行するためのコマンド ライン ツールです。 それは${VSInstallDir}\VSSDK\ビジュアルスタジオインテグレーション\ツール\ビン\VsixPublisher.exeからアクセスできます。 このツールで使用できるコマンドは、**発行**、**パブリシャの作成**、**パブリシャの削除**、**削除、拡張機能の削除**、**ログイン**、**ログアウト**です。

## <a name="commands"></a>コマンド

### <a name="publish"></a>[発行]

拡張機能をマーケットプレースに発行します。 拡張子は、vsix、exe/msi ファイル、またはリンクです。 同じバージョンの拡張機能が既に存在する場合は、拡張機能が上書きされます。 拡張機能が存在しない場合は、新しい拡張機能が作成されます。

|コマンド オプション |説明 |
|---------|---------|
|ペイロード (必須) | 公開するペイロードへのパスまたは「詳細 URL」として使用するリンク。 |
|マニフェストを発行する (必須) | 使用する発行マニフェスト ファイルへのパス。 |
|無視警告 | 拡張機能を公開するときに無視する警告の一覧。 これらの警告は、拡張機能を公開するときにコマンド ライン メッセージとして表示されます。 (たとえば、"VSIXValidatorWarning01、VSIXValidatorWarning02")
|パーソナルアクセストークン | 発行元の認証に使用される個人用アクセス トークン (PAT)。 指定しない場合、PAT はログインユーザから取得されます。 |

```
VsixPublisher.exe publish -payload "{path to vsix}" -publishManifest "{path to vs-publish.json}" -ignoreWarnings "VSIXValidatorWarning01,VSIXValidatorWarning02"
```

### <a name="createpublisher"></a>パブリッシャーを作成する

マーケットプレースでパブリッシャーを作成します。 また、将来のアクション (たとえば、拡張機能の削除/公開) のために、発行者をマシンに記録します。

|コマンド オプション |説明 |
|---------|---------|
|表示名 (必須) | 発行者の表示名。 |
|出版社名 (必須) | 発行者の名前 (識別子など)。 |
|パーソナルアクセストークン (必須) | 発行元の認証に使用される個人用アクセス トークン。 |
|shortDescription | 発行元の簡単な説明 (ファイルではありません)。 |
|長い説明 | パブリッシャの長い説明 (ファイルではありません)。 |

```
VsixPublisher.exe createPublisher -publisherName "{Publisher Name}" -displayName "{Publisher Display Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deletepublisher"></a>パブリッシャを削除する

マーケットプレースのパブリッシャーを削除します。

|コマンド オプション |説明 |
|---------|---------|
|出版社名 (必須) | 発行者の名前 (識別子など)。 |
|パーソナルアクセストークン (必須) | 発行元の認証に使用される個人用アクセス トークン。 |

```
VsixPublisher.exe deletePublisher -publisherName "{Publisher Name}" -personalAccessToken "{Personal Access Token}"
```

### <a name="deleteextension"></a>拡張機能を削除します。

マーケットプレースから拡張機能を削除します。

|コマンド オプション |説明 |
|---------|---------|
|拡張子名 (必須) | 削除する拡張機能の名前。 |
|出版社名 (必須) | 発行者の名前 (識別子など)。 |
|パーソナルアクセストークン | 発行元の認証に使用される個人用アクセス トークン。 指定しない場合、ログインしているユーザーから pat が取得されます。 |

```
VsixPublisher.exe deleteExtension -extensionName "{Extension Name}" -publisherName "{Publisher Name}"
```

### <a name="login"></a>ログイン (login)

発行者をマシンにログインさせます。

|コマンド オプション |説明 |
|---------|---------|
|パーソナルアクセストークン (必須) | 発行元の認証に使用される個人用アクセス トークン。 |
|出版社名 (必須) | 発行者の名前 (識別子など)。 |
|overwrite | 既存の発行元を新しい個人用アクセス トークンで上書きすることを指定します。 |

```
VsixPublisher.exe login -personalAccessToken "{Personal Access Token}" -publisherName "{Publisher Name}"
```

### <a name="logout"></a>logout

発行元をマシンからログアウトします。

|コマンド オプション |説明 |
|---------|---------|
|出版社名 (必須) | 発行者の名前 (識別子など)。 |
|ミッシングパブリッシャーを無視する | 指定された発行元がまだログインしていない場合に、ツールでエラーを発生しないように指定します。 |

```
VsixPublisher.exe logout -publisherName "{Publisher Name}"
```

## <a name="publishmanifest-file"></a>マニフェスト ファイルを発行する

発行マニフェスト ファイルは、**発行**コマンドによって使用されます。 これは、マーケットプレースが知る必要がある拡張機能に関するすべてのメタデータを表します。 アップロードされる拡張子が VSIX 拡張の場合、"id" プロパティには "internalName" が設定されている必要があります。 これは、残りの 「id」プロパティを vsixmanifest ファイルから生成できるためです。 拡張子が msi/exe またはリンク拡張の場合、ユーザーは"id" プロパティに必須フィールドを指定する必要があります。 マニフェストの残りの部分には、マーケットプレイス固有の情報 (カテゴリ、Q&A が有効かどうかなど) が含まれます。

VSIX 拡張機能の発行マニフェスト ファイルのサンプル:

```json
{
    "$schema": "http://json.schemastore.org/vsix-publish",
    "categories": [ "build", "coding" ],  // The categories of the extension. Between 1 and 3 categories are required.
    "identity": {
        "internalName": "MyVsixExtension" // If not specified, we try to generate the name from the display name of the extension in the vsixmanifest file.
                                            // Required if the display name is not the actual name of the extension.
    },
    "overview": "overview.md",            // Path to the "readme" file that gets uploaded to the Marketplace. Required.
    "priceCategory": "free",              // Either "free", "trial", or "paid". Defaults to "free".
    "publisher": "MyPublisherName",       // The name of the publisher. Required.
    "private": false,                     // Specifies whether or not the extension should be public when uploaded. Defaults to false.
    "qna": true,                          // Specifies whether or not the extension should have a Q&A section. Defaults to true.
    "repo": "https://github.com/MyPublisherName/MyVsixExtension" // Not required.
}
```

MSI/EXE またはリンク発行マニフェスト ファイルのサンプル:

```json
{
    "$schema": "http://json.schemastore.org/vsix-publish",
    "categories": [ "build", "coding" ],
    "identity": {
        "description": "My extension.", // The description of the extension. Required for non-vsix extensions.
        "displayName": "My Extension",  // The display name of the extension. Required for non-vsix extensions.
        "icon": "\\path\\to\\icon.ico", // The path to an icon file (can be relative to the json file location). Required for non-vsix extensions.
        "installTargets": [             // The installation targets for the extension. Required for non-vsix extensions.
            {
                "sku": "Microsoft.VisualStudio.Community",
                "version": "[10.0, 16.0)"
            }
        ],
        "internalName": "MyExtension",
        "language": "en-US",            // The default language id of the extension. Can be in the "1033" or "en-US" format. Required for non-vsix extensions.
        "tags": [ "tag1", "tag2" ],     // The tags for the extension. Not required.
        "version": "3.7.0",             // The version of the extension. Required for non-vsix extensions.
        "vsixId": "MyExtension",        // The vsix id of the extension. Not required but useful for showing updates to installed extensions.
    },
    "overview": "overview.md",
    "priceCategory": "free",
    "publisher": "MyPublisherName",
    "private": false,
    "qna": true,
    "repo": "https://github.com/MyPublisherName/MyVsixExtension"
}
```

## <a name="asset-files"></a>アセットファイル

アセットファイルは、Readmeファイルに画像などを埋め込むためのファイルを提供できます。 たとえば、拡張機能に次の "概要" マークダウン ドキュメントがある場合:

```markdown
TestExtension
...
This is test extension.
![Test logo](images/testlogo.png "Test logo")
```

前の例で "images/testlogo.png" を解決するために、ユーザーは次のように発行マニフェストに "assetFiles" を提供できます。

```json
{
    "assetFiles": [
        {
            "pathOnDisk": "\\path\\to\\logo.png",
            "targetPath": "images/logo.png"
        }
    ],
    // other required fields
}
```

## <a name="publishing-walkthrough"></a>発行のチュートリアル

### <a name="prerequisites"></a>必須コンポーネント

このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

### <a name="create-a-visual-studio-extension"></a>拡張機能を作成する

この場合、既定の VSPackage 拡張機能を使用しますが、同じ手順は、拡張機能のすべての種類に有効です。

1. メニュー コマンドを持つ "TestPublish" という名前の C# で VSPackage を作成します。 詳細については、「[最初の拡張の作成: Hello World](../extensibility/extensibility-hello-world.md)」を参照してください。

### <a name="package-your-extension"></a>拡張機能をパッケージ化する

1. 拡張機能 vsixmanifest を、製品名、作成者、およびバージョンに関する正しい情報で更新します。

   ![拡張機能の vsixmanifest を更新します。](media/update-extension-vsixmanifest.png)

2. **リリース**モードで拡張機能をビルドします。 これで、\bin\Release フォルダーに拡張機能が VSIX としてパッケージ化されます。

3. VSIX をダブルクリックして、インストールを確認できます。

### <a name="test-the-extension"></a>拡張機能をテストする

 拡張機能を配布する前に、ビルドし、テストして、Visual Studio の実験用インスタンスに正しくインストールされていることを確認します。

1. Visual Studio で、デバッグを開始します。 をクリックして、Visual Studio の実験用インスタンスを開きます。

2. 実験用の例では、[**ツール**] メニューの [**拡張機能と更新プログラム.** TestPublish 拡張機能が中央のウィンドウに表示され、有効にする必要があります。

3. [**ツール**] メニューにテスト コマンドが表示されていることを確認します。

### <a name="publish-the-extension-to-the-marketplace-via-command-line"></a>コマンドラインを使用して拡張機能を Marketplace に発行する

1. 拡張機能のリリース バージョンがビルドされていること、および最新の状態であることを確認します。

2. publishmanifest.json ファイルとoverview.mdファイルが作成されていることを確認します。

3. コマンド ラインを開き、${VSInstallDir}\VSSDK\VisualStudio 統合\ツール\ビン\ ディレクトリに移動します。

4. 新しいパブリッシャを作成するには、次のコマンドを使用します。

   ```
   VsixPublisher.exe createPublisher -publisherName "TestVSIXPublisher" -displayName "Test VSIX Publisher" -personalAccessToken "{Personal Access Token that is used to authenticate the publisher. If not provided, the pat is acquired from the logged-in users.}"
   ```

5. パブリッシャの作成が成功すると、次のコマンド ライン メッセージが表示されます。

   ```
   Added 'Test VSIX Publisher' as a publisher on the Marketplace.
   ```

6. 作成した新しいパブリッシャーを確認するには[、Visual Studio マーケットプレース](https://marketplace.visualstudio.com/manage/publishers)に移動します。

7. 新しい拡張機能を発行するには、次のコマンドを使用します。

   ```
   VsixPublisher.exe publish -payload "{Path to vsix file}"  -publishManifest "{path to publishManifest file}"
   ```

8. パブリッシャの作成が成功すると、次のコマンド ライン メッセージが表示されます。

   ```
   Uploaded 'MyVsixExtension' to the Marketplace.
   ```

9. 発行した新しい拡張機能を確認するには[、Visual Studio マーケットプレース](https://marketplace.visualstudio.com/)に移動します。

### <a name="install-the-extension-from-the-visual-studio-marketplace"></a>拡張機能を Visual Studio マーケットプレースからインストールする

拡張機能が発行された後、Visual Studio にインストールして、そこでテストします。

1. Visual Studio の [**ツール**] メニューの [**拡張機能と更新プログラム.**

2. [**オンライン**] をクリックし、次に [発行のテスト] を検索します。

3. **[Download]** をクリックします。 その後、拡張機能はインストールのスケジュールが設定されます。

4. インストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。

## <a name="remove-the-extension"></a>拡張機能を削除する

拡張機能は、Visual Studio マーケットプレースおよびコンピューターから削除できます。

### <a name="to-remove-the-extension-from-the-marketplace-via-command-line"></a>コマンドラインを使用してマーケットプレースから拡張機能を削除するには

1. 拡張機能を削除する場合は、次のコマンドを使用します。

   ```
   VsixPublisher.exe deleteExtension -publisherName "TestVSIXPublisher" -extensionName "MyVsixExtension"
   ```

2. 拡張機能が正常に削除されると、次のコマンド ライン メッセージが表示されます。

   ```
   Removed 'MyVsixExtension' from the Marketplace.
   ```

### <a name="to-remove-the-extension-from-your-computer"></a>コンピューターから拡張機能を削除するには

1. Visual Studio の [**ツール**] メニューの [**拡張機能と更新プログラム**] をクリックします。

2. [MyVsixExtension] を選択し、[**アンインストール**] をクリックします。 その後、拡張機能はアンインストールのスケジュールが設定されます。

3. アンインストールを完了するには、Visual Studio のすべてのインスタンスを閉じます。
