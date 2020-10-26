---
title: カスタムモデリングツールボックスアイテムを定義する |Microsoft Docs
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
ms.openlocfilehash: 0a038150519ea7a40a52fb1be16ed93045c09eed
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "75851516"
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

## <a name="defining-a-custom-modeling-tool"></a><a name="DefineTool"></a> カスタムモデリングツールの定義

#### <a name="to-define-a-custom-modeling-tool"></a>カスタム モデリング ツールを定義するには

1. 要素または要素グループを含んだ UML 図を作成します。

    - これらの要素の間にはリレーションシップを設定できます。また、要素は、ポート、属性、操作またはピンなどの付属の要素を持つこともできます。

2. 新しいツールにつける名前で図を保存します。 [ **ファイル** ] メニューの [保存] を使用します。 **として**。

3. Windows エクスプローラーを使用して、2 つの図ファイルを次のフォルダーまたはその下の任意のサブフォルダーにコピーします。

     [*ドキュメント*] **\ (Visual Studio\Architecture \) カスタムツールボックスアイテム**

    - このフォルダがまだ存在しない場合は作成します。 場合によっては、 **アーキテクチャツール** と **カスタムツールボックスアイテム**の両方を作成する必要があります。

    - 両方の図ファイルをコピーします。1つは "..." という名前で終わります。**".**.." という名前の "...**ダイアグラム。レイアウト**"

    - カスタム ツールは必要に応じていくつでも作成できます。 各ツールに 1 つの図を使用します。

