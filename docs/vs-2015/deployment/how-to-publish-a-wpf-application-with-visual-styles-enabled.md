---
title: '方法: Visual スタイルが有効になっている WPF アプリケーションを発行する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
ms.assetid: 73b22b02-fc75-42aa-82d3-51fdcaf8e5c8
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c3691f782f317667b56f6bf3641c0f4c6a703eda
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697569"
---
# <a name="how-to-publish-a-wpf-application-with-visual-styles-enabled"></a>方法: Visual スタイルが有効になっている WPF アプリケーションを公開する

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

visual スタイルを使用すると、ユーザーが選択したテーマに基づいてコモン コントロールの外観を変更できます。 既定では、Visual スタイルは、Windows Presentation Foundation (WPF) アプリケーションで有効になっていないため、手動で有効にする必要があります。 ただし、WPF アプリケーションの Visual スタイルを有効にすると、ソリューションの発行によりエラーが発生します。 このトピックでは、このエラーを解決する方法と、Visual スタイルを有効にした WPF アプリケーションを発行するためのプロセスについて説明します。 視覚スタイルの詳細については、「 [Visual スタイルの概要](https://msdn.microsoft.com/5b5d7bb6-684f-478d-bf5f-b8d18bbcff2e)」を参照してください。 エラーメッセージの詳細については、「 [ClickOnce 配置での特定のエラーのトラブルシューティング](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md)」を参照してください。

 エラーを解決し、ソリューションを公開するには、次のタスクを実行します。

- [Visual スタイルを有効にせずにソリューションを発行](#BKMK_publishsolwovs)します。

- [マニフェストファイルを作成](#BKMK_CreateManifest)します。

- マニフェストファイルを、発行された[ソリューションの実行可能ファイルに埋め込み](#BKMK_embedmanifest)ます。

- [アプリケーション マニフェストと配置マニフェストに署名します](#BKMK_signappdeplyman)。

  その後、エンド ユーザーがアプリケーションをインストールする場所に、発行されたファイルを移動できます。

## <a name="publish-the-solution-without-visual-styles-enabled"></a><a name="BKMK_publishsolwovs"></a> Visual スタイルを有効にせずにソリューションを発行する

1. プロジェクトに有効になった Visual スタイルがないことを確認します。 最初に、プロジェクトのマニフェスト ファイルに次の XML があるかチェックします。 その後、XML がある場合は、コメント タグで XML を囲みます。

     既定では、Visual スタイルは有効になっていません。

    ```xml
    <dependency>
        <dependentAssembly>
          <assemblyIdentity
              type="win32"
              name="Microsoft.Windows.Common-Controls"
              version="6.0.0.0"
              processorArchitecture="*"
              publicKeyToken="6595b64144ccf1df"
              language="*" />
        </dependentAssembly>
      </dependency>
    ```

     次の手順は、プロジェクトに関連付けられたマニフェスト ファイルを開く方法を示します。

    **Visual Basic プロジェクトのマニフェスト ファイルを開くには**

    1. メニューバーで、[**プロジェクト**]、[ _projectname_の**プロパティ**] の順に選択します。 *projectname*は、WPF プロジェクトの名前です。

         WPF プロジェクトのプロパティ ページが表示されます。

    2. **[アプリケーション]** タブで、**[Windows 設定の表示]** をクリックします。

         **コード エディター**で app.manifest ファイルが開きます。

    **C# プロジェクトのマニフェスト ファイルを開くには**

    1. メニューバーで、[**プロジェクト**]、[ _projectname_の**プロパティ**] の順に選択します。 *projectname*は、WPF プロジェクトの名前です。

         WPF プロジェクトのプロパティ ページが表示されます。

    2. **[アプリケーション]** タブで、マニフェストのフィールドに表示される名前をメモします。 これは、プロジェクトに関連付けられているマニフェストの名前です。

        > [!NOTE]
        > **[マニフェストを既定の設定で埋め込みます]** または **[マニフェストなしでアプリケーションを作成する]** がマニフェスト フィールドに表示されている場合、Visual スタイルは有効になりません。 マニフェスト ファイルの名前がマニフェスト フィールドに表示されている場合は、この手順の次の手順に進みます。

    3. **ソリューションエクスプローラー**で、[**すべてのファイルを表示**] () を選択します。

         このボタンは、除外された項目や通常は表示されない項目も含め、すべてのプロジェクト項目を表示します。 マニフェスト ファイルはプロジェクト項目として表示されます。

2. ソリューションをビルドし、発行します。 ソリューションを発行する方法の詳細については、「 [方法: 発行ウィザードを使用して ClickOnce アプリケーションを発行](../deployment/how-to-publish-a-clickonce-application-using-the-publish-wizard.md)する」を参照してください。

## <a name="create-a-manifest-file"></a><a name="BKMK_CreateManifest"></a> マニフェストファイルを作成する

1. 次の XML をメモ帳ファイルに貼り付けます。

     この XML は、Visual スタイルをサポートするコントロールを含むアセンブリについて説明します。

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
     <asmv1:assembly manifestVersion="1.0"
         xmlns="urn:schemas-microsoft-com:asm.v1"
         xmlns:asmv1="urn:schemas-microsoft-com:asm.v1"
         xmlns:asmv2="urn:schemas-microsoft-com:asm.v2"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <dependency>
        <dependentAssembly>
          <assemblyIdentity
            type="win32"
            name="Microsoft.Windows.Common-Controls"
            version="6.0.0.0"
            processorArchitecture="*"
            publicKeyToken="6595b64144ccf1df"
            language="*" />
        </dependentAssembly>
      </dependency>
    </asmv1:assembly>
    ```

2. メモ帳の **[ファイル]** をクリックし、**[名前を付けて保存]** をクリックします。

3. **[名前を付けて保存]** ダイアログ ボックスの **[ファイルの種類]** ドロップダウン リストで、**[すべてのファイル]** をクリックします。

4. **[ファイル名]** ボックスで、ファイルに名前を付け、ファイル名の最後に **.manifest** を付けます。 例: **themes.manifest**。

5. **[フォルダーの参照]** ボタンをクリックしてフォルダーを選択し、**[保存]** をクリックします。

    > [!NOTE]
    > 残りの手順では、このファイルの名前が **themes.manifest** で、ファイルがコンピューターの C:\temp ディレクトリに格納されていることを前提とします。

## <a name="embed-the-manifest-file-into-the-executable-file-of-the-published-solution"></a><a name="BKMK_embedmanifest"></a> 発行されたソリューションの実行可能ファイルにマニフェストファイルを埋め込みます。

1. **Visual Studio コマンド プロンプト**を開きます。

    **Visual Studio コマンドプロンプト**を開く方法の詳細については、「[コマンドプロンプト](https://msdn.microsoft.com/library/94fcf524-9045-4993-bfb2-e2d8bad44219)」を参照してください。

   > [!NOTE]
   > 残りの手順は、ソリューションに関して以下を前提とします。
   >
   > - ソリューションの名前は **MyWPFProject** です。
   > - このソリューションは、次のディレクトリにあり `%UserProfile%\Documents\Visual Studio 2010\Projects\` ます。
   >
   > - ソリューションは、次のディレクトリに発行されます `%UserProfile%\Documents\Visual Studio 2010\Projects\publish` 。
   > - 発行されたアプリケーションファイルの最新バージョンは、次のディレクトリにあります。 `%UserProfile%\Documents\Visual Studio 2010\Projects\publish\Application Files\WPFApp_1_0_0_0`
   >
   > 上記の名前とディレクトリの場所は、いずれも使用する必要はありません。 前の名前と場所は、ソリューションの発行に必要な手順について説明するためにのみ使用されます。

2. コマンド プロンプトで、発行済みのアプリケーション ファイルの最新バージョンが含まれるディレクトリへのパスを変更します。 この手順を次の例に示します。

   ```
   cd "%UserProfile%\Documents\Visual Studio 2010\Projects\MyWPFProject\publish\Application Files\WPFApp_1_0_0_0"
   ```

3. コマンド プロンプトで、次のコマンドを実行して、アプリケーションの実行可能ファイルにマニフェスト ファイルを埋め込みます。

   ```
   mt –manifest c:\temp\themes.manifest –outputresource:MyWPFApp.exe.deploy
   ```

## <a name="sign-the-application-and-deployment-manifests"></a><a name="BKMK_signappdeplyman"></a> アプリケーションマニフェストと配置マニフェストに署名する

1. コマンド プロンプトで、次のコマンドを実行して、現在のディレクトリ内の実行可能ファイルから `.deploy` 拡張子を削除します。

   ```
   ren MyWPFApp.exe.deploy MyWPFApp.exe
   ```

   > [!NOTE]
   > この例では、1 つのファイルだけが `.deploy` ファイル拡張子を持っていると仮定しています。 このディレクトリ内の `.deploy` 拡張子を持つすべてのファイルの名前を変更してください。

2. コマンド プロンプトで、次のコマンドを実行してアプリケーション マニフェストに署名します。

   ```
   mage -u MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > この例では、プロジェクトの `.pfx` ファイルを使用してマニフェストに署名すると仮定しています。 マニフェストに署名していない場合は、 `–cf` この例で使用するパラメーターを省略できます。 パスワードを必要とする証明書でマニフェストに署名する場合は、 `–password` オプション () を指定し `For example: mage –u MyWPFApp.exe.manifest –cf ..\..\..\MyWPFApp_TemporaryKey.pfx – password Password` ます。

3. コマンド プロンプトで、次のコマンドを実行して、この手順の前の手順で名前を変更したファイルの名前に `.deploy` 拡張子を追加します。

   ```
   ren MyWPFApp.exe MyWPFApp.exe.deploy
   ```

   > [!NOTE]
   > この例では、1 つのファイルだけが `.deploy` ファイル拡張子を持っていたと仮定しています。 このディレクトリ内の `.deploy` 拡張子を持っていたすべてのファイルの名前を変更してください。

4. コマンド プロンプトで、次のコマンドを実行して配置マニフェストに署名します。

   ```
   mage -u ..\..\MyWPFApp.application -appm MyWPFApp.exe.manifest -cf ..\..\..\MyWPFApp_TemporaryKey.pfx
   ```

   > [!NOTE]
   > この例では、プロジェクトの `.pfx` ファイルを使用してマニフェストに署名すると仮定しています。 マニフェストに署名していない場合は、 `–cf` この例で使用するパラメーターを省略できます。 パスワードを必要とする証明書でマニフェストに署名する場合は、次の `–password` 例のようにオプションを指定し `For example: mage –u MyWPFApp.exe.manifest –cf ..\..\..\MyWPFApp_TemporaryKey.pfx – password Password` ます。

   これらの手順を実行した後、エンド ユーザーがアプリケーションをインストールする場所に、発行されたファイルを移動できます。 ソリューションを頻繁に更新する場合は、新しいバージョンを発行するたびに、スクリプトにこれらのコマンドを移動し、スクリプトを実行できます。

## <a name="see-also"></a>参照

[ClickOnce 配置](../deployment/troubleshooting-specific-errors-in-clickonce-deployments.md) 
 における特定のエラーのトラブルシューティング[視覚スタイルの概要](https://msdn.microsoft.com/5b5d7bb6-684f-478d-bf5f-b8d18bbcff2e) 
[コマンドプロンプト](https://msdn.microsoft.com/library/94fcf524-9045-4993-bfb2-e2d8bad44219)
