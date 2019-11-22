---
title: Define a custom modeling toolbox item | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- UML - extending, customizing the toolbox
ms.assetid: a2463606-1100-40ac-97f3-5ba22ca47b7c
caps.latest.revision: 33
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: ac299f18e544ef4f3215707abbdc3d9e8d266de6
ms.sourcegitcommit: bad28e99214cf62cfbd1222e8cb5ded1997d7ff0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/21/2019
ms.locfileid: "74299296"
---
# <a name="define-a-custom-modeling-toolbox-item"></a>カスタム モデリング ツールボックス アイテムを定義する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

頻繁に使用するパターンを使って簡単に要素または要素グループを作成するために、Visual Studio のモデリング図のツールボックスに新しいツールを追加することができます。 これらのツールボックス アイテムは、Visual Studio の他のユーザーに配布することができます。

 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。

 カスタム ツールは、図の中に 1 つまたは複数の新しい要素を作成します。 例えば、次のような要素を作成するカスタム ツールを作成できます。

- .NET プロファイルにリンクされたパッケージと、.NET のステレオタイプを持つクラス。

- オブザーバー パターンを表す関連付けによってリンクされたクラスのペア。

> [!NOTE]
> このメソッドを使用して、要素ツールを作成することができます。 つまり、ツールボックスから図にドラッグするツールを作成できます。 コネクタ ツールは作成できません。

## <a name="DefineTool"></a> Defining a Custom Modeling Tool

#### <a name="to-define-a-custom-modeling-tool"></a>カスタム モデリング ツールを定義するには

1. 要素または要素グループを含んだ UML 図を作成します。

    - これらの要素の間にはリレーションシップを設定できます。また、要素は、ポート、属性、操作またはピンなどの付属の要素を持つこともできます。

2. 新しいツールにつける名前で図を保存します。 On the **File** menu, use **Save…As**.

3. Windows エクスプローラーを使用して、2 つの図ファイルを次のフォルダーまたはその下の任意のサブフォルダーにコピーします。

     *YourDocuments* **\Visual Studio\Architecture Tools\Custom Toolbox Items**

    - このフォルダがまだ存在しない場合は作成します。 You might have to create both **Architecture Tools** and **Custom Toolbox Items**.

    - Copy both diagram files, one with a name that ends "…**diagram**" and the other with a name that ends "…**diagram.layout**"

    - カスタム ツールは必要に応じていくつでも作成できます。 各ツールに 1 つの図を使用します。

