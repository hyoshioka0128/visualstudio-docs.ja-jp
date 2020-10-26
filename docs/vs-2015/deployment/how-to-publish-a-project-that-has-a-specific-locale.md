---
title: '方法: 特定のロケールを持つプロジェクトを発行する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- publishing, localized projects
- locales, publishing for
- deploying applications [ClickOnce], localized projects
- locales, deploying for
- publishing localized projects
- macros, deploying with
- macros, publishing with
ms.assetid: 7c4cd83a-f985-4c85-9022-fadb5dbd2b39
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 42fc6e45e0e32e9b165251c7ec61d3d67b924e1c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697605"
---
# <a name="how-to-publish-a-project-that-has-a-specific-locale"></a>方法 : 特定のロケールを持つプロジェクトを発行する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

1 つのアプリケーションに、ロケールの異なる複数のコンポーネントが含まれることも少なくありません。 その場合、複数のプロジェクトを持つソリューションを作成し、ロケールごとに個別のプロジェクトを発行することになります。 以降の手順では、マクロを使用して、ソリューションの 1 つ目のプロジェクトを 'en' ロケールを使用して発行する方法について説明しています。 この手順を 'en' 以外のロケールで実行する場合は、マクロ内の `localeString` を、使用するロケール ('de' や 'de-DE' など) に設定してください。  
  
> [!NOTE]
> このマクロを使用するには、[発行場所] に有効な URL または UNC (Universal Naming Convention) 共有を指定する必要があります。 また、コンピューターにインターネット インフォメーション サービス (IIS: Internet Information Service) がインストールされている必要があります。 IIS をインストールするには、**[スタート]** メニューの **[コントロール パネル]** をクリックします。 **[プログラムの追加と削除]** をダブルクリックします。 **[プログラムの追加と削除]** で **[Windows コンポーネントの追加と削除]** をクリックします。 **Windows コンポーネント ウィザード**の **[コンポーネント]** リストで、**[インターネット インフォメーション サービス (IIS)]** チェック ボックスをオンにします。 次に、[完了****] をクリックしてウィザードを閉じます。  
  
### <a name="to-create-the-publishing-macro"></a>発行マクロを作成するには  
  
1. マクロ エクスプローラーを開くには、**[ツール]** メニューの **[マクロ]** をポイントし、**[マクロ エクスプローラー]** をクリックします。  
  
2. 新しいマクロ モジュールを作成します。 マクロ エクスプローラーで **[MyMacros]** を選択します。 **[ツール]** メニューの **[マクロ]** をポイントし、**[新しいマクロ モジュール]** をクリックします。 モジュールに "**PublishSpecificCulture**" という名前を付けます。  
  
3. マクロ エクスプローラーで **[MyMacros]** ノードを展開し、**[PublishAllProjects]** モジュールをダブルクリックして開きます。(または、**[ツール]** メニューの **[マクロ]** をポイントし、**[マクロ IDE]** をクリックします。)  
  
4. マクロ IDE で、モジュールの `Import` ステートメントに続けて次のコードを追加します。  
  
    ```vb  
    Module PublishSpecificCulture  
        Sub PublishProjectFirstProjectWithEnLocale()  
            ' Note: You should publish projects by using the IDE at least once  
            ' before you use this macro. Items such as the certificate and the   
            ' security zone must be set.  
            Dim localeString As String = "en"  
  
            ' Get first project.  
            Dim proj As Project = DTE.Solution.Projects.Item(1)  
            Dim publishProperties As Object = proj.Properties.Item("Publish").Value  
  
            ' GenerateManifests and SignManifests must always be set to  
            ' True for publishing to work.   
            proj.Properties.Item("GenerateManifests").Value = True  
            proj.Properties.Item("SignManifests").Value = True  
  
            'Set the publish language.  
            'This will set the deployment language and pick up all   
            ' en resource dlls:  
            Dim originalTargetCulture As String = _  
                publishProperties.Item("TargetCulture").Value  
            publishProperties.Item("TargetCulture").Value = localeString  
  
            'Append 'en' to end of publish, install, and update URLs if needed:  
            Dim originalPublishUrl As String = _  
                publishProperties.Item("PublishUrl").Value  
            Dim originalInstallUrl As String = _  
                publishProperties.Item("InstallUrl").Value  
            Dim originalUpdateUrl As String = _  
                publishProperties.Item("UpdateUrl").Value  
            publishProperties.Item("PublishUrl").Value = _  
                AppendStringToUrl(localeString, New Uri(originalPublishUrl))  
            If originalInstallUrl <> String.Empty Then  
                publishProperties.Item("InstallUrl").Value = _  
                    AppendStringToUrl(localeString, New Uri(originalInstallUrl))  
            End If  
            If originalUpdateUrl <> String.Empty Then  
                publishProperties.Item("UpdateUrl").Value = _  
                    AppendStringToUrl(localeString, New Uri(originalUpdateUrl))  
            End If  
            proj.Save()  
  
            Dim slnbld2 As SolutionBuild2 = _  
                CType(DTE.Solution.SolutionBuild, SolutionBuild2)  
            slnbld2.Clean(True)  
  
            slnbld2.BuildProject( _  
            proj.ConfigurationManager.ActiveConfiguration.ConfigurationName, _  
            proj.UniqueName, True)  
  
            ' Only publish if build is successful.  
            If slnbld2.LastBuildInfo <> 0 Then  
                MsgBox("Build failed for " & proj.UniqueName)  
            Else  
                slnbld2.PublishProject( _  
                proj.ConfigurationManager.ActiveConfiguration.ConfigurationName, _  
                proj.UniqueName, True)  
                If slnbld2.LastPublishInfo = 0 Then  
                    MsgBox("Publish succeeded for " & proj.UniqueName _  
                    & vbCrLf & "." _  
                    & " Publish Language was '" & localeString & "'.")  
                Else  
                    MsgBox("Publish failed for " & proj.UniqueName)  
                End If  
            End If  
  
            ' Return URLs and target culture to their previous state.  
            publishProperties.Item("PublishUrl").Value = originalPublishUrl  
            publishProperties.Item("InstallUrl").Value = originalInstallUrl  
            publishProperties.Item("UpdateUrl").Value = originalUpdateUrl  
            publishProperties.Item("TargetCulture").Value = originalTargetCulture  
            proj.Save()  
        End Sub  
  
        Private Function AppendStringToUrl(ByVal str As String, _  
        ByVal baseUri As Uri) As String  
            Dim returnValue As String = baseUri.OriginalString  
            If baseUri.IsFile OrElse baseUri.IsUnc Then  
                returnValue = IO.Path.Combine(baseUri.OriginalString, str)  
            Else  
                If Not baseUri.ToString.EndsWith("/") Then  
                    returnValue = baseUri.OriginalString & "/" & str  
                Else  
                    returnValue = baseUri.OriginalString & str  
                End If  
            End If  
            Return returnValue  
        End Function  
    End Module  
    ```  
  
