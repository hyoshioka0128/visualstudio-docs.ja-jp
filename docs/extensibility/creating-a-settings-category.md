---
title: 設定カテゴリの作成 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- profile settings, creating categories
ms.assetid: 97c88693-05ff-499e-8c43-352ee073dcb7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 03d50ca998efa034b1d4392c1fb7cecb8de8ed06
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85904026"
---
# <a name="create-a-settings-category"></a>設定カテゴリの作成

このチュートリアルでは、Visual Studio の設定カテゴリを作成し、それを使用して設定ファイルに値を保存し、値を復元します。 設定カテゴリは、"カスタム設定ポイント" として表示される関連プロパティのグループです。これは、 **設定のインポートおよびエクスポート** ウィザードのチェックボックスとしてです。 ([ **ツール** ] メニューで見つけることができます)。設定はカテゴリとして保存または復元され、個々の設定はウィザードに表示されません。 詳細については、[環境設定](../ide/environment-settings.md)に関するページを参照してください。

設定カテゴリは、クラスから派生させることによって作成し <xref:Microsoft.VisualStudio.Shell.DialogPage> ます。

このチュートリアルを開始するには、まず、[オプションの [作成] ページ](../extensibility/creating-an-options-page.md)の最初のセクションを完了する必要があります。 結果のオプションのプロパティグリッドを使用して、カテゴリ内のプロパティを確認および変更できます。 プロパティカテゴリを設定ファイルに保存した後、ファイルを調べて、プロパティ値がどのように格納されているかを確認します。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-settings-category"></a>設定カテゴリの作成
 このセクションでは、カスタム設定ポイントを使用して、[設定] カテゴリの値を保存し、復元します。

### <a name="to-create-a-settings-category"></a>設定カテゴリを作成するには

1. [ [オプションの作成] ページ](../extensibility/creating-an-options-page.md)に入力します。

2. *VSPackage*ファイルを開き、次の3つの文字列リソースを追加します。

    |名前|値|
    |----------|-----------|
    |106|マイカテゴリ|
    |107|[個人の設定]|
    |108|オプション Integer とオプション Float|

     これにより、カテゴリに "My Category" という名前のリソース、オブジェクト "My Settings"、および "OptionInteger と Optioninteger" というカテゴリの説明が作成されます。

    > [!NOTE]
    > これら3つのうち、カテゴリ名だけが、設定の **インポートおよびエクスポート** ウィザードに表示されません。

3. *MyToolsOptionsPackage.cs*で、次の `float` `OptionFloat` 例に示すように、という名前のプロパティをクラスに追加し `OptionPageGrid` ます。

    ```csharp
    public class OptionPageGrid : DialogPage
    {
        private int optionInt = 256;
        private float optionFloat = 3.14F;

        [Category("My Options")]
        [DisplayName("My Integer option")]
        [Description("My integer option")]
        public int OptionInteger
        {
            get { return optionInt; }
            set { optionInt = value; }
        }
        [Category("My Options")]
        [DisplayName("My Float option")]
        [Description("My float option")]
        public float OptionFloat
        {
            get { return optionFloat; }
            set { optionFloat = value; }
        }
    }
    ```

    > [!NOTE]
    > `OptionPageGrid`"My category" という名前のカテゴリは、とという2つのプロパティで構成されるようになりました `OptionInteger` `OptionFloat` 。

4. を <xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute> クラスに追加 `MyToolsOptionsPackage` し、"my Category" というカテゴリ名を付けて、ObjectName に "my Settings" を指定し、isToolsOptionPage を true に設定します。 カテゴリ Resourceid、objectNameResourceID、および DescriptionResourceID を、前に作成した対応する文字列リソース Id に設定します。

    ```csharp
    [ProvideProfileAttribute(typeof(OptionPageGrid),
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]
    ```

5. プロジェクトをビルドし、デバッグを開始します。 実験用インスタンスでは、 **グリッドページ** に整数値と浮動小数点値の両方が指定されていることがわかります。

