---
title: ツールバーの追加 |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- toolbars [Visual Studio], adding to IDE
- IDE, adding toolbars
ms.assetid: 17302c25-6f59-4e97-8c85-54f95336a07f
caps.latest.revision: 39
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: 038b8e8503a89dd0ec565d3d1b5acf20e6437600
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51787953"
---
# <a name="adding-a-toolbar"></a>ツール バーの追加
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このチュートリアルでは、Visual Studio IDE にツールバーを追加する方法を示します。  
  
 ツールバーは、水平方向または垂直方向のストリップで、コマンドにバインドされているボタンが含まれています。 実装によって IDE でツールバーの位置を変更、IDE のメイン ウィンドウの任意の辺にドッキングしたり他のウィンドウの前に常に加えられました。  
  
 ユーザーがさらに、ツールバーにコマンドを追加またはを使用してから、削除、**カスタマイズ** ダイアログ ボックス。 通常、Vspackage では、ツールバーは、ユーザーがカスタマイズできます。 IDE がカスタマイズをすべてを処理し、VSPackage がコマンドに応答します。 VSPackage は、コマンドが物理的に配置されている場所を認識する必要はありません。  
  
 メニューの詳細については、次を参照してください。[コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)します。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 Visual Studio 2015 以降、ダウンロード センターから Visual Studio SDK をインストールすることはできません。 これは Visual Studio のセットアップにオプション機能として含まれるようになりました。 また、後から VS SDK をインストールすることもできます。 より詳細な情報については 、[Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md) に関する記事を参照してください。  
  
## <a name="creating-an-extension-with-a-toolbar"></a>ツールバーと拡張機能の作成  
 という名前の VSIX プロジェクトを作成する`IDEToolbar`します。 という名前のメニュー コマンド項目テンプレートを追加**ToolbarTestCommand**します。 これを行う方法については、次を参照してください。[メニュー コマンドを使用して拡張機能の作成](../extensibility/creating-an-extension-with-a-menu-command.md)です。  
  
## <a name="creating-a-toolbar-for-the-ide"></a>IDE のツールバーの作成  
  
1.  ToolbarTestCommandPackage.vsct の Symbols セクションを探します。 GuidToolbarTestCommandPackageCmdSet をという名前の GuidSymbol 要素では、次のようにツールバーとツールバー、グループの宣言を追加します。  
  
    ```xml  
    <IDSymbol name="Toolbar" value="0x1000" />  
    <IDSymbol name="ToolbarGroup" value="0x1050" />  
  
    ```  
  
2.  コマンドのセクションの上部にあるメニューのセクションを作成します。 メニュー セクションで、ツールバーを定義するには、メニュー要素を追加します。  
  
    ```xml  
    <Menus>  
        <Menu guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"  
            type="Toolbar" >  
            <CommandFlag>DefaultDocked</CommandFlag>  
            <Strings>  
                <ButtonText>Test Toolbar</ButtonText>  
                <CommandName>Test Toolbar</CommandName>  
            </Strings>  
          </Menu>  
    </Menus>  
    ```  
  
     ツールバーは、サブメニューのような入れ子にすることはできません。 そのため、親グループを割り当てるにはありません。 またがありません、優先順位を設定するため、ユーザーがツールバーを移動できます。 通常、ツールバーの初期配置がプログラムで定義されているが、ユーザーがそれ以降の変更が保存されます。  
  
3.  [グループ](../extensibility/groups-element.md)セクションでは、既存のグループ エントリの後に定義、[グループ](../extensibility/group-element.md)ツールバーのコマンドを格納する要素。  
  
    ```xml  
    <Group guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup"  
          priority="0x0000">  
      <Parent guid="guidToolbarTestCommandPackageCmdSet" id="Toolbar"/>  
    </Group>  
    ```  
  
4.  ツールバーの表示 ボタンを作成します。 [ボタン] セクションで、ツールバーにボタンの親ブロックに置き換えます。 結果として得られるボタン ブロックは、このようになります。  
  
    ```xml  
    <Button guid="guidToolbarTestCommandPackageCmdSet" id="ToolbarTestCommandId" priority="0x0100" type="Button">  
        <Parent guid= "guidToolbarTestCommandPackageCmdSet" id="ToolbarGroup" />  
                <Icon guid="guidImages" id="bmpPic1" />  
        <Strings>  
            <ButtonText>Invoke ToolbarTestCommand</ButtonText>  
        </Strings>  
    </Button>  
    ```  
  
     既定では、ツールバーにコマンドが存在しない場合に表示されません。  
  
5.  プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスが表示されます。  
  
6.  ツールバーの一覧を取得する Visual Studio のメニュー バーを右クリックします。 選択**テスト ツールバー**します。  
  
7.  ファイル アイコンには、検索の右側にアイコンとして、ツールバーがわかります。 示すメッセージ ボックスが表示アイコンをクリックすると**ToolbarTestCommandPackage します。IDEToolbar.ToolbarTestCommand.MenuItemCallback() 内**します。  
  
## <a name="see-also"></a>関連項目  
 [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)

