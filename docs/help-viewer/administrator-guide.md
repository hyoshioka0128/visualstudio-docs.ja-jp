---
title: ヘルプ ビューアーの管理者ガイド
ms.date: 11/01/2017
ms.topic: conceptual
ms.assetid: 4340c69f-b96b-4932-bb82-38b16a5ab149
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 037ee411c156d21145160dc95b40078fd841493c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "67825126"
---
# <a name="help-viewer-administrator-guide"></a>ヘルプ ビューアーの管理者ガイド

ヘルプ ビューアーを使用すると、インターネット アクセスの有無に関係なく、ネットワーク環境のローカル ヘルプのインストールを管理できます。 ローカル ヘルプ コンテンツは、コンピューターごとに構成されます。 既定では、ユーザーがローカル ヘルプのインストールを更新するには、そのユーザーに管理者権限が必要です。

ネットワーク環境でクライアントがインターネットにアクセスできるようにする場合は、 **ヘルプコンテンツマネージャー** の実行可能ファイルを使用して、インターネットからローカルヘルプコンテンツを展開できます。 *HlpCtntMgr.exe*のコマンドライン構文の詳細については、「[ヘルプコンテンツマネージャーのコマンドライン引数](../help-viewer/command-line-arguments.md)」を参照してください。

コンテンツの作成、イントラネット サービスのエンドポイントの作成、類似した種類のアクティビティの詳細については、[ヘルプ ビューアー SDK](../extensibility/internals/microsoft-help-viewer-sdk.md) を参照してください。

ご利用のネットワーク環境にインターネット アクセスがない場合、ヘルプ ビューアーでは、イントラネットかネットワーク共有からローカル ヘルプ コンテンツを展開できます。 次のような機能で[レジストリ キーをオーバーライド](../help-viewer/behavior-overrides.md)し、Visual Studio IDE のヘルプ オプションを無効にすることもできます。

- オンラインとオフラインのヘルプ

- IDE の初回起動時のコンテンツ インストール

- イントラネット コンテンツ サービスの指定

- コンテンツの管理

## <a name="deploy-local-help-content-from-the-internet"></a>インターネットからローカル ヘルプ コンテンツを配置する

**ヘルプ コンテンツ マネージャー** (*HlpCtntMgr.exe*) を利用し、インターネットからクライアント コンピューターにローカル ヘルプ コンテンツを配置できます。 次の構文を使用します。

```cmd
\\%ProgramFiles(x86)%\Microsoft Help Viewer\v2.3\HlpCtntmgr.exe /operation \<*name*> /catalogname \<*catalog name*> /locale \<*locale*>
```

*HlpCtntMgr.exe*のコマンドライン構文の詳細については、「[ヘルプコンテンツマネージャーのコマンドライン引数](../help-viewer/command-line-arguments.md)」を参照してください。

要件:

- クライアント コンピューターがインターネットにアクセスできる必要があります。

- インストール後にユーザーがローカル ヘルプ コンテンツを更新、追加、または削除するには、そのユーザーに管理者権限が必要です。

注意事項:

- ヘルプの既定のソースはオンラインのままです。

### <a name="example"></a>例

次の例では、クライアント コンピューターに Visual Studio の英語のコンテンツをインストールします。

#### <a name="to-install-english-content-from-the-internet"></a>インターネットから英語のコンテンツをインストールするには

1. **[スタート]** を選択し、**[ファイル名を指定して実行]** を選択します。

2. 次のように入力します。

     `C:\Program Files (x86)\Microsoft Help Viewer\v2.3\hlpctntmgr.exe /operation install /catalogname VisualStudio15 /locale en-us`

3. **Enter** キーを押します。

## <a name="deploy-pre-installed-local-help-content-on-client-computers"></a>事前にインストールされたローカル ヘルプ コンテンツをクライアント コンピューターに配置する

オンラインから 1 台のコンピューターに一連のコンテンツをインストールし、そのインストールされたコンテンツを他のコンピューターにコピーすることができます。

要件:

- 最初にコンテンツをインストールするコンピューターでは、インターネットにアクセスできる必要があります。