5. マクロ IDE を閉じます。 フォーカスが Visual Studio に戻ります。  
  
### <a name="to-publish-a-project-for-a-specific-locale"></a>特定のロケールのプロジェクトを発行するには  
  
1. Visual Basic Windows アプリケーション プロジェクトを作成するには、**[ファイル]** メニューの **[新規作成]** をポイントし、**[プロジェクト]** をクリックします。  
  
2. **[新しいプロジェクト]** ダイアログ ボックスの **[Visual Basic]** ノードで、**[Windows アプリケーション]** を選択します。 プロジェクトに "**PublishLocales**" という名前を付けます。  
  
3. Form1 をクリックします。 **[プロパティ]** ウィンドウの **[デザイン]** で、**[Language]** プロパティを **[(既定値)]** から **[英語]** に変更します。 フォームの **[Text]** プロパティを **MyForm** に変更します。  
  
     ローカライズされたリソース DLL は必要になるまで作成されません。 たとえば、新しいロケールを指定した後で、フォームやそのコントロールのテキストを変更した場合などに作成されます。  
  
4. Visual Studio IDE を使用して、PublishLocales を発行します。  
  
     **ソリューションエクスプローラー**で、[publishlocales] を選択します。 **[プロジェクト]** メニューの **[プロパティ]** を選択します。 プロジェクトデザイナーの [ **発行** ] ページで、発行場所を指定し、 **http://localhost/PublishLocales** [ **今すぐ発行**] をクリックします。  
  
     発行 Web ページが表示されたら、そのページを終了します。 (この手順では、プロジェクトを発行するだけで、インストールする必要はありません。)  
  
5. [Visual Studio コマンド プロンプト] ウィンドウでマクロを呼び出し、PublishLocales をもう一度発行します。 コマンドプロンプトウィンドウを表示するには、[ **表示** ] メニューの [ **その他のウィンドウ** ] をポイントし、[ **コマンドウィンドウ**] をクリックするか、ctrl + ALT + A キーを押します。 コマンドプロンプトウィンドウで、「」と入力すると、 `macros` 使用可能なマクロの一覧が表示されます。 次のマクロを選択し、Enter キーを押します。  
  
     `Macros.MyMacros.PublishSpecificCulture.PublishProjectFirstProjectWithEnLocale`  
  
6. 発行プロセスが正常に完了すると、"PublishLocales\PublishLocales.vbproj の発行は成功しました。 発行言語は ' en ' でした。 "メッセージボックスで [ **OK]** をクリックします。 発行 Web ページが表示されたら、**[インストール]** をクリックします。  
  
7. C:\Inetpub\wwwroot\PublishLocales\en にアクセスします。 ローカライズされたリソース DLL のほかに、マニフェスト、setup.exe、発行 Web ページ ファイルなどのインストールされたファイルがあるはずです。 (既定では、ClickOnce は EXE ファイルおよび DLL ファイルに .deploy という拡張子を追加します。この拡張子は展開後に削除できます。)  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションの発行](../deployment/publishing-clickonce-applications.md)   
 [マクロ開発環境](https://msdn.microsoft.com/d23105d8-34fe-4ad9-8278-fae2c660aeac)   
 [マクロエクスプローラーウィンドウ](https://msdn.microsoft.com/762169e6-f83f-44b4-bffa-d0f107cae9a3)   
 [方法: マクロを編集し、プログラムで作成する](https://msdn.microsoft.com/6716f820-1feb-48ad-a718-27eb6b473c5a)
