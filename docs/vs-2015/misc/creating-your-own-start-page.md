---
title: 独自のスタートページを作成する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: devlang-csharp
ms.topic: conceptual
helpviewer_keywords:
- Create start page
- custom start page
- customize start page
ms.assetid: a0df5b9c-0932-4e54-86f0-28530ad9d684
caps.latest.revision: 22
manager: jillfra
ms.openlocfilehash: fba7f1e0801b6f977d47b13af025538f5d2fe031
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75850989"
---
# <a name="creating-your-own-start-page"></a>ユーザー独自のスタート ページの作成
スタート ページのプロジェクト テンプレートを使用するか、または空白のスタート ページを作成することで、カスタム スタート ページを作成できます。  
  
 XAML デザイナーは、Visual Studio のアプリケーション モデルに依存するため、カスタム スタート ページの完全に正確な視覚的表現ができない場合があります。  
  
## <a name="using-the-project-template"></a>プロジェクト テンプレートの使用  
 スタート ページのプロジェクト テンプレートにより、Visual Studio のスタート ページの完全なコピーであるスタート ページ プロジェクトが作成されます。 その後、指定どおりにスタート ページを編集できます。  
  
#### <a name="to-create-a-custom-start-page-by-using-the-start-page-project-template"></a>スタート ページのプロジェクト テンプレートを使用してカスタム スタート ページを作成するには  
  
1. Visual Studio ギャラリーから [スタート ページのプロジェクト テンプレート](https://visualstudiogallery.msdn.microsoft.com/f655a5dc-1a2d-4eca-b774-76c352c03b87) をダウンロードしてインストールします。  
  
    > [!WARNING]
    > この時点では、Visual Studio 2010 のスタート ページのプロジェクト テンプレートはアップグレードされていません。 このテンプレートをアップグレードする方法の詳細については、「 [方法: Visual Studio のカスタムスタートページをアップグレード](../misc/how-to-upgrade-a-visual-studio-custom-start-page.md)する」を参照してください。  
  
2. テンプレートをインストールした後、それを使用して新しいスタート ページ プロジェクトを作成します。  
  
3. [新しいプロジェクト] ダイアログ ボックスの左ウィンドウで、 **[インストールされたテンプレート]** の下の **[その他のプロジェクトの種類]** ノードを展開し、 **[機能拡張]** をクリックします。  
  
4. 中央のウィンドウで、 **[カスタム スタート ページ]** をクリックし、プロジェクトに名前を付けて **[OK]** をクリックします。  
  
     Visual Studio により、Visual Studio のスタート ページの完全なコピーであるスタート ページ プロジェクトが作成されます。  
  
5. **ソリューション エクスプローラー**で、 **StartPage.xaml**を開きます。  
  
6. StartPage.xaml を編集します。  
  
     F5 キーを押してカスタム スタート ページがインストールされている Visual Studio の実験用インスタンスを開いて、作業内容を表示できます。  
  
## <a name="creating-a-blank-start-page"></a>空白のスタート ページの作成  
 空白のスタート ページを作成する最も簡単な方法は、スタート ページのプロジェクト テンプレートを使用してコンテンツを削除することです。  
  
#### <a name="to-create-a-blank-start-page-by-using-the-start-page-project-template"></a>スタート ページのプロジェクト テンプレートを使用して空白のスタート ページを作成するには  
  
1. 前の手順で説明したように、スタート ページのプロジェクト テンプレートを使用して、スタート ページ プロジェクトを作成します。  
  
2. StartPage.xaml を開きます。  
  
3. 外側の xml 要素と含まれているグリッドの <xref:System.Windows.Controls.Grid> 要素を残し、.xaml ファイルが次の例のようになるようにページのコンテンツをすべて削除します。  
  
   ```xaml
      <Grid xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
                xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006" 
                xmlns:d="http://schemas.microsoft.com/expression/blend/2008" 
                xmlns:sp="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.StartPage"
                xmlns:vs="clr-namespace:Microsoft.VisualStudio.PlatformUI;assembly=Microsoft.VisualStudio.Shell.10.0"
                xmlns:vsfx="clr-namespace:Microsoft.VisualStudio.Shell;assembly=Microsoft.VisualStudio.Shell.10.0"
            mc:Ignorable="d" 
                d:DesignHeight="600" d:DesignWidth="800">
       <Grid>
           <!--Add content here.-->
       </Grid>
   </Grid>
   ```
      
4. 使用しないサポート ファイルを削除します。  
  
    配置する .vsix ファイルと .pkgdef ファイルは残してください。  
  
   または、Visual Studio によって認識される適切なタグ構造を持つ XAML ファイルを作成することで、空白のスタート ページを作成することもできます。 その後、マークアップと分離コードを追加して、必要な外観と機能を取得できます。 詳細については、「 [カスタムスタートページの作成](../extensibility/creating-a-custom-start-page.md)」を参照してください。  
  
## <a name="testing-and-applying-the-custom-start-page"></a>カスタム スタート ページのテストと適用  
 クラッシュしないことを確認するまでは、プライマリ インスタンスを設定してカスタム スタート ページを実行しないでください。 テストしたカスタム スタート ページは、Visual Studio のプライマリ インスタンスでこの手順の最後の 3 つの手順を繰り返して、システムに適用できます。  
  
#### <a name="to-test-a-custom-start-page"></a>カスタム スタート ページをテストするには  
  
1. F5 キーを押す。  
  
    Visual Studio の実験用インスタンスが開きます。新しいスタート ページがインストールされていますが、選択されていません。  
  
2. Visual Studio の実験用インスタンスで、 **[ツール]** メニューの **[オプション]** をクリックします。  
  
3. **[オプション]** ダイアログ ボックスで、 **[環境]** の下の **[スタートアップ]** を選択します。 次に、 **[スタート ページのカスタマイズ]** ボックスの一覧で、.xaml ファイルを選択して **[OK]** をクリックします。  
  
4. **[表示]** メニューの **[スタート ページ]** をクリックします。  
  
    作業中のスタート ページが表示されます。 実験用インスタンスを閉じて変更したファイルを再度コピーし、実験用インスタンスを再度開いて新しい変更を確認します。  
  
   カスタムスタートページを共有するには、bin\debug ディレクトリから [Visual Studio Marketplace](https://marketplace.visualstudio.com/) web サイト、または別の web サイトまたはイントラネット共有に .vsix ファイルをアップロードします。 詳細については、「 [Deploying Custom Start Pages](../extensibility/deploying-custom-start-pages.md)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [スタートページのカスタマイズ](../ide/customizing-the-start-page-for-visual-studio.md)   
 [チュートリアル: カスタム XAML をスタート ページに追加する](../extensibility/walkthrough-adding-custom-xaml-to-the-start-page.md)
