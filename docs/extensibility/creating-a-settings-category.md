---
title: 設定カテゴリを作成する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profile settings, creating categories
ms.assetid: 97c88693-05ff-499e-8c43-352ee073dcb7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 5f4b2fa9d82181d0eb899bf9680e8a9debd6c50b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739610"
---
# <a name="create-a-settings-category"></a>設定カテゴリを作成する

このチュートリアルでは、Visual Studio の設定カテゴリを作成し、設定ファイルに値を保存し、設定ファイルから値を復元するために使用します。 設定カテゴリは、「カスタム設定ポイント」として表示される関連プロパティのグループです。つまり、**設定のインポートとエクスポート**ウィザードのチェック ボックスとして使用します。 (**ツール**メニューで確認できます)。設定はカテゴリとして保存または復元され、個々の設定はウィザードに表示されません。 詳細については、[環境設定](../ide/environment-settings.md)に関するページを参照してください。

設定カテゴリは、クラスから派生して作成します<xref:Microsoft.VisualStudio.Shell.DialogPage>。

このチュートリアルを開始するには、まず[「オプション ページの作成](../extensibility/creating-an-options-page.md)」の最初のセクションを完了する必要があります。 結果の [オプション] プロパティ グリッドを使用すると、カテゴリのプロパティを確認および変更できます。 設定ファイルにプロパティ カテゴリを保存した後、ファイルを調べて、プロパティ値がどのように格納されているかを確認します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

## <a name="create-a-settings-category"></a>設定カテゴリを作成する
 このセクションでは、カスタム設定ポイントを使用して、設定カテゴリの値を保存および復元します。

### <a name="to-create-a-settings-category"></a>設定カテゴリを作成するには

1. [[オプションの作成] ページに入力](../extensibility/creating-an-options-page.md)します。

2. *VSPackage.resx*ファイルを開き、次の 3 つの文字列リソースを追加します。

    |名前|[値]|
    |----------|-----------|
    |106|マイカテゴリ|
    |107|[個人の設定]|
    |108|オプション整数とオプションフロート|

     これにより、カテゴリ "マイ カテゴリ" 、オブジェクト "My Settings" 、およびカテゴリの説明 "OptionInteger と OptionFloat" という名前のリソースが作成されます。

    > [!NOTE]
    > これら 3 つのうち、**設定のインポートとエクスポート**ウィザードにはカテゴリ名だけが表示されません。

3. *MyToolsOptionsPackage.cs*で、次の`float`例に`OptionFloat`示すように`OptionPageGrid`、クラスに名前を付けたプロパティを追加します。

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
    > "My Category" という名前のカテゴリは`OptionPageGrid`、2`OptionInteger`つの`OptionFloat`プロパティと で構成されます。

4. クラスに<xref:Microsoft.VisualStudio.Shell.ProvideProfileAttribute>a`MyToolsOptionsPackage`を追加し、カテゴリ名 "マイ カテゴリ" を指定し、そのクラスに "マイ設定" というオブジェクト名を付けて、isToolsOptionPage を true に設定します。 カテゴリリソース ID、オブジェクト名リソース ID、および説明リソース ID を、以前に作成された対応する文字列リソース ID に設定します。

    ```csharp
    [ProvideProfileAttribute(typeof(OptionPageGrid),
        "My Category", "My Settings", 106, 107, isToolsOptionPage:true, DescriptionResourceID = 108)]
    ```

5. プロジェクトをビルドし、デバッグを開始します。 実験用のインスタンスでは **、My Grid Page**に整数と浮動小数点値の両方が含まれていることがわかります。

## <a name="examine-the-settings-file"></a>設定ファイルを確認する
 このセクションでは、プロパティ カテゴリ値を設定ファイルにエクスポートします。 ファイルを調べてから、プロパティ カテゴリに値をインポートします。

1. **F5**キーを押して、プロジェクトをデバッグ モードで起動します。 実験インスタンスが開始されます。

2. [**ツール** > **オプション]** ダイアログ を開きます。

3. 左側のウィンドウのツリー ビューで、[**マイ カテゴリ]** を展開し、[**マイ グリッド ページ**] をクリックします。

4. **オプションフロート**の値を 3.1416 に変更し、**オプション整数**を 12 に変更します。 **[OK]** をクリックします。

5. **[ツール]** メニューの **[設定のインポートとエクスポート]** を選択します。

     **設定のインポートとエクスポート**ウィザードが表示されます。

6. [**選択した環境設定をエクスポートする]** が選択されていることを確認し、[**次へ**] をクリックします。

     [**エクスポートする設定の選択]** ページが表示されます。

7. [**マイ設定]** をクリックします。

     **説明**が **[オプション整数] と [オプションフロート]** に変わります。

8. [**個人用設定]** が選択されている唯一のカテゴリであることを確認し、[**次へ**] をクリックします。

     [**設定ファイルの名前]** ページが表示されます。

9. 新しい設定ファイルに*MySettings.vssettings*という名前を付け、適切なディレクトリに保存します。 **[完了]** をクリックします。

     [**エクスポートの完了]** ページには、設定が正常にエクスポートされたことを報告します。

10. **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** をクリックします。 *マイ設定.vssettings を*見つけて開きます。

     エクスポートしたプロパティ カテゴリは、ファイルの次のセクションで確認できます (GUID は異なります)。

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

     カテゴリ名にアンダースコアを追加し、その後にオブジェクト名を付けて、完全なカテゴリ名を形成することに注意してください。 オプションフロートとオプション整数は、エクスポートされた値と共にカテゴリに表示されます。

11. 設定ファイルを変更せずに閉じます。

12. [**ツール**] メニュー**OptionInteger**の [**オプション**] をクリックし、[**マイ カテゴリ****]** を展開**OptionFloat**します。 **[OK]** をクリックします。

13. [**ツール**] メニューの [**設定のインポートとエクスポート**] をクリックし、[**選択した環境設定のインポート**]**をクリックします**。

     [**現在の設定を保存]** ページが表示されます。

14. [**いいえ、新しい設定をインポートする] を**選択し、[**次へ**] をクリックします。

     [**インポートする設定のコレクションを選択]** ページが表示されます。

15. ツリービューの *[マイ設定]ノードで[MySettings.vssettings]* ファイルを選択します。 **My Settings** ファイルがツリービューに表示されない場合は、[参照]をクリック**して**検索します。 **[次へ]** をクリックします。

     [**インポートする設定の選択]** ダイアログ ボックスが表示されます。

16. **[マイ設定]** が選択されていることを確認し、[**完了**] をクリックします。 [**インポートの完了]** ページが表示されたら、[**閉じる**] をクリックします。

17. [**ツール**] メニューの **[オプション]** をクリックし、[**マイ カテゴリ**] を展開**します**。