4. Optional「[カスタムツールのプロパティを定義する方法](#tbxinfo)」の説明に従って **.tbxinfo**ファイルを作成し、同じディレクトリに追加します。 これによって、ツールボックス アイコンやヒントなどを定義することができます。

    - 1つの **.tbxinfo** ファイルを使用して、複数のツールを定義できます。 これは、サブフォルダーにある複数の図ファイルを参照できます。

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

## <a name="how-to-define-the-properties-of-custom-tools"></a><a name="tbxinfo"></a> カスタムツールのプロパティを定義する方法
 ツールボックス情報 (**.tbxinfo**) ファイルを使用すると、1つまたは複数のカスタムツールのツールボックス名、アイコン、ツールヒント、タブ、およびヘルプキーワードを指定できます。 **Mytools**などの任意の名前を付けます。

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

  **.Tbxinfo**ファイル内のノードは次のとおりです。 各ノードには、既定値が設定されています。

|ノード名|定義|
|---------------|-------------|
|displayName|ツールボックス アイテムの名前。|
|tabName|アイテムが表示されるツールボックス タブ。 この種類の図の標準タブの名前か、別の名前を指定できます。|
|image|ビットマップ (**.bmp**) ファイルの位置。高さと幅は16、色深度は24ビットである必要があります。|
|f1Keyword|ヘルプ トピックを検索するキーワードです。|
|ヒント|このツールのヒントです。|

 Visual Studio でビットマップ ファイルを編集して、[プロパティ] ウィンドウで高さと幅を 16 に設定できます。

> [!NOTE]
> 図ファイルを単独で使用して試した後に .tbxinfo ファイルを使用し始めた場合、ツールボックスには、ツールボックス アイテムの古いバージョンと新しいバージョンの両方が含まれる場合があります。 これは、.tbxinfo ファイルで図ファイルの名前が間違っている場合にも発生します。 この問題が発生した場合は、ツールボックスのショートカットメニューで [ **ツールボックスのリセット**] を選択します。 カスタム ツールボックス アイテムが表示されなくなります。 Visual Studio を再起動すると、正しいカスタム アイテムが表示されます。

## <a name="how-to-distribute-toolbox-items-in-a-visual-studio-extension"></a><a name="Extension"></a> Visual Studio 拡張機能にツールボックスアイテムを配布する方法
 ツールボックスアイテムを [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Visual Studio 拡張機能 (VSIX) にパッケージ化することで、他のユーザーに配布できます。 コマンド、プロファイルなどの拡張機能を同じ VSIX ファイルにパッケージ化できます。 詳細については、「 [Visual Studio 拡張機能の配置](https://msdn.microsoft.com/library/dd393694(VS.100).aspx)」を参照してください。

 Visual Studio 拡張機能をビルドするには、通常は VSIX プロジェクトのテンプレートを使用します。 これを行うには、[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] をインストールしておく必要があります。

#### <a name="to-add-a-toolbox-item-to-a-visual-studio-extension"></a>ツールボックス アイテムを Visual Studio 拡張機能に追加するには

1. [1 つまたは複数のカスタムツールを作成してテスト](#DefineTool)します。

2. ツールを参照する[.tbxinfo ファイルを作成し](#tbxinfo)ます。

3. 既存の Visual Studio 拡張機能プロジェクトを開きます。

     \- または

     新しい Visual Studio 拡張機能プロジェクトを定義します。

    1. **[ファイル]** メニューで、**[新規作成]**、**[プロジェクト]** の順に選択します。

    2. [ **新しいプロジェクト** ] ダイアログボックスの [ **インストールされているテンプレート**] で、[ **Visual C#**]、[ **機能拡張**]、[ **VSIX プロジェクト**] の順に選択します。

4. プロジェクトにツールボックスの定義を追加します。 **.Tbxinfo**ファイル、図ファイル、ビットマップファイル、およびリソースファイルを含め、それらが VSIX に含まれることを確認します。

    - ソリューションエクスプローラーで、VSIX プロジェクトのショートカットメニューの [ **追加**]、[ **既存の項目**] の順に選択します。 ダイアログボックスで、 **種類が [すべてのファイル] のオブジェクト**を設定します。 ファイルを見つけて、すべてを選択し、[ **追加**] を選択します。

        > [!NOTE]
        > このプロジェクトでは、図ファイルをモデル エディターで開くことができません。

5. ここで追加したすべてのファイルについて次のプロパティを設定します。 ソリューション エクスプローラーでそれらすべてを選択すると、それらのプロパティを同時に設定できます。 プロジェクト内の他のファイルのプロパティを変更しないように注意してください。

     **出力ディレクトリ**  =  にコピー**常にコピー**

     **[ビルド アクション]**  =  **[コンテンツ]**

     **VSIX**  =  に含める**true**

6. **source.extension.vsixmanifest**を開きます。 このファイルは拡張機能マニフェスト エディターで開きます。

7. [ **メタデータ**] で、カスタムツールの説明を追加します。

     [ **アセット**] の下で [ **新規** ] を選択し、次のようにダイアログのフィールドを設定します。

    - **型**  = **カスタム拡張機能の種類**

    - 種類 = `Microsoft.VisualStudio.ArchitectureTools.CustomToolboxItems`

        > [!NOTE]
        > これは、ドロップダウン リストのオプションの 1 つではありません。 キーボードを使用して入力する必要があります。

    - **ソース**  = **ファイルシステム上のファイル**。

    - **Path** = **.tbxinfo**ファイル (例: **mytools. .tbxinfo** )

8. プロジェクトをビルドします。

9. **拡張機能が動作することを確認するに**は、F5 キーを押します。 Visual Studio の実験用インスタンスが開始します。

     実験用のインスタンスで、関連する型の UML 図を作成するか開きます。 新しいツールがツールボックスに表示されることと、正しく要素が作成されることを確認します。

10. **配置用の VSIX ファイルを取得するには、次のようにします。** Windows エクスプローラーで、 **.\bin\Debug** または **.\bin\Release** フォルダーを開き、 **.vsix** ファイルを検索します。 これは [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 拡張ファイルです。 このファイルは、自分のコンピューターにインストールできるほか、他の Visual Studio ユーザーに送信することもできます。

#### <a name="to-install-custom-tools-from-a-visual-studio-extension"></a>Visual Studio 拡張機能からカスタム ツールをインストールするには

1. Windows エクスプローラーまたは Visual Studio で `.vsix` ファイルを開きます。

2. 表示されるダイアログボックスで [ **インストール** ] を選択します。

3. 拡張機能をアンインストールするか、一時的に無効にするには、[**ツール**] メニューの [**拡張機能と更新プログラム**] を開きます。

## <a name="localization"></a>ローカリゼーション
 拡張機能が別のコンピューターにインストールされるとターゲット コンピューターの言語でツールの名前やヒントが表示されるように設定できます。

#### <a name="to-provide-versions-of-the-tool-in-more-than-one-language"></a>複数の言語のバージョンのツールを提供するには

1. 1 つ以上のカスタム ツールを含んだ Visual Studio 拡張機能プロジェクトを作成します。

    **.Tbxinfo**ファイルで、リソースファイルのメソッドを使用して、ツール、ツール `displayName` ボックス、およびツールヒントを定義します `tabName` 。 これらの文字列が定義されているリソース ファイルを作成してアセンブリにコンパイルし、tbxinfo ファイルからそれを参照します。

2. 他の言語の文字列のリソース ファイルが含まれている追加のアセンブリを作成します。

3. 言語のカルチャ コードを名前にしたフォルダーに、追加のアセンブリをそれぞれ配置します。 たとえば、フランス語版のアセンブリを **fr**という名前のフォルダー内に配置します。

4. `fr-CA` のような特定カルチャではなく、通常 2 つの文字で構成されるニュートラル カルチャ コードを使用する必要があります。 カルチャコードの詳細については、「 [CultureInfo メソッド](https://msdn.microsoft.com/library/system.globalization.cultureinfo.getcultures(VS.100).aspx)」を参照してください。これにより、カルチャコードの完全な一覧が提供されます。

5. Visual Studio 拡張機能をビルドして配布します。

6. 拡張機能が別のコンピューターにインストールされると、ユーザーのローカル カルチャのリソース ファイルのバージョンが自動的にロードされます。 ユーザーのカルチャのバージョンをまだ提供していない場合、デフォルトのリソースが使用されます。

   この方式を使用して、プロトタイプ図のさまざまなバージョンをインストールすることはできません。 要素とコネクタの名前は、どのインストールでも同じになります。

## <a name="other-toolbox-operations"></a>その他のツールボックスの操作
 通常、[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] では、ツールの名前を変更したり、別のツールボックスのタブに移動したり、それらを削除したりすることで、ツールボックスをカスタマイズすることができます。 ただし、このトピックで説明した手順で作成したカスタム モデリング ツールでは、このような変更が維持されません。 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] を再起動すると、定義済みの名前とツールボックスの場所でツールボックスが再表示されます。

 さらに、[ **ツールボックスのリセット** ] コマンドを実行すると、カスタムツールは表示されなくなります。 しかし、[!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] を再起動すると再び表示されます。

## <a name="see-also"></a>参照
 [Uml モデルと図を拡張](../modeling/extend-uml-models-and-diagrams.md)[するプロファイルを定義して uml を拡張する](../modeling/define-a-profile-to-extend-uml.md)[モデリング図のメニューコマンド](../modeling/define-a-menu-command-on-a-modeling-diagram.md)の定義[uml モデルの検証制約を定義](../modeling/define-validation-constraints-for-uml-models.md)する
