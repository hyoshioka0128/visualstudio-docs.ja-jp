---
title: カスタムスタートページを作成する |Microsoft Docs
description: カスタムスタートページを作成する方法について説明します。 空白のスタートページから開始し、コントロールを空の UserControl 要素に追加して、ページをテストします。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
ms.assetid: d67e0c53-9f5a-45fb-a929-b9d2125c3c82
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 65415c22da2815650278ac1190e7d19f54b96063
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99853086"
---
# <a name="creating-a-custom-start-page"></a>カスタムスタートページの作成

このドキュメントの手順に従って、カスタムスタートページを作成できます。

## <a name="create-a-blank-start-page"></a>空白のスタートページを作成する

最初に、Visual Studio が認識するタグ構造を持つ *.xaml* ファイルを作成して、空のスタートページを作成します。 次に、マークアップと分離コードを追加して、必要な外観と機能を生成します。

1. **WPF アプリケーション** の種類の新しいプロジェクトを作成します (**Visual C#**  >  **Windows デスクトップ**)。

2. `Microsoft.VisualStudio.Shell.14.0` への参照を追加します。

3. XML エディターで XAML ファイルを開き、最上位の \<Window> 要素を、 \<UserControl> 名前空間宣言を削除せずに要素に変更します。

4. `x:Class`最上位レベルの要素から宣言を削除します。 これにより、スタートページをホストする Visual Studio ツールウィンドウと XAML コンテンツとの互換性が確保されます。

5. 次の名前空間宣言を最上位の要素に追加し \<UserControl> ます。

    ```vb
    xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
    xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
    ```

     これらの名前空間を使用すると、Visual Studio のコマンド、コントロール、および UI の設定にアクセスできます。 詳細については、「 [スタートページへの Visual Studio コマンドの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)」を参照してください。

     次の例は、空のスタートページの *.xaml* ファイルのマークアップを示しています。 カスタムコンテンツは、内側の要素に含まれている必要があり <xref:System.Windows.Controls.Grid> ます。

    ```vb
    <UserControl
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:MyNamespace="clr-namespace:ManualStartPage;assembly=ManualStartPage"
        xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
                xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
        xmlns:local="clr-namespace:StartPageHost"
        mc:Ignorable="d"
         Height="350" Width="525">
        <Grid>
        <!--Add content here.-->
        </Grid>
    </UserControl>
    ```

6. 空の要素にコントロールを追加し \<UserControl> て、カスタムスタートページに入力します。 Visual Studio に固有の機能を追加する方法の詳細については、「 [スタートページへの Visual studio コマンドの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)」を参照してください。

## <a name="test-and-apply-the-custom-start-page"></a>カスタムスタートページのテストと適用

Visual studio のプライマリインスタンスは、Visual Studio がクラッシュしないことを確認するまで、カスタムスタートページを実行するように設定しないでください。 代わりに、実験用インスタンスでテストします。

### <a name="to-test-a-manually-created-custom-start-page"></a>手動で作成されたカスタムスタートページをテストするには

1. XAML ファイルと、サポートするテキストファイルまたはマークアップファイルを *%USERPROFILE%\My Documents\Visual Studio 2015 \ StartPages \\* フォルダーにコピーします。

2. スタートページで、Visual Studio によってインストールされていないアセンブリ内のコントロールまたは型が参照されている場合は、アセンブリをコピーし、 *{Visual studio インストールフォルダー} \Common7\IDE\PrivateAssemblies \\* に貼り付けます。

3. Visual Studio のコマンドプロンプトで、「 **devenv/rootsuffix Exp** 」と入力して、visual studio の実験用インスタンスを開きます。

4. 実験用インスタンスで、[**ツール**  >  **] [オプション]**[環境] [  >    >  **スタートアップ**] ページにアクセスし、[**スタートページのカスタマイズ**] ドロップダウンから XAML ファイルを選択します。

5. **[表示]** メニューの **[スタート ページ]** をクリックします。

     カスタムスタートページが表示されます。 ファイルを変更する場合は、実験用インスタンスを閉じて変更を加え、変更されたファイルをコピーして貼り付けてから、実験用インスタンスを再度開いて変更内容を表示する必要があります。

### <a name="to-apply-the-custom-start-page-in-the-primary-instance-of-visual-studio"></a>Visual Studio のプライマリインスタンスにカスタムスタートページを適用するには

- スタートページをテストし、安定していることがわかったら、[**オプション**] ダイアログボックスの [**スタートページのカスタマイズ**] オプションを使用して、Visual Studio のプライマリインスタンスのスタートページとして選択します。

## <a name="see-also"></a>関連項目

- [チュートリアル: スタートページへのカスタム XAML の追加](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
- [スタートページにユーザーコントロールを追加する](../extensibility/adding-user-control-to-the-start-page.md)
- [スタートページへの Visual Studio コマンドの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
- [チュートリアル: スタートページにユーザー設定を保存する](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)
- [カスタムスタートページのデプロイ](../extensibility/deploying-custom-start-pages.md)
