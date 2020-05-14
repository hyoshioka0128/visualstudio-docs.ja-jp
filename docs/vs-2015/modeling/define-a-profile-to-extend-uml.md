---
title: プロファイルを定義して UML を拡張する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: conceptual
helpviewer_keywords:
- profiles, UML
- stereotypes, UML
- UML, profiles and stereotypes
- UML - extending, defining profiles
- UML, customizing
- UML, profiles
ms.assetid: 776589cb-f89d-48d5-aafa-04a4c074b0d6
caps.latest.revision: 44
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a495a566f78ceb2b89f8e2070837f038da352a4d
ms.sourcegitcommit: 939407118f978162a590379997cb33076c57a707
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2020
ms.locfileid: "75918876"
---
# <a name="define-a-profile-to-extend-uml"></a>プロファイルを定義して UML を拡張する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*UML プロファイル*を定義して、標準のモデル要素を特定の目的に合わせてカスタマイズすることができます。 プロファイルは、1つまたは複数の*UML ステレオタイプ*を定義します。 ステレオタイプは、特定の種類のオブジェクトを表すものとして型をマークするために使用できます。 ステレオタイプを使用して、要素のプロパティのリストを拡張することもできます。

 いくつかのプロファイルは、これをサポートするエディションの Visual Studio をインストールするときに、同時にインストールされます。 この機能をサポートする Visual Studio のバージョンを確認するには、「 [Version support for architecture and modeling tools](../modeling/what-s-new-for-design-in-visual-studio.md#VersionSupport)」を参照してください。 これらのプロファイルの詳細およびステレオタイプを適用する方法については、「[プロファイルとステレオタイプを使用](../modeling/customize-your-model-with-profiles-and-stereotypes.md)してモデルをカスタマイズする」を参照してください。

 独自のプロファイルを定義して、UML を特定のビジネス領域またはアーキテクチャに適応させ、拡張することができます。 例:

- Web サイトを頻繁に定義する場合は、クラス図のクラスに適用できる «WebPage» ステレオタイプを提供する独自のプロファイルを定義できます。 これにより、クラス図を使用して Web サイトを計画できます。 各 «WebPage» クラスは、ページのコンテンツやスタイルなどの追加のプロパティを持つことになります。

- 銀行業務ソフトウェアを開発する場合は、«Account» ステレオタイプを提供するプロファイルを定義できます。 これにより、クラス図を使用して複数の異なる種類の口座を定義し、口座間の関係を示すことができます。

  独自に生成したプロファイルはチームに配布できます。 すべてのチーム メンバーがそれぞれそのプロファイルをインストールできます。 これにより、チーム メンバーは、独自に編集を加えて、そのステレオタイプを使用するモデルを生成できます。

> [!NOTE]
> 現在編集中のモデルでプロファイルのステレオタイプを適用し、そのモデルを他のユーザーと共有する場合、これらのユーザーは同じプロファイルをそれぞれ自分のコンピューターにインストールする必要があります。 インストールされていないと、他のユーザーは適用されたステレオタイプを確認できません。

 プロファイルは、多くの場合、より大きな [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 拡張機能の一部です。 たとえば、モデルのいくつかのパートをコードに翻訳するコマンドを定義できます。 このとき、ユーザーが翻訳するパッケージに適用する必要のあるプロファイルを定義します。 この新しいコマンドを、単一の [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 拡張機能でプロファイルと共に配布します。

 また、プロファイルをローカライズしたバリアントも定義できます。 生成した拡張機能を読み込んだユーザーには、ユーザーのカルチャに適したバリアントが表示されます。

## <a name="DefineProfile"></a>プロファイルを定義する方法

#### <a name="to-define-a-uml-profile"></a>UML プロファイルを定義するには

1. `.profile` というファイル名拡張子を持つ新しい XML ファイルを生成します。

2. 「[プロファイルの構造](#Schema)」で説明されているガイドラインに従って、ステレオタイプの定義を追加します。

3. プロファイルを Visual Studio 拡張機能 (`.vsix` ファイル) に追加します。 プロファイル用に新しい拡張機能を生成するか、またはプロファイルを既存の拡張機能に追加します。

     次のセクション「[プロファイルを Visual Studio 拡張機能に追加する方法](#AddProfile)」を参照してください。

4. 拡張機能をコンピューターにインストールします。

    1. `.vsix` というファイル名拡張子を持つ拡張ファイルをダブルクリックします。

    2. Visual Studio を再起動します。

5. プロファイルがインストールされたことを確認します。

    1. UML エクスプローラーでモデルを選択します。

    2. プロパティウィンドウで、 **[プロファイル]** プロパティをクリックします。 プロファイルがメニューに表示されます。 プロファイルの横にチェック マークを設定します。

    3. プロファイルでステレオタイプを定義する要素を選択します。 プロパティウィンドウで、 **[ステレオタイプ]** プロパティをクリックします。 リストにステレオタイプが表示されます。 ステレオタイプのいずれか 1 つにチェック マークを設定します。

    4. プロファイルでこのステレオタイプの追加のプロパティを定義する場合は、ステレオタイプ プロパティを展開してプロパティを表示します。

6. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の他のユーザーに拡張ファイルを送信して、コンピューターにインストールしてもらいます。

## <a name="AddProfile"></a>Visual Studio 拡張機能にプロファイルを追加する方法
 プロファイルをインストールし、他のユーザーに送信できるようにするには、プロファイルを Visual Studio 拡張機能に追加する必要があります。 詳細については、「 [Visual Studio 拡張機能の配置](https://msdn.microsoft.com/library/dd393694(VS.100).aspx)」を参照してください。

#### <a name="to-define-a-profile-in-a-new-visual-studio-extension"></a>新しい Visual Studio 拡張機能でプロファイルを定義するには

1. Visual Studio 拡張機能プロジェクトを生成します。

   > [!NOTE]
   > この手順を実行するには、[!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] がインストールされている必要があります。

   1. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。

   2. **[新しいプロジェクト]** ダイアログボックスの **[インストールされたテンプレート]** で、 **[ビジュアルC# ]** 、 **[機能拡張]** 、 **[VSIX プロジェクト]** の順に展開します。 プロジェクト名を設定し、[ **OK]** をクリックします。

2. プロファイルをプロジェクトに追加します。

   - ソリューションエクスプローラーで、プロジェクトを右クリックして **[追加]** をポイントし、 **[既存の項目]** をクリックします。 ダイアログ ボックスで、生成したプロファイル ファイルを見つけます。

3. プロファイルファイルの "**出力にコピー** " プロパティを設定します。

   1. ソリューションエクスプローラーで、プロファイルファイルを右クリックし、 **[プロパティ]** をクリックします。

   2. プロパティウィンドウで、 **[出力ディレクトリにコピー]** プロパティを **[常にコピー]** する に設定します。

4. ソリューション エクスプローラーで、`source.extension.vsixmanifest` を開きます。

    このファイルは拡張機能マニフェスト エディターで開きます。

5. **[資産]** ページで、プロファイルを説明する行を追加します。

   - [新規] をクリックします。 **[新しい資産の追加]** ダイアログボックスで、次のようにフィールドを設定します。

   - **型**を `Microsoft.VisualStudio.UmlProfile` に設定します

        これは、ドロップダウン リストに表示される選択肢の 1 つではありません。 この名前はキーボードを使用して入力します。

   - **[ファイルシステム上のファイル]** をクリックし、プロファイルファイルの名前を選択し `MyProfile.profile`

6. プロジェクトをビルドする。

7. **プロファイルをデバッグするに**は、F5 キーを押します。

    Visual Studio の実験用インスタンスが開きます。 このインスタンスで、モデリング プロジェクトを開きます。 UML エクスプローラーで、モデルのルート要素を選択し、[プロパティ] ウィンドウでプロファイルを選択します。 次に、モデル内の要素を選択し、それらの要素に対して定義したステレオタイプを設定します。

8. **配置用に VSIX を抽出するには**

   1. Windows エクスプローラーで、 **.\bin\Debug**または **.\bin\Release**フォルダーを開き、 **.vsix**ファイルを検索します。 これは [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 拡張ファイルです。 このファイルは、自分のコンピューターにインストールできるほか、他の Visual Studio ユーザーに送信することもできます。

   2. 拡張機能をインストールするには

       1. `.vsix` ファイルをダブルクリックします。 Visual Studio 拡張機能インストーラーが起動されます。

       2. 実行中のすべての Visual Studio のインスタンスを再起動します。

   [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] がインストールされていない場合は、サイズの小さい拡張機能に対して、次の手順を代わりに使用できます。

#### <a name="to-define-a-profile-extension-without-using-visual-studio-sdk"></a>Visual Studio SDK を使用せずにプロファイル拡張機能を定義するには

1. Windows ディレクトリを生成し、次の 3 つのファイルを格納します。

    - *プロファイル*`.profile`

    - `extension.vsixmanifest`

    - `[Content_Types].xml`-次に示すように、角かっこを使用してこの名前を入力します。

2. 次のテキストが含まれるように `[Content_Types].xml` を編集します。 それぞれのファイル名拡張子のエントリが含まれている点に注目してください。

    ```
    <?xml version="1.0" encoding="utf-8"?>
    <Types xmlns="http://schemas.openxmlformats.org/package/2006/content-types">
      <Default Extension="profile" ContentType="application/octet-stream" />
      <Default Extension="vsixmanifest" ContentType="text/xml" />
    </Types>
    ```

3. 既存の `extension.vsixmanifest` をコピーし、XML エディターを使用して編集します。 ID、Name、および Content の各ノードに変更を加えます。

    - 次のディレクトリ内に、`extension.vsixmanifest` の例が含まれています。

         *ドライブ* **: \Common7\IDE\Extensions\Microsoft\Architecture | Visual Studio [バージョン]** ツールのプロファイル

    - Content ノードは次のようになります。

        ```
        <Content>
          <CustomExtension Type="Microsoft.VisualStudio.UmlProfile"
          >YourProfile.Profile</CustomExtension>
        </Content>
        ```

4. 3 つのファイルを 1 つの zip ファイルに圧縮します。

     Windows エクスプローラーで、3つのファイルを選択し、右クリックして **[送信]** をポイントし、 **[圧縮 (zip 形式) フォルダー]** をクリックします。

5. zip ファイルの名前を変更し、ファイル名拡張子を `.zip` から `.vsix` に変更します。

6. Visual Studio の適切なエディションがインストールされているコンピューターにこのプロファイルをインストールするには、`.vsix` ファイルをダブルクリックします。

#### <a name="to-install-a-uml-profile-from-a-visual-studio-extension"></a>Visual Studio 拡張機能から UML プロファイルをインストールするには

1. Windows エクスプローラーで `.vsix` ファイルをダブルクリックするか、または Visual Studio 内でこのファイルを開きます。

2. 表示されるダイアログボックスで **[インストール]** をクリックします。

3. 拡張機能をアンインストールするか、一時的に無効にするには、 **[ツール]** メニューの **[拡張機能と更新プログラム]** を開きます。

## <a name="Localized"></a>ローカライズされたプロファイルを定義する方法
 複数の異なるカルチャまたは言語に対して複数の異なるプロファイルを定義し、それらすべてを同じ拡張機能にパッケージ化することができます。 ユーザーが拡張機能を読み込むと、ユーザーのカルチャに対して定義されているプロファイルが表示されます。

 既定のプロファイルは必ず用意する必要があります。 ユーザーのカルチャに対して定義されているプロファイルがない場合は、既定のプロファイルが表示されます。

#### <a name="to-define-a-localized-profile"></a>ローカライズされたプロファイルを定義するには

1. 前のセクション「[プロファイルを定義する方法](#DefineProfile)」および「[プロファイルを Visual Studio 拡張機能に追加する方法](#AddProfile)」の説明に従って、プロファイルを作成します。 これが既定のプロファイルであり、ローカライズされたプロファイルが用意されていないインストールで使用されます。

2. 既定のプロファイル ファイルが格納されているディレクトリ内に新しいディレクトリを追加します。

    > [!NOTE]
    > Visual Studio 拡張機能プロジェクトを使用して拡張機能を構築する場合は、ソリューション エクスプローラーを使用して新しいフォルダーをプロジェクトに追加します。

3. 新しいディレクトリの名前を、ローカライズ カルチャを示す短い ISO コードに変更します (たとえば、ブルガリア語の場合は `bg`、フランス語の場合は `fr`)。 `fr-CA` のような特定カルチャではなく、通常 2 つの文字で構成されるニュートラル カルチャ コードを使用する必要があります。 カルチャコードの詳細については、「 [CultureInfo メソッド](https://msdn.microsoft.com/library/system.globalization.cultureinfo.getcultures(VS.100).aspx)」を参照してください。これにより、カルチャコードの完全な一覧が提供されます。

4. 既定のプロファイルを新しいディレクトリにコピーします。 ファイル名は変更しないでください。

     サンプル [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)] 拡張機能フォルダーは、`.vsix` ファイルに構築または圧縮される前に、次のフォルダーとファイルを含みます。

     `extension.vsixmanifest`

     `MyProfile.profile`

     `fr\MyProfile.profile`

     `de\MyProfile.profile`

    > [!NOTE]
    > `extension.vsixmanifest` にはプロファイルのローカライズ バージョンへの参照を挿入しないでください。 コピーされたプロファイル ファイルの名前は、親フォルダー内のプロファイルの名前と同じある必要があります。

5. プロファイルの新しいコピーを編集して、ユーザーに対して表示されるすべての部分 (たとえば、`displayName` の属性) をターゲット言語に翻訳します。

6. 追加のカルチャ フォルダーとローカライズされたプロファイルは、必要なカルチャの数だけ生成できます。

7. 前のセクションで説明したように、拡張機能プロジェクトをビルドするか、またはすべてのファイルを圧縮して、Visual Studio 拡張機能を生成します。

## <a name="Schema"></a>プロファイルの構造

 プロファイル ファイルを編集しやすいように、次の場所に `.xsd` ファイルをインストールします。

 **%ProgramFiles%\Microsoft Visual Studio [version] \ xmlschema**

 ここでは、例として C# プロファイルを使用します。 完全なプロファイル定義については、次のファイルを参照してください。

 *ドライブ* **: \Common7\IDE\Extensions\Microsoft\Architecture Visual Studio [バージョン] Tools\UmlProfiles\CSharp.profile**

 このパスの最初の部分は、インストールに応じて異なる可能性があります。

 .NET プロファイルの詳細については、「 [UML モデルの標準ステレオタイプ](../modeling/standard-stereotypes-for-uml-models.md)」を参照してください。

### <a name="main-sections-of-the-uml-profile-definition"></a>UML プロファイル定義の主要なセクション
 すべてのプロファイルに次の内容が含まれています。

```
<?xml version="1.0" encoding="utf-8"?>
<profile dslVersion="1.0.0.0"
       name="CSharpProfile" displayName="C# Profile"
       xmlns="http://schemas.microsoft.com/UML2.1.2/ProfileDefinition">
  <stereotypes>...</stereotypes>
  <metaclasses>...</metaclasses>
  <propertyTypes>...</propertyTypes>
</profile>
```

> [!NOTE]
> `name` という属性には、空白または句読点を含めることはできません。 ユーザー インターフェイスに表示される属性 `displayName` は、有効な XML 文字列である必要があります。

 すべてのプロファイルに次の 3 つの主要なセクションが含まれています。 これらのセクションを逆順に示します。

- `<propertyTypes>`-[ステレオタイプ] セクションで定義されているプロパティに使用される型の一覧です。

- `<metaclasses>`: このプロファイルのステレオタイプが適用されるモデル要素の型のリスト (IClass、IInterface、IOperation、IDependency など)。

- `<stereotypes>`-ステレオタイプの定義。 それぞれの定義には、ターゲットのモデル要素に追加されるプロパティの名前と型が含まれています。

#### <a name="property-types"></a>プロパティの型
 `<propertyTypes>` セクションでは、`<stereotypes>` セクションのプロパティに使用される型のリストを宣言します。 プロパティの型には、外部型と列挙型の 2 種類があります。

 外部型は、標準 .NET 型の完全修飾名を宣言します。

```
<externalType name="System.String" />
```

 列挙型は、リテラル値のセットを定義します。

```
<enumerationType name="PackageVisibility">
  <enumerationLiterals>
    <enumerationLiteral name="internal" displayName="internal"  />
    <enumerationLiteral name="protectedinternal" displayName="protected internal" />
  </enumerationLiterals>
</enumerationType>
```

#### <a name="metaclasses"></a>メタクラス
 `<metaclasses>` セクションは、このプロファイルのステレオタイプを定義できるモデル要素の型のリストです。

```
<metaclass
      name="Microsoft.VisualStudio.Uml.Classes.IClass" />
<metaclass
      name="Microsoft.VisualStudio.Uml.Classes.IInterface" />
<metaclass
      name="Microsoft.VisualStudio.Uml.Components.IComponent" />
```

 メタクラスとして使用できるモデル要素とリレーションシップ型の完全な一覧については、「[モデル要素の型](#Elements)」を参照してください。

#### <a name="stereotype-definition"></a>ステレオタイプ定義
 `<stereotypes>` セクションには、1 つ以上のステレオタイプ定義が記述されています。

```
<stereotype name="CSharpClass" displayName="C# Class"> ...
```

 各ステレオタイプには、そのステレオタイプを適用できる 1 つ以上のモデル要素または関係の型が記述されています。 基本型の名前を指定して、すべての派生型を含めることができます。 たとえば、`Microsoft.VisualStudio.Uml.Classes.IType` と指定した場合、このステレオタイプは、`IClass`、`IInterface`、`IEnumeration`、およびいくつかのその他の要素の型に適用できます。

```
<metaclasses>
  <metaclassMoniker name=
   "/CSharpProfile/Microsoft.VisualStudio.Uml.Classes.IClass" />
</metaclasses>
```

 `name` の `metaclassMoniker` 属性は、`<metaClasses>` セクションの要素へのリンクです。

> [!NOTE]
> モニカー名は `/yourProfileName/` で始まる必要があります。ここで、`yourProfileName` は、プロファイルの `name` 属性で定義されています (この例では "CSharpProfile")。 モニカーは、メタクラス セクションのいずれかのエントリ名で終わります。

 それぞれのステレオタイプでは、ステレオタイプが適用される任意のモデル要素に追加する 0 個以上のプロパティを指定できます。 `<propertyType>` には、`<propertyTypes>` セクションで定義されているいずれかの型へのリンクが含まれています。 リンクは、`<externalTypeMoniker>` (`<externalType>,` を参照する場合) または `<enumerationTypeMoniker>` (`<enumerationType>` を参照する場合) のどちらかである必要があります。 このリンクについても、プロファイルの名前がプレフィックスとして付けられます。

```
  <properties>
    <property name="IsStatic"
            displayName="Is Static" defaultValue="false">
      <propertyType>
<externalTypeMoniker
               name="/CSharpProfile/System.Boolean" />
      </propertyType>
    </property>
    <property name="PackageVisibility"
              displayName="Package Visibility"
              defaultValue="internal">
      <propertyType>
        <enumerationTypeMoniker
              name="/CSharpProfile/PackageVisibility"/>
      </propertyType>
    </property>
  </properties>
</stereotype>
```

## <a name="Elements"></a>モデル要素の型
 ステレオタイプを定義できる型のセットについては、「 [UML モデル要素の型](../modeling/uml-model-element-types.md)」をご覧ください。

## <a name="troubleshooting"></a>トラブルシューティング
 ステレオタイプが UML モデルに表示されません。
パッケージまたはモデルでプロファイルを選択する必要があります。 これで、ステレオタイプはパッケージまたはモデル内の要素上に表示されます。 詳細については、「 [UML モデル要素にステレオタイプを追加する](../modeling/add-stereotypes-to-uml-model-elements.md)」を参照してください。

 UML モデルを開くと、次のエラーが表示されます: **VS1707: シリアル化エラーが発生したため、次のプロファイルを読み込むことができません: myprofile。プロファイル**
1. .profile の基本的な XML 構文が正しいことを確認してください。

2. 各モニカー名の形式が /profileName/nodeName であることを確認してください。 profileName とは、ルート プロファイル ノードの名前属性の値です。 nodeName とは、メタクラス externalType または enumerationType の名前属性の値です。

3. ここで説明されている構文に従ってください。「 _drive_ **:\\\Common7\IDE\Extensions\Microsoft\Architecture」 (Visual Studio [version])** で説明されているように、「drive:」のようにします。

4. 障害のある拡張機能をアンインストールします。 **[ツール]** メニューの **[拡張機能と更新プログラム]** をクリックします。

   - 拡張機能が表示されなければ、次のアイテムを確認します。

5. VSIX ファイルをリビルドし、Windows エクスプローラーで開いて再インストールします。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]を再起動します。

   拡張機能は拡張機能マネージャーに表示されませんが、再インストールを試みると、次のメッセージが表示されます:**拡張機能は、適用されているすべての製品に既にインストール**されています。
   1. *Localappdata*\Microsoft\VisualStudio\\[version] \Extensions\ のサブフォルダーから拡張ファイルを削除します。

   - *Localappdata*を表示するには、Windows エクスプローラーのフォルダーオプションの [表示] タブで [非表示のファイルとフォルダーの表示] を設定する必要があります。

   - *Localappdata*は通常、C:\Users\\*ユーザー名*\AppData\Local\ にあります。

6. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]を再起動します。

## <a name="see-also"></a>参照
 [Uml モデル要素にステレオタイプを追加する](../modeling/add-stereotypes-to-uml-model-elements.md)[プロファイルとステレオタイプを使用したモデルのカスタマイズ](../modeling/customize-your-model-with-profiles-and-stereotypes.md) [uml モデルの標準ステレオタイプ](../modeling/standard-stereotypes-for-uml-models.md)
 