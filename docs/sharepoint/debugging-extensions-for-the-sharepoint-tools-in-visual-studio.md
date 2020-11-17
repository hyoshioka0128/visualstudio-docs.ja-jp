---
title: Visual Studio での SharePoint ツールの拡張機能のデバッグ |Microsoft Docs
description: Visual Studio の SharePoint ツールの拡張機能をデバッグします。 実験用インスタンスまたはの通常のインスタンス (VS) で SharePoint ツールの拡張機能をデバッグします。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, debugging extensions
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 5ad95ce8b4ab9567f22748453ae59c258f24aa86
ms.sourcegitcommit: 3d96f7a8c9affab40358c3e81e3472db31d841b2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/17/2020
ms.locfileid: "94671221"
---
# <a name="debug-extensions-for-the-sharepoint-tools-in-visual-studio"></a>Visual Studio での SharePoint ツールの拡張機能のデバッグ
  Visual Studio の実験用インスタンスまたは通常のインスタンスで、SharePoint ツールの拡張機能をデバッグできます。 拡張機能の動作をトラブルシューティングする必要がある場合は、レジストリ値を変更して、追加のエラー情報を表示し、Visual Studio での SharePoint コマンドの実行方法を構成することもできます。

## <a name="debug-extensions-in-the-experimental-instance-of-visual-studio"></a>Visual Studio の実験用インスタンスでの拡張機能のデバッグ
 テストされていない拡張機能による誤った破損から Visual Studio 開発環境を保護するために、Visual Studio SDK には、拡張機能のインストールとテストに使用できる、 *実験用インスタンス* と呼ばれる別の visual studio インスタンスが用意されています。 新しい拡張機能は Visual Studio の通常のインスタンスを使用して開発しますが、デバッグと実行は実験用インスタンスで行います。 詳細については、 [実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。

 VSIX プロジェクトを使用して拡張機能を配置し、その VSIX プロジェクトをソリューションのスタートアップ プロジェクトにする場合は、ソリューションをデバッグするときに、実験用インスタンスで拡張機能が自動的にインストールされて実行されます。 スタートアップ プロジェクトとは、複数のプロジェクトを含むソリューションをデバッグするときに開始されるプロジェクトです。 VSIX プロジェクトを使用した拡張機能の配置の詳細については、「 [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

 Visual Studio の実験用インスタンスでさまざまな種類の拡張機能をデバッグする方法を示す例については、次のチュートリアルを参照してください。

- [チュートリアル: SharePoint プロジェクト項目の種類の拡張](../sharepoint/walkthrough-extending-a-sharepoint-project-item-type.md)

- [チュートリアル: 項目テンプレートを使用してカスタム動作プロジェクト項目を作成する (パート 1)](../sharepoint/walkthrough-creating-a-custom-action-project-item-with-an-item-template-part-1.md)

- [チュートリアル: SharePoint プロジェクトのカスタム配置手順の作成](../sharepoint/walkthrough-creating-a-custom-deployment-step-for-sharepoint-projects.md)

- [チュートリアル: サーバーエクスプローラーを拡張して web パーツを表示する](../sharepoint/walkthrough-extending-server-explorer-to-display-web-parts.md)

- [チュートリアル: サーバーエクスプローラーの拡張機能で SharePoint クライアントオブジェクトモデルを呼び出す](../sharepoint/walkthrough-calling-into-the-sharepoint-client-object-model-in-a-server-explorer-extension.md)

## <a name="debug-extensions-in-the-regular-instance-of-visual-studio"></a>Visual Studio の通常のインスタンスでの拡張機能のデバッグ
 Visual Studio の通常のインスタンスで拡張機能プロジェクトをデバッグするには、まず、その拡張機能を通常のインスタンスにインストールします。 次に、デバッガーを Visual Studio の第 2 プロセスにアタッチします。 デバッグの完了後、拡張機能を削除して、開発用コンピューターに読み込まれないようにすることができます。

#### <a name="to-install-the-extension"></a>拡張機能をインストールするには

1. Visual Studio のすべてのインスタンスを閉じます。

2. 拡張プロジェクトのビルド出力フォルダーで、.vsix ファイルをダブルクリックするか、ショートカットメニューを開き、[**開く**] を選択して、 *.vsix* ファイルを開きます。

3. [ **Visual Studio 拡張機能インストーラー** ] ダイアログボックスで、拡張機能をインストールする visual studio のエディションを選択し、[ **インストール** ] をクリックします。

     Visual Studio によって、%UserProfile%\AppData\Local\Microsoft\VisualStudio\11.0\Extensions \\ *author name* \\ *extension name* \\ *バージョン* に拡張ファイルがインストールされます。 このパスの最後の3つのフォルダーは `Author` 、 `Name` `Version` 拡張機能の *source.extension.vsixmanifest* ファイルの、、およびの各要素から構成されます。

4. Visual Studio によって拡張機能がインストールされたら、[ **閉じる** ] をクリックします。

#### <a name="to-debug-the-extension"></a>拡張機能をデバッグするには

1. 管理者特権で Visual Studio を開き、拡張機能プロジェクトを開きます。 次の手順では、 *最初のインスタンス* として Visual Studio のこのインスタンスを参照します。

2. Visual Studio の別のインスタンスを管理者特権で起動します。 次の手順では、 *2 番目のインスタンス* として Visual Studio のこのインスタンスを参照します。

3. Visual Studio の第 1 インスタンスに切り替えます。

4. メニューバーで、[ **デバッグ**]、[ **プロセスにアタッチ**] の順に選択します。

5. [選択 **可能なプロセス** ] ボックスの一覧で、[ *devenv.exe*] を選択します。 これが、Visual Studio の第 2 インスタンスを表します。プロジェクトの拡張機能は、このインスタンスでデバッグすることになります。

6. [ **アタッチ** ] ボタンをクリックします。

     Visual Studio によって拡張機能プロジェクトがデバッグ モードで実行されます。

7. Visual Studio の第 2 インスタンスに切り替えます。

8. 拡張機能を読み込む新しい SharePoint プロジェクトを作成します。 たとえば、リスト定義プロジェクト項目の拡張機能をデバッグする場合は、 **リスト定義** プロジェクトを作成します。

9. 拡張機能のコードのテストに必要な手順をすべて実行します。

10. 拡張機能のデバッグが完了したら、Visual Studio の第 2 インスタンスを閉じます。

#### <a name="to-remove-the-extension"></a>拡張機能を削除するには

1. Visual Studio のメニューバーで、[ **ツール**]、[ **拡張機能と更新プログラム**] の順に選択します。

     **[拡張機能と更新プログラム]** ダイアログ ボックスが表示されます。

2. 拡張機能の一覧で、拡張機能の名前を選択し、[ **アンインストール** ] をクリックします。

3. 表示されるダイアログボックスで、 **[はい** ] をクリックして、拡張機能をアンインストールすることを確認します。

4. [ **今すぐ再起動** ] ボタンをクリックして、アンインストールを完了します。

## <a name="debug-sharepoint-commands"></a>SharePoint コマンドのデバッグ
 SharePoint ツールの拡張機能の一部である SharePoint コマンドをデバッグする場合は、 *vssphost4.exe* プロセスにデバッガーをアタッチする必要があります。 これは、SharePoint コマンドを実行する 64 ビット ホスト プロセスです。 SharePoint コマンドと *vssphost4.exe* の詳細については、「 [sharepoint オブジェクトモデルの呼び出し](../sharepoint/calling-into-the-sharepoint-object-models.md)」を参照してください。

#### <a name="to-attach-the-debugger-to-the-vssphost4exe-process"></a>vssphost4.exe プロセスにデバッガーをアタッチするには

1. 前に説明した手順に従って、Visual Studio の実験用インスタンスまたは Visual Studio の通常のインスタンスで拡張機能のデバッグを開始します。

2. デバッガーを実行している Visual Studio のインスタンスのメニューバーで、[ **デバッグ**]、[ **プロセスにアタッチ**] の順に選択します。

3. [選択 **可能なプロセス** ] ボックスの一覧で、[ *vssphost.exe*] を選択します。

    > [!NOTE]
    > vssphost.exe が一覧に表示されない場合は、拡張機能を実行している Visual Studio のインスタンスで *vssphost4.exe* プロセスを開始する必要があります。 通常、そのためには、Visual Studio によって開発コンピューター上の SharePoint サイトに接続する操作を実行します。 たとえば、Visual Studio は、[**サーバーエクスプローラー** ] ウィンドウの [ **SharePoint 接続**] ノードの下にあるサイト接続ノード (サイトの URL を表示するノード) を展開するか、**リストインスタンス** や **イベントレシーバー** 項目などの特定の sharepoint プロジェクトアイテムを sharepoint プロジェクトに追加するときに *vssphost4.exe* 開始します。

4. [ **アタッチ** ] ボタンをクリックします。

5. デバッグ対象の Visual Studio のインスタンスで、コマンドの実行に必要な手順を実行します。

## <a name="modify-registry-values-to-help-debug-sharepoint-tools-extensions"></a>SharePoint ツールの拡張機能のデバッグに役立つようにレジストリ値を変更する
 Visual Studio の SharePoint ツールの拡張機能をデバッグする場合は、レジストリの値を変更すると、拡張機能のトラブルシューティングに役立ちます。 値は **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools** キーの下に存在します。 既定では、これらの値は存在しません。

 SharePoint ツールの拡張機能をトラブルシューティングする場合は、EnableDiagnostics 値を作成して設定できます。 その値を次の表に示します。

|値|説明|
|-----------|-----------------|
|EnableDiagnostics|診断メッセージを **出力** ウィンドウに表示するかどうかを指定する REG_DWORD ます。<br /><br /> 診断メッセージを表示する場合は、この値を 1 に設定します。 メッセージを表示しないようにするには、この値を 0 に設定するか、または削除します。<br /><br /> SharePoint ツールの拡張機能から **出力** ウィンドウにメッセージを書き込むには、sharepoint プロジェクトサービスを使用します。 詳細については、「 [SharePoint プロジェクトサービスの使用](../sharepoint/using-the-sharepoint-project-service.md)」を参照してください。|

 拡張機能に SharePoint コマンドが含まれる場合は、コマンドのトラブルシューティングに役立つ追加の値を作成して設定できます。 次の表では、これらの値を説明します。

|値|説明|
|-----------|-----------------|
|AttachDebuggerToHostProcess|起動時にデバッガーを *vssphost4.exe* にアタッチできるダイアログボックスを表示するかどうかを指定する REG_DWORD ます。 これは、デバッグするコマンドが vssphost.exe の開始直後にそのプロセスによって実行され、コマンドが実行される前に手動でデバッガーをアタッチする時間がない場合に役立ちます。 ダイアログボックスを表示するに *vssphost4.exe* は、vssphost4.exe<xref:System.Diagnostics.Debugger.Break%2A> 起動時にメソッドを呼び出します。<br /><br /> この動作を有効にするには、この値を 1 に設定します。 この動作を無効にするには、この値を 0 に設定するか、または削除します。<br /><br /> この値を1に設定した場合は、ホストが正常に開始されたことを Visual Studio が要求する前に、HostProcessStartupTimeout 値を増やして、デバッガーをアタッチするのに十分な時間を与えるようにすることもでき *vssphost4.exe* ます。|
|ChannelOperationTimeout|SharePoint コマンドの実行を待機する時間 (秒単位) を指定する REG_DWORD です。 時間内にコマンドが実行されない場合、<xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException> がスローされます。<br /><br /> 既定値は 120 秒です。|
|HostProcessStartupTimeout|*vssphost4.exe* が正常に開始されたことを Visual Studio が通知するまでの時間を秒単位で指定する REG_DWORD。 *vssphost4.exe* が正常に開始されたことを通知しない場合は、 <xref:Microsoft.VisualStudio.SharePoint.SharePointConnectionException> がスローされます。<br /><br /> 既定値は 60 秒です。|
|MaxReceivedMessageSize|Visual Studio と *vssphost4.exe* 間で渡される WCF メッセージの最大許容サイズ (バイト単位) を指定する REG_DWORD。<br /><br /> 既定値は 1,048,576 バイト (1 MB) です。|
|MaxStringContentLength|Visual Studio と *vssphost4.exe* 間で渡される文字列の最大許容サイズ (バイト単位) を指定する REG_DWORD。<br /><br /> 既定値は 1,048,576 バイト (1 MB) です。|

## <a name="see-also"></a>関連項目

- [Visual Studio での SharePoint ツールの拡張](../sharepoint/extending-the-sharepoint-tools-in-visual-studio.md)
- [Visual Studio での SharePoint ツールの拡張機能の配置](../sharepoint/deploying-extensions-for-the-sharepoint-tools-in-visual-studio.md)
