---
title: 基本プロジェクトシステムの作成 パート 1 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: 882a10fa-bb1c-4b01-943a-7a3c155286dd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 4ff969a905d48ef16b3cb036fa897bf0307b929d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739727"
---
# <a name="create-a-basic-project-system-part-1"></a>基本プロジェクト システムの作成、パート 1
Visual Studio では、プロジェクトは、開発者がソース コード ファイルやその他の資産を整理するために使用するコンテナーです。 プロジェクトは、**ソリューション エクスプローラ**にソリューションの子として表示されます。 プロジェクトを使用すると、ソース コードの編成、ビルド、デバッグ、および配置を行い、Web サービス、データベース、およびその他のリソースへの参照を作成できます。

 プロジェクトは、Visual C# プロジェクトの *.csproj*ファイルなど、プロジェクト ファイルで定義されます。 独自のプロジェクト ファイル名拡張子を持つ独自のプロジェクトの種類を作成できます。 プロジェクトの種類の詳細については、「[プロジェクトの種類](../extensibility/internals/project-types.md)」を参照してください。

> [!NOTE]
> Visual Studio をカスタム プロジェクトの種類で拡張する必要がある場合は、プロジェクト システムを最初から構築する上で多くの利点がある[Visual Studio プロジェクト システム](https://github.com/Microsoft/VSProjectSystem)(VSPS) を活用することを強くお勧めします。
>
> - オンボーディングが簡単です。  基本的なプロジェクト システムでも、数万行のコードが必要です。  VSPS を活用することで、必要に応じてカスタマイズする準備が整う前に、オンボーディングのコストを数回のクリックで削減できます。
> - より容易な維持。  VSPS を活用することで、独自のシナリオを維持するだけで済みます。  すべてのプロジェクト システム インフラストラクチャの維持管理を行います。
>
>   Visual Studio 2013 より古いバージョンの Visual Studio を対象とする場合は、Visual Studio 拡張機能で VSPS を活用することはできません。  この場合、このチュートリアルを開始することをお勧めします。

 このチュートリアルでは、プロジェクト ファイル名拡張子 *.myproj*を持つプロジェクトの種類を作成する方法を示します。 このチュートリアルでは、既存の Visual C# プロジェクト システムを使用します。

> [!NOTE]
> 拡張プロジェクトのその他の例については[、VSSDK サンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)を参照してください。

 このチュートリアルでは、次のタスクを実行する方法について説明します。

- 基本的なプロジェクトタイプを作成します。

- 基本的なプロジェクト テンプレートを作成します。

- プロジェクト テンプレートを Visual Studio に登録します。

- [**新しいプロジェクト**] ダイアログ ボックスを開き、テンプレートを使用してプロジェクト インスタンスを作成します。

- プロジェクト システムのプロジェクト ファクトリを作成します。

- プロジェクト システムのプロジェクト ノードを作成します。

- プロジェクト システムのカスタム アイコンを追加します。

- 基本的なテンプレート パラメーター置換を実装します。

## <a name="prerequisites"></a>必須コンポーネント
 Visual Studio 2015 以降では、ダウンロード センターから Visual Studio SDK をインストールしません。 これは、Visual Studio のセットアップのオプション機能として含まれています。 VS SDK は後でインストールすることもできます。 詳細については、「 [Visual Studio SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

 [また、プロジェクトのマネージ パッケージ フレームワーク](https://github.com/tunnelvisionlabs/MPFProj10)のソース コードもダウンロードする必要があります。 作成するソリューションにアクセスできる場所にファイルを抽出します。

## <a name="create-a-basic-project-type"></a>基本的なプロジェクト タイプを作成する
 という名前の C# VSIX プロジェクト**を**作成します。 (**ファイル** > **の新しい** > **プロジェクト**と**Visual C#** > **拡張機能** > **VSIX プロジェクト**) 。 Visual Studio パッケージ プロジェクト項目テンプレートを追加します (**ソリューション エクスプローラ**でプロジェクト ノードを右クリックし、[**新しい項目**の**追加** > ] を選択して、**機能拡張** > **Visual Studio パッケージ**に移動します)。 ファイルに*名前を付けます*。

## <a name="creating-a-basic-project-template"></a>基本的なプロジェクト テンプレートの作成
 これで、この基本的な VSPackage を変更して、新しい *.myproj*プロジェクトの種類を実装できます。 *myproj*プロジェクトの種類に基づくプロジェクトを作成するには、Visual Studio で新しいプロジェクトに追加するファイル、リソース、および参照を認識する必要があります。 この情報を提供するには、プロジェクト ファイルをプロジェクト テンプレート フォルダに配置します。 ユーザーが *.myproj*プロジェクトを使用してプロジェクトを作成すると、ファイルが新しいプロジェクトにコピーされます。

### <a name="to-create-a-basic-project-template"></a>基本的なプロジェクト テンプレートを作成するには

1. プロジェクトに 3 つのフォルダーを追加*します。* (**ソリューション エクスプローラー**で**SimpleProject プロジェクト**ノードを右クリックし、[**追加**] をポイントして、[**新しいフォルダー**] をクリックします。 フォルダに*Templates という名前を付けます*。 *[テンプレート]* フォルダに *、Projects*という名前のフォルダを追加します。 *プロジェクト*フォルダーに *、SimpleProject*という名前のフォルダーを追加します。

2. *テンプレート\プロジェクト\SimpleProject*フォルダーで *、SimpleProject.ico*という名前のアイコンとして使用するビットマップ イメージ ファイルを追加します。 [**追加**] をクリックすると、アイコン エディタが開きます。

3. アイコンを特徴的にします。 このアイコンは、チュートリアルの後半の [**新しいプロジェクト**] ダイアログ ボックスに表示されます。

    ![単純なプロジェクト アイコン](../extensibility/media/simpleprojicon.png "シンプルプロジコン")

4. アイコンを保存し、アイコンエディタを閉じます。

5. *テンプレート\プロジェクト\シンプル プロジェクト*フォルダーで *、Program.cs*という**名前のクラス**項目を追加します。

6. 既存のコードを次の行に置き換えます。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Text;

   namespace $nameSpace$
   {
       public class $className$
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello VSX!!!");
               Console.ReadKey();
           }
       }
   }
   ```

   > [!IMPORTANT]
   > これは *、Program.cs*コードの最終形式ではありません。置換パラメータは後のステップで処理されます。 コンパイル エラーが表示される場合がありますが、ファイルの**BuildAction**が**コンテンツ**である限り、通常どおりプロジェクトをビルドして実行できるはずです。

7. ファイルを保存します。

8. *[**プロパティ]* フォルダーから AssemblyInfo.cs ファイルを*プロジェクト\SimpleProject*フォルダーにコピーします。

9. *プロジェクト\シンプルプロジェクト*フォルダに *、SimpleProject.myproj*という名前の XML ファイルを追加します。

   > [!NOTE]
   > この種類のすべてのプロジェクトのファイル名拡張子は *.myproj*です。 変更する場合は、チュートリアルで説明したすべての場所で変更する必要があります。

10. 既存のコンテンツを次の行に置き換えます。

    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
      <PropertyGroup>
        <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
        <SchemaVersion>2.0</SchemaVersion>
        <ProjectGuid></ProjectGuid>
        <OutputType>Exe</OutputType>
        <RootNamespace>MyRootNamespace</RootNamespace>
        <AssemblyName>MyAssemblyName</AssemblyName>
        <EnableUnmanagedDebugging>false</EnableUnmanagedDebugging>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)' == 'Debug' ">
        <DebugSymbols>true</DebugSymbols>
        <OutputPath>bin\Debug\</OutputPath>
      </PropertyGroup>
      <PropertyGroup Condition=" '$(Configuration)' == 'Release' ">
        <DebugSymbols>false</DebugSymbols>
        <OutputPath>bin\Release\</OutputPath>
      </PropertyGroup>
      <ItemGroup>
        <Reference Include="mscorlib" />
        <Reference Include="System" />
        <Reference Include="System.Data" />
        <Reference Include="System.Xml" />
      </ItemGroup>
      <ItemGroup>
        <Compile Include="AssemblyInfo.cs">
          <SubType>Code</SubType>
        </Compile>
        <Compile Include="Program.cs">
          <SubType>Code</SubType>
        </Compile>
      </ItemGroup>
      <Import Project="$(MSBuildBinPath)\Microsoft.CSharp.targets" />
    </Project>
    ```

11. ファイルを保存します。

12. [**プロパティ ]** ウィンドウで、 [ *AssemblyInfo.cs*]、[ *Program.cs*、 *SimpleProject.ico*、 *SimpleProject.myproj*の**ビルド アクション**を**コンテンツ**に設定し **、VSIX プロパティに含める**プロパティを**True**に設定します。

    このプロジェクト テンプレートは、デバッグ構成とリリース構成の両方を持つ基本的な Visual C# プロジェクトを記述します。 プロジェクトには *、AssemblyInfo.cs*と*Program.cs*の 2 つのソース ファイルと、いくつかのアセンブリ参照が含まれています。 テンプレートからプロジェクトを作成すると、ProjectGuid 値は自動的に新しい GUID に置き換えられます。

    **ソリューション エクスプローラー**で、展開された **[Templates]** フォルダーが次のように表示されます。

```
Templates
   Projects
      SimpleProject
         AssemblyInfo.cs
         Program.cs
         SimpleProject.ico
         SimpleProject.myproj
```

## <a name="create-a-basic-project-factory"></a>基本的なプロジェクト ファクトリを作成する
 プロジェクト テンプレート フォルダーの場所を Visual Studio に指定する必要があります。 これを行うには、プロジェクト ファクトリを実装する VSPackage クラスに属性を追加して、VSPackage のビルド時にテンプレートの場所がシステム レジストリに書き込まれるようにします。 まず、プロジェクト ファクトリ GUID で識別される基本的なプロジェクト ファクトリを作成します。 この属性<xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute>を使用して、プロジェクト ファクトリを`SimpleProjectPackage`クラスに接続します。

### <a name="to-create-a-basic-project-factory"></a>基本的なプロジェクト ファクトリを作成するには

1. プロジェクト ファクトリの GUID を作成するか **([ツール**] メニューの **[GUID**の作成] をクリック) するか、次の例の GUID を使用します。 既に定義されている`SimpleProjectPackage``PackageGuidString`セクションの近くのクラスに GUID を追加します。 GUID は、GUID 形式と文字列形式の両方である必要があります。 結果のコードは、次の例のようになります。

   ```csharp
       public sealed class SimpleProjectPackage : Package
       {
           ...
           public const string SimpleProjectPkgString = "96bf4c26-d94e-43bf-a56a-f8500b52bfad";
           public const string SimpleProjectFactoryString = "471EC4BB-E47E-4229-A789-D1F5F83B52D4";

           public static readonly Guid guidSimpleProjectFactory = new Guid(SimpleProjectFactoryString);
       }
   ```

2. クラスを、 という名前の*最上部の SimpleProject*フォルダー *SimpleProjectFactory.cs*追加します。

3. ディレクティブを使用して以下を追加します。

   ```csharp
   using System.Runtime.InteropServices;
   using Microsoft.VisualStudio.Shell;
   ```

4. GUID 属性をクラスに`SimpleProjectFactory`追加します。 属性の値は、新しいプロジェクト ファクトリ GUID です。

   ```csharp
   [Guid(SimpleProjectPackage.SimpleProjectFactoryString)]
   class SimpleProjectFactory
   {
   }
   ```

   これで、プロジェクト テンプレートを登録できます。

### <a name="to-register-the-project-template"></a>プロジェクト テンプレートを登録するには

1. *SimpleProjectPackage.cs*で、次のように<xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute>クラスに`SimpleProjectPackage`属性を追加します。

   ```csharp
   [ProvideProjectFactory(    typeof(SimpleProjectFactory),     "Simple Project",
       "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
       @"Templates\Projects\SimpleProject",     LanguageVsTemplate = "SimpleProject")]
   [Guid(SimpleProjectPackage.PackageGuidString)]
   public sealed class SimpleProjectPackage : Package
   ```

2. ソリューションを再構築し、エラーが発生せずにビルドされることを確認します。

    プロジェクト テンプレートを再ビルドすると、そのテンプレートが登録されます。

   パラメータ`defaultProjectExtension`は、`possibleProjectExtensions`プロジェクト ファイル名拡張子 (*.myproj*) に設定されます。 パラメーター`projectTemplatesDirectory`は *、Templates*フォルダーの相対パスに設定されます。 ビルド中に、このパスは完全ビルドに変換され、プロジェクト システムを登録するレジストリに追加されます。

## <a name="test-the-template-registration"></a>テンプレート登録のテスト
 テンプレートの登録では、Visual Studio が [**新しいプロジェクト**] ダイアログ ボックスにテンプレート名とアイコンを表示できるように、プロジェクト テンプレート フォルダーの場所を指定します。

### <a name="to-test-the-template-registration"></a>テンプレート登録をテストするには

1. **F5 キー**を押して、Visual Studio の実験用インスタンスのデバッグを開始します。

2. 実験用インスタンスで、新しく作成したプロジェクトタイプの新しいプロジェクトを作成します。 [**新しいプロジェクト**] ダイアログ ボックスで、[**インストールされているテンプレート**] の下**に SimpleProject**が表示されます。

   これで、登録されているプロジェクト ファクトリが作成されました。 ただし、まだプロジェクトを作成することはできません。 プロジェクト パッケージとプロジェクト ファクトリは、プロジェクトを作成および初期化するために連携して動作します。

## <a name="add-the-managed-package-framework-code"></a>マネージ パッケージ フレームワーク コードの追加
 プロジェクト パッケージとプロジェクト ファクトリ間の接続を実装します。

- 管理パッケージ フレームワークのソース コード ファイルをインポートします。

    1. SimpleProject プロジェクトをアンロードします (**ソリューション エクスプローラー**でプロジェクト ノードを選択し、コンテキスト メニューの [**プロジェクトのアンロード**] をクリックします) をクリックし、XML エディターでプロジェクト ファイルを開きます。

    2. 次のブロックをプロジェクト ファイル (インポート>\<ブロックのすぐ上) に追加します。 ダウンロード`ProjectBasePath`したマネージ パッケージ フレームワーク コード内の*ProjectBase.files*ファイルの場所に設定します。 パス名に円記号を追加する必要がある場合があります。 そうしないと、プロジェクトがマネージ パッケージ フレームワークのソース コードを見つけられない可能性があります。

        ```
        <PropertyGroup>
             <ProjectBasePath>your path here\</ProjectBasePath>
             <RegisterWithCodebase>true</RegisterWithCodebase>
          </PropertyGroup>
          <Import Project="$(ProjectBasePath)\ProjectBase.Files" />
        ```

        > [!IMPORTANT]
        > パスの最後にあるバックスラッシュを忘れないでください。

    3. プロジェクトを再読み込みします。

    4. 次のアセンブリへの参照を追加します。

        - `Microsoft.VisualStudio.Designer.Interfaces`* \<(VSSDK では、>\VisualStudio 統合\共通\アセンブリ\v2.0*をインストールします)。

        - `WindowsBase`

        - `Microsoft.Build.Tasks.v4.0`

### <a name="to-initialize-the-project-factory"></a>プロジェクト ファクトリを初期化するには

1. *SimpleProjectPackage.cs*ファイルに次`using`のディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

2. から`Microsoft.VisualStudio.Package.ProjectPackage`クラス`SimpleProjectPackage`を派生します。

    ```csharp
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

3. プロジェクト ファクトリを登録します。 メソッドの直後`base.Initialize`に次の`SimpleProjectPackage.Initialize`行を追加します。

    ```csharp
    base.Initialize();
    this.RegisterProjectFactory(new SimpleProjectFactory(this));
    ```

4. 抽象プロパティ`ProductUserContext`を実装します。

    ```csharp
    public override string ProductUserContext
        {
            get { return ""; }
    }
    ```

5. *SimpleProjectFactory.cs*で、既存`using``using`のディレクティブの後に次のディレクティブを追加します。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

6. から`ProjectFactory`クラス`SimpleProjectFactory`を派生します。

    ```csharp
    class SimpleProjectFactory : ProjectFactory
    ```

7. 次のダミー メソッドをクラス`SimpleProjectFactory`に追加します。 このメソッドは、後のセクションで実装します。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        return null;
    }
    ```

8. 次のフィールドとコンストラクターをクラスに`SimpleProjectFactory`追加します。 この`SimpleProjectPackage`参照は、サービス プロバイダー サイトの設定で使用できるように、プライベート フィールドにキャッシュされます。

    ```csharp
    private SimpleProjectPackage package;

    public SimpleProjectFactory(SimpleProjectPackage package)
        : base(package)
    {
        this.package = package;
    }
    ```

9. ソリューションを再構築し、エラーが発生せずにビルドされることを確認します。

## <a name="test-the-project-factory-implementation"></a>プロジェクト ファクトリの実装をテストする
 プロジェクト ファクトリ実装のコンストラクターが呼び出されているかどうかをテストします。

### <a name="to-test-the-project-factory-implementation"></a>プロジェクト ファクトリの実装をテストするには

1. *SimpleProjectFactory.cs*ファイルで、コンストラクターの次の行にブレークポイントを設定`SimpleProjectFactory`します。

    ```csharp
    this.package = package;
    ```

2. **F5 キー**を押して、Visual Studio の実験用インスタンスを起動します。

3. 実験用インスタンスで、新しいプロジェクトの作成を開始します。 [**新しいプロジェクト**] ダイアログ ボックスで **、SimpleProject**プロジェクトの種類を選択し **、[OK]** をクリックします。 ブレークポイントで実行が停止します。

4. ブレークポイントをクリアし、デバッグを停止します。 まだプロジェクトノードを作成していないので、プロジェクト作成コードは例外をスローします。

## <a name="extend-the-projectnode-class"></a>クラスを拡張します。
 これで、クラスから派生`SimpleProjectNode`したクラスを`ProjectNode`実装できます。 基本`ProjectNode`クラスは、プロジェクト作成の次のタスクを処理します。

- プロジェクト テンプレート ファイル*SimpleProject.myproj*を新しいプロジェクト フォルダーにコピーします。 コピーの名前は、[**新しいプロジェクト**] ダイアログ ボックスに入力した名前に従って変更されます。 プロパティ`ProjectGuid`値は、新しい GUID に置き換えられます。

- プロジェクト テンプレート ファイル*の*MSBuild 要素を走査して、要素を検索`Compile`します。 各`Compile`ターゲット ファイルについて、新しいプロジェクト フォルダーにファイルをコピーします。

  派生`SimpleProjectNode`クラスは、次のタスクを処理します。

- **ソリューション エクスプローラー**のプロジェクト ノードおよびファイル ノードのアイコンを作成または選択できるようにします。

- 追加のプロジェクト テンプレート パラメーター置換を指定できます。

### <a name="to-extend-the-projectnode-class"></a>クラスを拡張するには

1. `SimpleProjectNode.cs`という名前のクラスを追加します。

2. 既存のコードを次のコードに置き換えます。

   ```csharp
   using System;
   using System.Collections.Generic;
   using Microsoft.VisualStudio.Project;

   namespace SimpleProject
   {
       public class SimpleProjectNode : ProjectNode
       {
           private SimpleProjectPackage package;

           public SimpleProjectNode(SimpleProjectPackage package)
           {
               this.package = package;
           }
           public override Guid ProjectGuid
           {
               get { return SimpleProjectPackage.guidSimpleProjectFactory; }
           }
           public override string ProjectType
           {
               get { return "SimpleProjectType"; }
           }

           public override void AddFileFromTemplate(
               string source, string target)
           {
               this.FileTemplateProcessor.UntokenFile(source, target);
               this.FileTemplateProcessor.Reset();
           }
       }
   }
   ```

   この`SimpleProjectNode`クラスの実装には、次のオーバーライドされたメソッドがあります。

- `ProjectGuid`プロジェクト ファクトリ GUID を返します。

- `ProjectType`を指定すると、プロジェクトの種類のローカライズされた名前が返されます。

- `AddFileFromTemplate`を選択すると、選択したファイルがテンプレート フォルダからコピー先のプロジェクトにコピーされます。 このメソッドは、後のセクションで実装されます。

  コンストラクター`SimpleProjectNode`は、`SimpleProjectFactory`コンストラクターと同様に、後で`SimpleProjectPackage`使用するためにプライベート フィールドに参照をキャッシュします。

  `SimpleProjectFactory`クラスを`SimpleProjectNode`クラスに接続するには、メソッド内で新しい`SimpleProjectNode`インスタンスを`SimpleProjectFactory.CreateProject`作成し、後で使用できるようにプライベート フィールドにキャッシュする必要があります。

### <a name="to-connect-the-project-factory-class-and-the-node-class"></a>プロジェクト ファクトリ クラスとノード クラスを接続するには

1. *SimpleProjectFactory.cs*ファイルに、次`using`のディレクティブを追加します。

    ```csharp
    using IOleServiceProvider =    Microsoft.VisualStudio.OLE.Interop.IServiceProvider;
    ```

2. 次の`SimpleProjectFactory.CreateProject`コードを使用して、メソッドを置き換えます。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        SimpleProjectNode project = new SimpleProjectNode(this.package);

        project.SetSite((IOleServiceProvider)        ((IServiceProvider)this.package).GetService(            typeof(IOleServiceProvider)));
        return project;
    }
    ```

3. ソリューションを再構築し、エラーが発生せずにビルドされることを確認します。

## <a name="test-the-projectnode-class"></a>プロジェクト ノード クラスをテストする
 プロジェクト ファクトリをテストして、プロジェクト階層が作成されるかどうかを確認します。

### <a name="to-test-the-projectnode-class"></a>クラスをテストするには

1. **F5** キーを押してデバッグを開始します。 実験用インスタンスで、新しい Simple プロジェクトを作成します。

2. Visual Studio は、プロジェクト ファクトリを呼び出してプロジェクトを作成する必要があります。

3. Visual Studio の実験用インスタンスを終了します。

## <a name="add-a-custom-project-node-icon"></a>カスタム プロジェクト ノード アイコンを追加する
 前のセクションのプロジェクト ノード アイコンは、既定のアイコンです。 カスタム アイコンに変更できます。

### <a name="to-add-a-custom-project-node-icon"></a>カスタム プロジェクト ノード アイコンを追加するには

1. **リソース**フォルダーに *、SimpleProjectNode.bmp*という名前のビットマップ ファイルを追加します。

2. **[プロパティ]** ウィンドウで、ビットマップを 16 x 16 ピクセルに縮小します。 ビットマップを特徴的にします。

    ![単純なプロジェクト Comm](../extensibility/media/simpleprojprojectcomm.png "シンプルプロジプロジェクトコム")

3. [**プロパティ]** ウィンドウで、ビットマップの **[ビルド] アクション**を **[埋め込みリソース**] に変更します。

4. *SimpleProjectNode.cs*で、次`using`のディレクティブを追加します。

   ```csharp
   using System.Drawing;
   using System.Windows.Forms;
   ```

5. 次の静的フィールドとコンストラクターをクラスに`SimpleProjectNode`追加します。

   ```csharp
   private static ImageList imageList;

   static SimpleProjectNode()
   {
       imageList =        Utilities.GetImageList(            typeof(SimpleProjectNode).Assembly.GetManifestResourceStream(                "SimpleProject.Resources.SimpleProjectNode.bmp"));
   }
   ```

6. クラスの先頭に次のプロパティを追加`SimpleProjectNode`します。

   ```csharp
   internal static int imageIndex;
      public override int ImageIndex
      {
          get { return imageIndex; }
      }
   ```

7. インスタンス コンストラクターを次のコードに置き換えます。

   ```csharp
   public SimpleProjectNode(SimpleProjectPackage package)
   {
       this.package = package;

       imageIndex = this.ImageHandler.ImageList.Images.Count;

       foreach (Image img in imageList.Images)
       {
           this.ImageHandler.AddImage(img);
       }
   }
   ```

   静的構築時に`SimpleProjectNode`、アセンブリ マニフェスト リソースからプロジェクト ノード ビットマップを取得し、後で使用するためにプライベート フィールドにキャッシュします。 イメージ パスの構文<xref:System.Reflection.Assembly.GetManifestResourceStream%2A>に注目してください。 アセンブリに埋め込まれているマニフェスト リソースの名前を表示するには、<xref:System.Reflection.Assembly.GetManifestResourceNames%2A>メソッドを使用します。 このメソッドがアセンブリに適用される`SimpleProject`場合、結果は次のようになります。

- *リソース*

- *リソース*

- *リソース*

- *リソース.イメージリス.bmp*

- *リソース*

- *リソース*

- *リソース.シンプルプロジェクトノード.bmp*

  インスタンスの構築中に`ProjectNode`、基本クラスは*Resources.imagelis.bmp*を読み込み、組み込まれている*Resources\imagelis.bmp*から 16 x 16 のビットマップを埋め込みます。 このビットマップ リストは、`SimpleProjectNode`で`ImageHandler.ImageList`使用できます。 `SimpleProjectNode`プロジェクト ノードビットマップをリストに追加します。 イメージ リスト内のプロジェクト ノード ビットマップのオフセットは、後でパブリック`ImageIndex`プロパティの値として使用するためにキャッシュされます。 Visual Studio では、このプロパティを使用して、プロジェクト ノード アイコンとして表示するビットマップを決定します。

## <a name="test-the-custom-project-node-icon"></a>カスタム プロジェクト ノード アイコンをテストする
 プロジェクト ファクトリをテストして、カスタム プロジェクト ノード アイコンを持つプロジェクト階層が作成されているかどうかを確認します。

### <a name="to-test-the-custom-project-node-icon"></a>カスタム プロジェクト ノード アイコンをテストするには

1. デバッグを開始し、実験用インスタンスで新しい SimpleProject を作成します。

2. 新しく作成されたプロジェクトで *、SimpleProjectNode.bmp*がプロジェクト ノード アイコンとして使用されていることに注目してください。

     ![単純なプロジェクト New Project ノード](../extensibility/media/simpleprojnewprojectnode.png "ノード")

3. コード エディターで *Program.cs* を開きます。 次のコードのようなソース コードが表示されます。

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Text;

    namespace $nameSpace$
    {
        public class $className$
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Hello VSX!!!");
                Console.ReadKey();
            }
        }
    }
    ```

     テンプレートパラメーター$nameSpace$ と $className$ には新しい値が含まれていないことに注意してください。 テンプレート パラメーターの置換を実装する方法については、次のセクションで説明します。

## <a name="substitute-template-parameters"></a>代替テンプレート パラメーター
 前のセクションでは、属性を使用して Visual Studio でプロジェクト`ProvideProjectFactory`テンプレートを登録しました。 この方法でテンプレート フォルダーのパスを登録すると、クラスをオーバーライドおよび展開することで、基本的なテンプレート パラメーター`ProjectNode.AddFileFromTemplate`の置換を有効にできます。 詳細については、「[新しいプロジェクト生成: ボンネットの下のパート 2](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)」を参照してください。

 次に、置換コードを`AddFileFromTemplate`クラスに追加します。

### <a name="to-substitute-template-parameters"></a>テンプレート パラメーターを置き換える

1. *SimpleProjectNode.cs*ファイルに次`using`のディレクティブを追加します。

   ```csharp
   using System.IO;
   ```

2. 次の`AddFileFromTemplate`コードを使用して、メソッドを置き換えます。

   ```csharp
   public override void AddFileFromTemplate(
       string source, string target)
   {
       string nameSpace =
           this.FileTemplateProcessor.GetFileNamespace(target, this);
       string className = Path.GetFileNameWithoutExtension(target);

       this.FileTemplateProcessor.AddReplace("$nameSpace$", nameSpace);
       this.FileTemplateProcessor.AddReplace("$className$", className);

       this.FileTemplateProcessor.UntokenFile(source, target);
       this.FileTemplateProcessor.Reset();
   }
   ```

3. メソッドの割り当てステートメントの直後に`className`ブレークポイントを設定します。

   代入ステートメントは、名前空間と新しいクラス名の妥当な値を決定します。 2`ProjectNode.FileTemplateProcessor.AddReplace`つのメソッド呼び出しは、これらの新しい値を使用して、対応するテンプレート パラメーター値を置き換えます。

## <a name="test-the-template-parameter-substitution"></a>テンプレート パラメーター置換のテスト
 これで、テンプレートパラメーターの置換をテストできます。

### <a name="to-test-the-template-parameter-substitution"></a>テンプレート パラメーターの置換をテストするには

1. デバッグを開始し、実験用インスタンスで新しい SimpleProject を作成します。

2. メソッドのブレークポイントで実行が`AddFileFromTemplate`停止します。

3. パラメーターと`className`パラメーターの`nameSpace`値を調べます。

   - `nameSpace`プロジェクト テンプレート ファイルの\<ルート名前空間>要素の値*が*与えられます。 この場合、値は `MyRootNamespace` です。

   - `className`には、ファイル名拡張子を付けずにクラス ソース ファイル名の値が指定されます。 この場合、コピー先フォルダにコピーされる最初のファイルは*AssemblyInfo.cs。* したがって、クラス名の値は`AssemblyInfo`です。

4. ブレークポイントを削除し **、F5**キーを押して実行を続行します。

    プロジェクトの作成が完了します。

5. コード エディターで *Program.cs* を開きます。 次のコードのようなソース コードが表示されます。

   ```csharp
   using System;
   using System.Collections.Generic;
   using System.Linq;
   using System.Text;

   namespace MyRootNamespace
   {
       public class Program
       {
           static void Main(string[] args)
           {
               Console.WriteLine("Hello VSX!!!");
               Console.ReadKey();
           }
       }
   }
   ```

    名前空間が現在`MyRootNamespace`の名前空間であり、クラス名が`Program`.

6. プロジェクトのデバッグを開始します。 新しいプロジェクトはコンパイル、実行、および表示する必要があります"こんにちは VSX!!!" コンソール ウィンドウに表示します。

    ![単純なプロジェクト コマンド](../extensibility/media/simpleprojcommand.png "シンプルプロジコマンド")

   おめでとうございます! 基本管理プロジェクト システムを実装しました。
