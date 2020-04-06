---
title: カスタムスタートページの作成 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: d67e0c53-9f5a-45fb-a929-b9d2125c3c82
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
monikerRange: vs-2017
ms.openlocfilehash: 3ac0abfe9eedf1c03a8be3bacddbe06ff5698380
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739632"
---
# <a name="creating-a-custom-start-page"></a>カスタムスタートページの作成

このドキュメントの手順に従って、カスタムスタート ページを作成できます。

## <a name="create-a-blank-start-page"></a>空白のスタート ページを作成する

まず、Visual Studio で認識されるタグ構造を持つ *.xaml*ファイルを作成して、空白のスタート ページを作成します。 次に、マークアップと分離コードを追加して、目的の外観と機能を作成します。

1. **WPF アプリケーション****(Visual C#** > **Windows デスクトップ**) の種類の新しいプロジェクトを作成します。

2. `Microsoft.VisualStudio.Shell.14.0` への参照を追加します。

3. XML エディターで XAML ファイルを開き、名前空間宣言\<を削除せずに、トップレベル\<ウィンドウ>要素を UserControl>要素に変更します。

4. 最上位の`x:Class`要素から宣言を削除します。 これにより、XAML コンテンツは、スタート ページをホストする Visual Studio ツール ウィンドウと互換性があります。

5. 最上位の\<UserControl>要素に、次の名前空間宣言を追加します。

    ```vb
    xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.14.0"
    xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.14.0"
    ```

     これらの名前空間を使用すると、Visual Studio のコマンド、コントロール、および UI 設定にアクセスできます。 詳細については、「 [Visual Studio のコマンドをスタート ページに追加する](../extensibility/adding-visual-studio-commands-to-a-start-page.md)」を参照してください。

     空白のスタート ページの *.xaml*ファイルのマークアップを次の例に示します。 カスタム コンテンツは、内部<xref:System.Windows.Controls.Grid>要素に含める必要があります。

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

6. ユーザー\<設定のスタート ページに入力する空のユーザー コントロール>要素にコントロールを追加します。 Visual Studio に固有の機能を追加する方法については、「 [Visual Studio コマンドをスタート ページに追加する](../extensibility/adding-visual-studio-commands-to-a-start-page.md)」を参照してください。

## <a name="test-and-apply-the-custom-start-page"></a>カスタムスタートページをテストして適用する

Visual Studio がクラッシュしないことを確認するまで、カスタム スタート ページを実行するように Visual Studio のプライマリ インスタンスを設定しないでください。 代わりに、実験用インスタンスでテストします。

### <a name="to-test-a-manually-created-custom-start-page"></a>手動で作成したカスタム スタート ページをテストするには

1. XAML ファイルとサポートテキスト ファイルまたはマークアップ ファイルを *%USERPROFILE%\マイ ドキュメント\Visual Studio 2015\StartPages\\*フォルダーにコピーします。

2. Visual Studio によってインストールされていないアセンブリ内のコントロールまたは型をスタート ページが参照している場合は、アセンブリをコピーして *{Visual Studio インストール フォルダー}\Common7\IDE\PrivateAssembly\\*に貼り付けます。

3. Visual Studio のコマンド プロンプトで **、devenv /ルートサフィックス Exp と**入力して、Visual Studio の実験的なインスタンスを開きます。

4. 実験用インスタンスで、[**ツール** > **オプション** > **環境** > の**スタートアップ**] ページに移動し、[スタート**ページのカスタマイズ**] ドロップダウンから XAML ファイルを選択します。

5. **[表示]** メニューの **[スタート ページ]** をクリックします。

     カスタムスタートページが表示されます。 ファイルを変更する場合は、実験用インスタンスを閉じ、変更を加え、変更されたファイルをコピーして貼り付け、その後、実験用インスタンスを再度開いて変更を表示する必要があります。

### <a name="to-apply-the-custom-start-page-in-the-primary-instance-of-visual-studio"></a>Visual Studio のプライマリ インスタンスでカスタムスタート ページを適用するには

- スタート ページをテストして安定していることが判明したら、[**オプション]** ダイアログ ボックスの [**スタート ページのカスタマイズ**] オプションを使用して、Visual Studio のプライマリ インスタンスのスタート ページとして選択します。

## <a name="see-also"></a>関連項目

- [チュートリアル: カスタム XAML をスタート ページに追加する](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
- [スタート ページにユーザー コントロールを追加する](../extensibility/adding-user-control-to-the-start-page.md)
- [スタート ページへの Visual Studio コマンドの追加](../extensibility/adding-visual-studio-commands-to-a-start-page.md)
- [チュートリアル: スタート ページにユーザー設定を保存する](../extensibility/walkthrough-saving-user-settings-on-a-start-page.md)
- [カスタムスタート ページの展開](../extensibility/deploying-custom-start-pages.md)
