---
title: 'チュートリアル: カスタム XAML をスタート ページに追加する |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- custom start page
- xaml start page
ms.assetid: 9af4d5f9-1cfc-4221-aea7-c8cd3f7571a6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 4e2afc90dc96978e8a8290afaa2d3278e8b621b3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697673"
---
# <a name="walkthrough-add-custom-xaml-to-the-start-page"></a>チュートリアル: カスタム XAML をスタート ページに追加する

このチュートリアルでは、Web ブラウザーを含むカスタム Visual Studio スタート ページを作成する方法を示します。

## <a name="add-custom-xaml"></a>カスタム XAML の追加

1. 「カスタムスタート ページの作成」の手順に従って[スタート ページを作成します](../extensibility/creating-a-custom-start-page.md)。

2. *MainWindow.xaml*ファイルで、[グリッド>] セクションを\<見つけます。

3. 次の\<例に示すように、グリッド\<>要素内に\<TabControl>要素と TabItem>を追加します。

    ```xml
    <Grid>
        <TabControl>
            <TabItem Header="Bing" Height="Auto">
                <Frame Source="http://www.bing.com" />
            </TabItem>
        </TabControl>
    </Grid>
    ```

4. 新しいプロジェクト\<を開く\<ボタン>要素を含む 2 つ目の TabItem>を追加します。

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

1. **F5**キーを押します。

     Visual Studio の実験用インスタンスが開き、カスタム スタート ページがインストールされていますが、選択されていません。

2. Visual Studio の実験用インスタンスで、[**ツール] / [オプション] / [環境**] ページを開きます。

3. [ スタートアップ ]**を選択**します。 [**スタート ページのカスタマイズ]** の一覧で *、.xaml*ファイルを選択し **、[OK]** をクリックします。

4. **[表示]** メニューの **[スタート ページ]** をクリックします。

5. **[Bing]** タブをクリックします。

     Bingの Web ページが表示されます。

6. [**マイ ボタン]** タブをクリックします。

     **[MyProject]** ボタンが表示され、[**新しいプロジェクト**] ダイアログが開きます。

7. 実験用インスタンスを閉じます。

カスタムスタート ページを適用するには、[**ツール** > **オプション** > **環境**] で [**スタートアップ**] を選択します。 [**スタート ページのカスタマイズ]** の一覧で *、.xaml*ファイルを選択し **、[OK]** をクリックします。

## <a name="next-steps"></a>次の手順

Visual Studio のスタート ページには、Web ブラウザー タブと [マイ ボタン] タブを表示するタブが表示されるようになりました。他の機能を持つカスタム スタート ページを作成するには、「スタート ページへのユーザー コントロールの追加」に示すように、*コード ビハインド*モデルを使用してカスタム .dll[を追加](../extensibility/adding-user-control-to-the-start-page.md)します。 作成された .vsix ファイルを[Visual Studio マーケットプレース](https://marketplace.visualstudio.com/)Web サイト、または別の Web サイトまたはネットワーク共有に発行することで、カスタム スタート ページを他のユーザーと共有できます。 詳細については、「 [Deploying Custom Start Pages](../extensibility/deploying-custom-start-pages.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [スタート ページをカスタマイズする](../ide/customizing-the-start-page-for-visual-studio.md)
- [WPF コンテナー コントロール](https://msdn.microsoft.com/library/a0177167-d7db-4205-9607-8ae316952566)