- インストール後にユーザーがローカル ヘルプ コンテンツを更新、追加、または削除するには、そのユーザーに管理者権限が必要です。

    > [!TIP]
    > ユーザーに管理者権限がない場合は、ヘルプ ビューアーで **[コンテンツの管理]** タブを無効にすることをお勧めします。 詳細については、「 [ヘルプコンテンツマネージャーのオーバーライド](../help-viewer/behavior-overrides.md)」を参照してください。

注意事項:

- ヘルプの既定のソースはオンラインのままです。

### <a name="create-the-content-set"></a>コンテンツ セットを作成する

基本コンテンツ セットを作成する前に、ターゲット コンピューターで Visual Studio のすべてのローカル コンテンツをアンインストールする必要があります。

#### <a name="to-uninstall-local-help"></a>ローカル ヘルプをアンインストールするには

1. ヘルプ ビューアーで、**[コンテンツの管理]** タブを選択します。

2. Visual Studio ドキュメント セットに移動します。

3. 各サブ項目の横の **[削除]** を選択します。

4. **[更新]** を選択し、アンインストールします。

5. *%ProgramData%\Microsoft\HelpLibrary2\Catalogs\VisualStudio15*を参照し、フォルダーにファイル*catalogType.xml*のみが含まれていることを確認します。

   前にインストールされた Visual Studio のローカル ヘルプ コンテンツをすべて削除したら、基本コンテンツ セットをダウンロードする準備が整いました。

#### <a name="to-download-the-content"></a>コンテンツをダウンロードするには

1. ヘルプ ビューアーで、**[コンテンツの管理]** タブを選択します。

2. **[推奨されるドキュメント]** または **[利用可能なドキュメント]** で、ダウンロードするドキュメント セットに移動し、**[追加]** を選択します。

3. **[更新]** を選択します。

次に、クライアント コンピューターに配置できるように、コンテンツをパッケージ化する必要があります。

#### <a name="to-package-the-content"></a>コンテンツをパッケージ化するには

1. 後の配置でコンテンツをコピーするフォルダーを作成します。 例: *\myserver\vshelp*。

2. 管理者のアクセス許可で *cmd.exe* を開きます。

3. 手順 1 で作成したフォルダーに移動します。

4. 次のように入力します。

     `Xcopy %ProgramData%\Microsoft\HelpLibrary2 \<*foldername*>\ /y /e /k /o`

     例: `Xcopy %ProgramData%\Microsoft\HelpLibrary2 c:\VSHelp\ /y /e /k /o`

### <a name="deploy-the-content"></a>コンテンツを配置する

1. ネットワーク共有を作成し、その場所にヘルプ コンテンツをコピーします。

     たとえば、 *\myserver\vshelp*の内容を* \\ \myserver\VSHelp*にコピーします。

2. ヘルプ コンテンツの配置スクリプトを含める *.bat* ファイルを作成します。 クライアントがプッシュの一部として、削除されるファイルのいずれかに読み取りロックを設定している可能性があるため、更新をプッシュする前にクライアントをシャットダウンする必要があります。 次に例を示します。

    ```cmd
    REM - copy pre-ripped content to ProgramData
    Xcopy %~dp0HelpLibrary2 %SYSTEMDRIVE%\ProgramData\Microsoft\HelpLibrary2\ /y /e /k /o
    if ERRORLEVEL 1 ECHO *** ERROR COPYING Help Library files to ProgramData (%ERRORLEVEL%)
    ```

3. ヘルプコンテンツをインストールするローカルコンピューターで *.bat* ファイルを実行します。

## <a name="see-also"></a>関連項目

- [ヘルプコンテンツマネージャーのコマンドライン引数](../help-viewer/command-line-arguments.md)
- [ヘルプコンテンツマネージャーのオーバーライド](../help-viewer/behavior-overrides.md)
- [Microsoft ヘルプ ビューアー](../help-viewer/overview.md)
- [ヘルプ ビューアー SDK](../extensibility/internals/microsoft-help-viewer-sdk.md)