4. (Optional) Create a **.tbxinfo** file as described in [How to Define the Properties of Custom Tools](#tbxinfo), and add it to the same directory. これによって、ツールボックス アイコンやヒントなどを定義することができます。

    - A single **.tbxinfo** file can be used to define several tools. これは、サブフォルダーにある複数の図ファイルを参照できます。

5. Visual Studio を再起動します。 ツールボックスにそれぞれの図の型に対応する追加のツールが表示されます。

### <a name="what-the-custom-tool-will-replicate"></a>カスタム ツールのレプリケート対象
 カスタム ツールは、元の図のほとんどの機能をレプリケートします。

- 名前。 ツールボックスから項目が作成されると、同じ名前空間で名前が重複することを回避するために、必要に応じて名前の末尾に数値が追加されます。

- 色、サイズ、および図形

- ステレオタイプおよびパッケージ プロファイル

- Is Abstract などのプロパティ値

- リンクされた作業項目

- リレーションシップの多重度と他のプロパティ

- 図形の相対位置。

  次の機能は、カスタム ツールでは保存されません。

- 単純な図形。 これらはモデル要素に関連しない、一部の種類の図に描画できる図形のことです。

- コネクタのルーティング。 コネクタを手動でルーティングする場合、ツールを使用するとルーティングは保持されません。 ポートなどの入れ子になった一部の図形の位置は、その所有者に関連して保持されることはありません。

## <a name="tbxinfo"></a> How to Define the Properties of Custom Tools
 A toolbox information ( **.tbxinfo**) file allows you to specify a toolbox name, icon, tooltip, tab, and help keyword for one or more custom tools. Give it any name, such as **MyTools.tbxinfo**.

 一般的なファイル形式は、次のとおりです。

```
<?xml version="1.0" encoding="utf-8" ?>
<customToolboxItems xmlns="http://schemas.microsoft.com/visualstudio/[version]/ArchitectureTools/CustomToolboxItems">
  <customToolboxItem fileName="MyObserverTool.classdiagram">
    <displayName>
       <value>Observer Pattern</value>
    </displayName>
    <tabName>
       <value>UML Class Diagram</value>
    </tabName>
    <image><bmp fileName="ObserverPatternIcon.bmp"/></image>
    <f1Keyword>
      <value>ObserverPatternHelp</value>
    </f1Keyword>
    <tooltip>
       <value>Create a pair of classes</value>
    </tooltip>
  </customToolboxItem>
</customToolboxItems>
```

 各アイテムの値は、次のいずれかになります。

- この例で示すように、ツールボックス アイコンでは `<bmp fileName="…"/>` で、その他のアイテムでは `<value>string</value>` です。

  \- または

- `<resource fileName="Resources.dll"`

   `baseName="Observer.resources" id="Observer.tabname" />`

   この場合は、文字列値がリソースとしてコンパイルされている、コンパイル済みのアセンブリを指定します。

  定義するツールボックス アイテムごとに `<customToolboxItem>` ノードを追加します。

  The nodes in the **.tbxinfo** file are as follows. 各ノードには、既定値が設定されています。

|ノード名|定義|
|---------------|-------------|
|displayName|ツールボックス アイテムの名前。|
|tabName|アイテムが表示されるツールボックス タブ。 この種類の図の標準タブの名前か、別の名前を指定できます。|
|イメージ|The location of the bitmap ( **.bmp**) file, which must have height and width of 16, and a color depth of 24 bits.|
|f1Keyword|ヘルプ トピックを検索するキーワードです。|
|ヒント|このツールのヒントです。|

 Visual Studio でビットマップ ファイルを編集して、[プロパティ] ウィンドウで高さと幅を 16 に設定できます。

> [!NOTE]
> 図ファイルを単独で使用して試した後に .tbxinfo ファイルを使用し始めた場合、ツールボックスには、ツールボックス アイテムの古いバージョンと新しいバージョンの両方が含まれる場合があります。 これは、.tbxinfo ファイルで図ファイルの名前が間違っている場合にも発生します。 If this occurs, on the shortcut menu of the toolbox choose **Reset Toolbox**. カスタム ツールボックス アイテムが表示されなくなります。 Visual Studio を再起動すると、正しいカスタム アイテムが表示されます。

## <a name="Extension"></a> How to Distribute Toolbox Items in a Visual Studio Extension
 You can distribute toolbox items to other [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] users by packaging them into a Visual Studio Extension (VSIX). コマンド、プロファイルなどの拡張機能を同じ VSIX ファイルにパッケージ化できます。 For more information, see [Deploying Visual Studio Extensions](https://go.microsoft.com/fwlink/?LinkId=160780).

 Visual Studio 拡張機能をビルドするには、通常は VSIX プロジェクトのテンプレートを使用します。 これを行うには、[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] をインストールしておく必要があります。

#### <a name="to-add-a-toolbox-item-to-a-visual-studio-extension"></a>ツールボックス アイテムを Visual Studio 拡張機能に追加するには

1. [Create and test one or more custom tools](#DefineTool).

2. [Create a .tbxinfo file](#tbxinfo) that references the tools.

3. 既存の Visual Studio 拡張機能プロジェクトを開きます。

     \- または

     新しい Visual Studio 拡張機能プロジェクトを定義します。

    1. **[ファイル]** メニューで、 **[新規]** 、 **[プロジェクト]** をクリックします。

    2. In the **New Project** dialog box, under **Installed Templates**, choose **Visual C#** , **Extensibility**, **VSIX project**.

4. プロジェクトにツールボックスの定義を追加します。 Include the **.tbxinfo** file, the diagram files, bitmap files, and any resource files, and make sure that they are included in the VSIX.

    - In Solution Explorer, on the shortcut menu of the VSIX project, choose **Add**, **Existing Item**. In the dialog box, set **Objects of Type: All Files**. Locate the files, select them all, and then choose **Add**.

        > [!NOTE]
        > このプロジェクトでは、図ファイルをモデル エディターで開くことができません。

5. ここで追加したすべてのファイルについて次のプロパティを設定します。 ソリューション エクスプローラーでそれらすべてを選択すると、それらのプロパティを同時に設定できます。 プロジェクト内の他のファイルのプロパティを変更しないように注意してください。

     **Copy to Output Directory** = **Copy Always**

     **Build Action** = **Content**

     **Include in VSIX** = **true**

6. **source.extension.vsixmanifest**を開きます。 このファイルは拡張機能マニフェスト エディターで開きます。

7. Under **Metadata**, add a description for the custom tools.

     Under **Assets**, choose **New** and then set the fields in the dialog as follows:

    - **Type** = **Custom Extension Type**

    - 種類 = `Microsoft.VisualStudio.ArchitectureTools.CustomToolboxItems`

        > [!NOTE]
        > これは、ドロップダウン リストのオプションの 1 つではありません。 キーボードを使用して入力する必要があります。

    - **Source** = **File on filesystem**.

    - **Path** = your **.tbxinfo** file, for example **MyTools.tbxinfo**

8. プロジェクトをビルドします。

9. **To verify that the extension works**, press F5. Visual Studio の実験用インスタンスが開始します。

     実験用のインスタンスで、関連する型の UML 図を作成するか開きます。 新しいツールがツールボックスに表示されることと、正しく要素が作成されることを確認します。

10. **To obtain a VSIX file for deployment:** In Windows Explorer, open the folder **.\bin\Debug** or **.\bin\Release** to find the **.vsix** file. これは [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 拡張ファイルです。 このファイルは、自分のコンピューターにインストールできるほか、他の Visual Studio ユーザーに送信することもできます。

#### <a name="to-install-custom-tools-from-a-visual-studio-extension"></a>Visual Studio 拡張機能からカスタム ツールをインストールするには

1. Windows エクスプローラーまたは Visual Studio で `.vsix` ファイルを開きます。

2. Choose **Install** in the dialog box that appears.

3. To uninstall or temporarily disable the extension, open **Extensions and Updates** from the **Tools** menu.

## <a name="localization"></a>ローカリゼーション
 拡張機能が別のコンピューターにインストールされるとターゲット コンピューターの言語でツールの名前やヒントが表示されるように設定できます。

#### <a name="to-provide-versions-of-the-tool-in-more-than-one-language"></a>複数の言語のバージョンのツールを提供するには

1. 1 つ以上のカスタム ツールを含んだ Visual Studio 拡張機能プロジェクトを作成します。

    In the **.tbxinfo** file, use the resource file method to define the tool's `displayName`, toolbox `tabName`, and the tooltip. これらの文字列が定義されているリソース ファイルを作成してアセンブリにコンパイルし、tbxinfo ファイルからそれを参照します。

2. 他の言語の文字列のリソース ファイルが含まれている追加のアセンブリを作成します。

3. 言語のカルチャ コードを名前にしたフォルダーに、追加のアセンブリをそれぞれ配置します。 For example, place a French version of the assembly inside a folder that is named **fr**.

4. `fr-CA` のような特定カルチャではなく、通常 2 つの文字で構成されるニュートラル カルチャ コードを使用する必要があります。 For more information about culture codes, see [CultureInfo.GetCultures method](https://go.microsoft.com/fwlink/?LinkId=160782), which provides a complete list of culture codes.

5. Visual Studio 拡張機能をビルドして配布します。

6. 拡張機能が別のコンピューターにインストールされると、ユーザーのローカル カルチャのリソース ファイルのバージョンが自動的にロードされます。 ユーザーのカルチャのバージョンをまだ提供していない場合、デフォルトのリソースが使用されます。

   この方式を使用して、プロトタイプ図のさまざまなバージョンをインストールすることはできません。 要素とコネクタの名前は、どのインストールでも同じになります。

## <a name="other-toolbox-operations"></a>その他のツールボックスの操作
 通常、[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] では、ツールの名前を変更したり、別のツールボックスのタブに移動したり、それらを削除したりすることで、ツールボックスをカスタマイズすることができます。 ただし、このトピックで説明した手順で作成したカスタム モデリング ツールでは、このような変更が維持されません。 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] を再起動すると、定義済みの名前とツールボックスの場所でツールボックスが再表示されます。

 Furthermore, your custom tools will disappear if you perform the **Reset Toolbox** command. しかし、[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] を再起動すると再び表示されます。

## <a name="see-also"></a>参照
 [Extend UML models and diagrams](../modeling/extend-uml-models-and-diagrams.md) [Define a profile to extend UML](../modeling/define-a-profile-to-extend-uml.md) [Define a menu command on a modeling diagram](../modeling/define-a-menu-command-on-a-modeling-diagram.md) [Define validation constraints for UML models](../modeling/define-validation-constraints-for-uml-models.md)