## <a name="examine-the-settings-file"></a>設定ファイルを確認する
 このセクションでは、プロパティカテゴリの値を設定ファイルにエクスポートします。 ファイルを調べてから、プロパティカテゴリに値をインポートします。

1. **F5**キーを押して、プロジェクトをデバッグモードで起動します。 これにより、実験用インスタンスが開始されます。

2. [**ツール**  >  **オプション**] ダイアログを開きます。

3. 左側のウィンドウのツリービューで、[ **My Category** ] を展開し、[ **my Grid Page**] をクリックします。

4. **Optionfloat**の値を3.1416 に、**オプション integer**を12に変更します。 **[OK]** をクリックします。

5. **[ツール]** メニューの **[設定のインポートとエクスポート]** を選択します。

     **設定のインポートとエクスポート**ウィザードが表示されます。

6. [ **選択した環境設定のエクスポート** ] が選択されていることを確認し、[ **次へ**] をクリックします。

     [ **エクスポートする設定の選択]** ページが表示されます。

7. [ **個人用設定**] をクリックします。

     **説明**は、 **Optioninteger と optioninteger**に変わります。

8. [ **個人用設定** ] が選択されている唯一のカテゴリであることを確認し、[ **次へ**] をクリックします。

     [ **設定ファイルの名前** ] ページが表示されます。

9. 新しい設定ファイルに「 *Mysettings. .vssettings* 」という名前を付け、適切なディレクトリに保存します。 **[完了]** をクリックします。

     [ **エクスポートの完了** ] ページには、設定が正常にエクスポートされたことが表示されます。

10. **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。 「 *Mysettings. .vssettings* 」に移動して開きます。

     エクスポートしたプロパティカテゴリは、ファイルの次のセクションで確認できます (Guid は異なります)。

    ```
    <Category name="My Category_My Settings"
          Category="{4802bc3e-3d9d-4591-8201-23d1a05216a6}"
          Package="{6bb6942e-014c-489e-a612-a935680f703d}"
          RegisteredName="My Category_My Settings">
          PackageName="MyToolsOptionsPackage">
       <PropertyValue name="OptionFloat">3.1416</PropertyValue>
       <PropertyValue name="OptionInteger">12</PropertyValue>
    </Category>
    ```

     カテゴリ名の後にオブジェクト名が続くアンダースコアを追加することによって、完全なカテゴリ名が形成されていることに注意してください。 オプション Float と Optionfloat は、エクスポートされた値と共にカテゴリに表示されます。

11. 設定ファイルを変更せずに閉じます。

12. [ **ツール** ] メニューの [ **オプション**] をクリックし、[ **個人用カテゴリ**] を展開して、[ **マイグリッドページ** ] をクリックします。次に、[オプション **] の値を1.0 に変更** し、[オプションの **整数** ] を1に変更します。 **[OK]** をクリックします。

13. [ **ツール** ] メニューの [ **設定のインポートとエクスポート**] をクリックし、[ **選択した環境設定のインポート**] を選択して、[ **次へ**] をクリックします。

     [ **現在の設定の保存** ] ページが表示されます。

14. [ **いいえ、新しい設定をインポート** します] を選択し、[ **次へ**] をクリックします。

     [ **インポートする設定のコレクションを選択** ] ページが表示されます。

15. ツリービューの **[マイ設定**] ノードで、 *mysettings の .vssettings*ファイルを選択します。 ファイルがツリービューに表示されない場合は、[ **参照** ] をクリックして検索します。 **[次へ]** をクリックします。

     [ **インポートする設定の選択** ] ダイアログボックスが表示されます。

16. [ **マイ設定** ] が選択されていることを確認し、[ **完了**] をクリックします。 [ **インポートが完了** しました] ページが表示されたら、[ **閉じる**] をクリックします。

17. [ **ツール** ] メニューの [ **オプション**] をクリックし、[ **個人用カテゴリ**] を展開し、[ **マイグリッドページ** ] をクリックして、プロパティカテゴリの値が復元されていることを確認します。
