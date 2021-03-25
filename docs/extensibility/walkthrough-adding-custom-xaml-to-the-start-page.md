---
title: 'チュートリアル: スタートページへのカスタム XAML の追加 |Microsoft Docs'
description: このチュートリアルを使用して、web ブラウザーを含むカスタム Visual Studio のスタートページを作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- custom start page
- xaml start page
ms.assetid: 9af4d5f9-1cfc-4221-aea7-c8cd3f7571a6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 972f8c477a62078b14d16ff61d3f6b8c7978616d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062032"
---
# <a name="walkthrough-add-custom-xaml-to-the-start-page"></a>チュートリアル: スタートページへのカスタム XAML の追加

このチュートリアルでは、Web ブラウザーを含むカスタム Visual Studio のスタートページを作成する方法について説明します。

## <a name="add-custom-xaml"></a>カスタム XAML の追加

1. 「 [カスタムスタートページを作成する](../extensibility/creating-a-custom-start-page.md)」の手順に従って、スタートページを作成します。

2. *Mainwindow.xaml* ファイルで、セクションを見つけ \<Grid> ます。

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

## <a name="test-the-custom-start-page"></a>カスタムスタートページをテストする

1. **F5** キーを押します。

     Visual Studio の実験用インスタンスが開き、カスタムスタートページがインストールされますが、選択されていません。

2. Visual Studio の実験用インスタンスで、[ **ツール/Options/環境** ] ページを開きます。

3. [ **スタートアップ**] を選択します。 [ **スタートページのカスタマイズ** ] ボックスの一覧で、 *.xaml* ファイルを選択し、[ **OK]** をクリックします。

4. **[表示]** メニューの **[スタート ページ]** をクリックします。

5. [ **Bing** ] タブをクリックします。

     Bing web ページが表示できます。

6. [ **MyButton** ] タブをクリックします。

     **MyProject** ボタンが表示され、[**新しいプロジェクト**] ダイアログボックスが開きます。

7. 実験用インスタンスを閉じます。

カスタムスタートページを適用するには、[**ツール**  >  **オプション]**[  >  **環境**] で [**スタートアップ**] を選択します。 [ **スタートページのカスタマイズ** ] ボックスの一覧で、 *.xaml* ファイルを選択し、[ **OK]** をクリックします。

## <a name="next-steps"></a>次のステップ

Visual Studio のスタートページに、[Web ブラウザー] タブと [MyButton] タブを表示するタブが表示されるようになりました。他の機能を持つカスタムスタートページを作成するには、「[スタートページへのユーザーコントロールの追加](../extensibility/adding-user-control-to-the-start-page.md)」の説明に従って、カスタム .dll を追加するための *分離コード* モデルを使用します。 作成した .vsix ファイルを [Visual Studio Marketplace](https://marketplace.visualstudio.com/) の web サイト、または別の web サイトまたはネットワーク共有に発行することで、カスタムスタートページを他のユーザーと共有できます。 詳細については、「 [Deploying Custom Start Pages](../extensibility/deploying-custom-start-pages.md)」を参照してください。

## <a name="see-also"></a>こちらもご覧ください

- [スタートページをカスタマイズする](../ide/customizing-the-start-page-for-visual-studio.md)
- [WPF コンテナーコントロール](/previous-versions/bb675291(v=vs.110))