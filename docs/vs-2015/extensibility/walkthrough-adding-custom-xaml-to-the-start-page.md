---
title: 'チュートリアル: スタートページへのカスタム XAML の追加 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- custom start page
- xaml start page
ms.assetid: 9af4d5f9-1cfc-4221-aea7-c8cd3f7571a6
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 7b2de492bd1eddf4bf18e4824cdb64de4241fa5f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65674122"
---
# <a name="walkthrough-adding-custom-xaml-to-the-start-page"></a>チュートリアル: カスタム XAML をスタート ページに追加する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、Web ブラウザーを含むカスタム Visual Studio のスタートページを作成する方法について説明します。  
  
## <a name="adding-custom-xaml"></a>追加 (カスタム XAML を)  
  
1. 「 [カスタムスタートページを作成](../extensibility/creating-a-custom-start-page.md)する」の手順に従って、スタートページを作成します。  
  
2. Mainwindow.xaml ファイルで、セクションを見つけ \<Grid> ます。  
  
3. 次の \<TabControl> \<TabItem> 例に示すように、要素内に要素とを追加し \< Grid> ます。  
  
    ```xml  
    <Grid>  
        <TabControl>  
            <TabItem Header="Bing" Height="Auto">  
                <Frame Source="http://www.bing.com" />  
            </TabItem>  
        </TabControl>  
    </Grid>  
    ```  
  
4. \<TabItem>新しいプロジェクトを開く要素を含む2つ目のを追加し \<Button> ます。  
  
    ```xml  
    <Grid>  
        <TabControl>  
            <TabItem Header="MyButton" Height="Auto">  
                <Button Name="btnNewProj" Content="New Project"   
                    Command="{x:Static vscom:VSCommands.ExecuteCommand}"  
                    CommandParameter="File.NewProject" >  
                </Button>  
            </TabItem>  
            <TabItem Header="Bing" Height="Auto">  
                <Frame Source="http://www.bing.com" />  
            </TabItem>  
        </TabControl>  
    </Grid>  
    ```  
  
## <a name="testing-the-custom-start-page"></a>カスタムスタートページのテスト  
  
1. F5 キーを押す。  
  
     Visual Studio の実験用インスタンスが開き、カスタムスタートページがインストールされますが、選択されていません。  
  
2. Visual Studio の実験用インスタンスで、[ **ツール/Options/環境** ] ページを開きます。  
  
3. [ **スタートアップ**] を選択します。 [ **スタートページのカスタマイズ** ] ボックスの一覧で、.xaml ファイルを選択し、[ **OK]** をクリックします。  
  
4. **[表示]** メニューの **[スタート ページ]** をクリックします。  
  
5. [ **Bing** ] タブをクリックします。  
  
     Bing web ページが表示できます。  
  
6. [ **MyButton** ] タブをクリックします。  
  
     **MyProject**ボタンが表示され、[**新しいプロジェクト**] ダイアログボックスが開きます。  
  
7. 実験用インスタンスを閉じます。  
  
## <a name="applying-the-custom-start-page"></a>カスタムスタートページの適用  
  
#### <a name="to-test-the-custom-start-page"></a>カスタムスタートページをテストするには  
  
1. [ **ツール**]、[オプション]、[環境] で、[ **スタートアップ**] を選択します。 [ **スタートページのカスタマイズ** ] ボックスの一覧で、.xaml ファイルを選択し、[ **OK]** をクリックします。  
  
## <a name="next-steps"></a>次の手順  
 Visual Studio のスタートページに、[Web ブラウザー] タブと [MyButton] タブを表示するタブが表示されるようになりました。他の機能を持つカスタムスタートページを作成するには、「[スタートページへのユーザーコントロールの追加](../extensibility/adding-user-control-to-the-start-page.md)」の説明に従って、カスタム .dll を追加するための*分離コード*モデルを使用します。 作成した .vsix ファイルを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) の web サイト、または別の web サイトまたはネットワーク共有に発行することで、カスタムスタートページを他のユーザーと共有できます。 詳細については、「 [Deploying Custom Start Pages](../extensibility/deploying-custom-start-pages.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [スタートページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)   
 [WPF コンテナーコントロール](https://msdn.microsoft.com/a0177167-d7db-4205-9607-8ae316952566)
