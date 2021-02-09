---
title: 基本的なプロジェクトシステムの作成、パート 1 |Microsoft Docs
description: 拡張子 myproj という名前のプロジェクトの種類を作成する方法について説明します。 Visual Studio では、プロジェクトはソースコードファイルやその他のアセットを整理するために使用されるコンテナーです。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- writing a project system
- project system
- tutorial
ms.assetid: 882a10fa-bb1c-4b01-943a-7a3c155286dd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: a1b21ef736e69c962db389a7bb1a3eb284ebdd0a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99887368"
---
# <a name="create-a-basic-project-system-part-1"></a>基本プロジェクトシステムを作成する (第1部)
Visual Studio では、プロジェクトは、ソースコードファイルやその他のアセットを整理するために開発者が使用するコンテナーです。 プロジェクトは、 **ソリューションエクスプローラー** のソリューションの子として表示されます。 プロジェクトを使用すると、ソースコードを整理、ビルド、デバッグ、および配置したり、Web サービス、データベース、その他のリソースへの参照を作成したりすることができます。

 プロジェクトは、プロジェクトファイル (たとえば、Visual C# プロジェクトの *.csproj* ファイル) で定義されます。 独自のプロジェクトファイル名拡張子を持つ独自のプロジェクトの種類を作成できます。 プロジェクトの種類の詳細については、「 [プロジェクトの種類](../extensibility/internals/project-types.md)」を参照してください。

> [!NOTE]
> カスタムプロジェクトの種類を使用して Visual Studio を拡張する必要がある場合は、 [Visual studio プロジェクトシステム](https://github.com/Microsoft/VSProjectSystem) (.vsps) を活用することを強くお勧めします。これには、プロジェクトシステムをゼロから構築するよりも多くの利点があります。
>
> - 簡単なオンボード。  基本的なプロジェクトシステムであっても、10万行のコードが必要です。  .VSPS を利用することで、お客様のニーズに合わせてカスタマイズできるようになるまでに、オンボードコストをわずか数クリックで減らすことができます。
> - 保守が簡単になります。  .VSPS を利用することで、独自のシナリオを維持する必要があります。  すべてのプロジェクトシステムインフラストラクチャの保守を処理します。
>
>   Visual Studio 2013 よりも前のバージョンの Visual Studio を対象とする必要がある場合は、Visual Studio 拡張機能で .VSPS を利用することはできません。  その場合は、このチュートリアルを開始することをお勧めします。

 このチュートリアルでは、プロジェクトファイル名拡張子 *myproj* を持つプロジェクトの種類を作成する方法について説明します。 このチュートリアルでは、既存の Visual C# プロジェクトシステムからではします。

> [!NOTE]
> 拡張機能プロジェクトのその他の例については、「 [Vssdk のサンプル](https://github.com/Microsoft/VSSDK-Extensibility-Samples)」を参照してください。

 このチュートリアルでは、次のタスクを実行する方法について説明します。

- 基本的なプロジェクトの種類を作成します。

- 基本的なプロジェクトテンプレートを作成します。

- プロジェクトテンプレートを Visual Studio に登録します。

- [ **新しいプロジェクト** ] ダイアログボックスを開き、テンプレートを使用して、プロジェクトインスタンスを作成します。

- プロジェクトシステムのプロジェクトファクトリを作成します。

- プロジェクトシステムのプロジェクトノードを作成します。

- プロジェクトシステムのカスタムアイコンを追加します。

- 基本的なテンプレートパラメーターの置換を実装します。

## <a name="prerequisites"></a>前提条件
 Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。 詳細については、「 [Visual STUDIO SDK のインストール](../extensibility/installing-the-visual-studio-sdk.md)」を参照してください。

 また、 [プロジェクトのマネージパッケージフレームワーク](https://github.com/tunnelvisionlabs/MPFProj10)のソースコードをダウンロードする必要があります。 作成するソリューションにアクセスできる場所にファイルを抽出します。

## <a name="create-a-basic-project-type"></a>基本的なプロジェクトの種類を作成する
 **Simpleproject** という名前の C# VSIX プロジェクトを作成します。 (**ファイル**  > **新規**  > [**プロジェクト**]、次に [ **Visual C#**]  >  **機能拡張**  >  **VSIX プロジェクト**) をクリックします。 Visual Studio パッケージプロジェクト項目テンプレートを追加します (**ソリューションエクスプローラー** で、プロジェクトノードを右クリックし、[**追加**] [  >  **新しい項目**] の順に選択し、[**機能拡張**  >  **Visual Studio パッケージ**] にアクセスします)。 ファイルに *Simpleprojectpackage* という名前を指定します。

## <a name="creating-a-basic-project-template"></a>基本的なプロジェクトテンプレートの作成
 ここで、この基本的な VSPackage を変更して、新しい *myproj* プロジェクトの種類を実装できます。 *Myproj* プロジェクトの種類に基づくプロジェクトを作成するには、Visual Studio は、新しいプロジェクトに追加するファイル、リソース、および参照を認識している必要があります。 この情報を提供するには、プロジェクトファイルをプロジェクトテンプレートフォルダーに配置します。 ユーザーが *myproj* プロジェクトを使用してプロジェクトを作成すると、ファイルが新しいプロジェクトにコピーされます。

### <a name="to-create-a-basic-project-template"></a>基本的なプロジェクトテンプレートを作成するには

1. プロジェクトに3つのフォルダーを追加します。もう1つは *Templates\Projects\SimpleProject* です。 ( **ソリューションエクスプローラー** で、 **simpleproject** プロジェクトノードを右クリックして [ **追加**] をポイントし、[ **新しいフォルダー**] をクリックします。 フォルダーに *テンプレート* の名前を指定します。 *Templates* フォルダーに、 *Projects* という名前のフォルダーを追加します。 *Projects* フォルダーに、 *simpleproject* という名前のフォルダーを追加します。)

2. *Templates\Projects\SimpleProject* フォルダーに、 *simpleproject .ico* という名前のアイコンとして使用するビットマップイメージファイルを追加します。 [ **追加**] をクリックすると、アイコンエディターが開きます。

3. アイコンが特徴的になるようにします。 このアイコンは、このチュートリアルの後半の [ **新しいプロジェクト** ] ダイアログボックスに表示されます。

    ![単純なプロジェクト アイコン](../extensibility/media/simpleprojicon.png "SimpleProjIcon")

4. アイコンを保存し、アイコンエディターを閉じます。

5. *Templates\Projects\SimpleProject* フォルダーに、 *Program.cs* という名前の **クラス** 項目を追加します。

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
   > これは、 *Program.cs* コードの最終的な形式ではありません。置換パラメーターについては、後の手順で扱います。 コンパイルエラーが発生する場合がありますが、ファイルの **BuildAction** が **コンテンツ** である限り、通常どおりにプロジェクトをビルドして実行できます。

7. ファイルを保存します。

8. *AssemblyInfo.cs* ファイルを *Properties* フォルダーから、[プロジェクト]、[ *simpleproject* ] フォルダーにコピーします。

9. [プロジェクト]、[ *simpleproject* ] フォルダーで、 *simpleproject. myproj* という名前の XML ファイルを追加します。

   > [!NOTE]
   > この種類のすべてのプロジェクトのファイル名拡張子は、 *myproj* です。 変更する場合は、このチュートリアルで説明されているすべての場所で変更する必要があります。

10. 既存の内容を次の行に置き換えます。

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

12. [**プロパティ**] ウィンドウで、 *AssemblyInfo.cs*、 *Program.cs*、 *Simpleproject* の **ビルドアクション** を [**コンテンツ** *] に設定* し、[ **VSIX に含める**] プロパティを [ **True**] に設定します。

    このプロジェクトテンプレートには、デバッグ構成とリリース構成の両方を含む基本的な Visual C# プロジェクトが記述されています。 プロジェクトには、 *AssemblyInfo.cs* と *Program.cs* の2つのソースファイルと、いくつかのアセンブリ参照が含まれています。 プロジェクトがテンプレートから作成されると、ProjectGuid 値は自動的に新しい GUID に置き換えられます。

    **ソリューションエクスプローラー** では、展開された **テンプレート** フォルダーは次のようになります。

```
Templates
   Projects
      SimpleProject
         AssemblyInfo.cs
         Program.cs
         SimpleProject.ico
         SimpleProject.myproj
```

## <a name="create-a-basic-project-factory"></a>基本的なプロジェクトファクトリの作成
 プロジェクトテンプレートフォルダーの場所を Visual Studio に通知する必要があります。 これを行うには、プロジェクトファクトリを実装する VSPackage クラスに属性を追加して、VSPackage のビルド時にテンプレートの場所がシステムレジストリに書き込まれるようにします。 まず、プロジェクトファクトリ GUID で識別される基本的なプロジェクトファクトリを作成します。 属性を使用して、 <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> プロジェクトファクトリをクラスに接続し `SimpleProjectPackage` ます。

### <a name="to-create-a-basic-project-factory"></a>基本的なプロジェクトファクトリを作成するには

1. プロジェクトファクトリの Guid を作成します ([ **ツール** ] メニューの [ **guid の作成**] をクリックするか、次の例のいずれかを使用します)。 `SimpleProjectPackage`が既に定義されているセクションの近くで、guid をクラスに追加 `PackageGuidString` します。 Guid は、GUID 形式と文字列形式の両方にする必要があります。 結果のコードは、次の例のようになります。

   ```csharp
       public sealed class SimpleProjectPackage : Package
       {
           ...
           public const string SimpleProjectPkgString = "96bf4c26-d94e-43bf-a56a-f8500b52bfad";
           public const string SimpleProjectFactoryString = "471EC4BB-E47E-4229-A789-D1F5F83B52D4";

           public static readonly Guid guidSimpleProjectFactory = new Guid(SimpleProjectFactoryString);
       }
   ```

2. *SimpleProjectFactory.cs* という名前の最上位の *simpleproject* フォルダーにクラスを追加します。

3. ディレクティブを使用して以下を追加します。

   ```csharp
   using System.Runtime.InteropServices;
   using Microsoft.VisualStudio.Shell;
   ```

4. クラスに GUID 属性を追加 `SimpleProjectFactory` します。 属性の値は、新しいプロジェクトファクトリ GUID です。

   ```csharp
   [Guid(SimpleProjectPackage.SimpleProjectFactoryString)]
   class SimpleProjectFactory
   {
   }
   ```

   これで、プロジェクトテンプレートを登録できるようになりました。

### <a name="to-register-the-project-template"></a>プロジェクトテンプレートを登録するには

1. *SimpleProjectPackage.cs* で、次のように、 <xref:Microsoft.VisualStudio.Shell.ProvideProjectFactoryAttribute> クラスに属性を追加し `SimpleProjectPackage` ます。

   ```csharp
   [ProvideProjectFactory(    typeof(SimpleProjectFactory),     "Simple Project",
       "Simple Project Files (*.myproj);*.myproj", "myproj", "myproj",
       @"Templates\Projects\SimpleProject",     LanguageVsTemplate = "SimpleProject")]
   [Guid(SimpleProjectPackage.PackageGuidString)]
   public sealed class SimpleProjectPackage : Package
   ```

2. ソリューションをリビルドし、エラーなしでビルドされることを確認します。

    再構築すると、プロジェクトテンプレートが登録されます。

   パラメーターとは、 `defaultProjectExtension` `possibleProjectExtensions` プロジェクトのファイル名拡張子 (*myproj*) に設定されます。 `projectTemplatesDirectory`パラメーターは、 *Templates* フォルダーの相対パスに設定されます。 ビルド中、このパスは完全ビルドに変換され、プロジェクトシステムを登録するためにレジストリに追加されます。

## <a name="test-the-template-registration"></a>テンプレートの登録をテストする
 テンプレートの登録では、visual studio が [ **新しいプロジェクト** ] ダイアログボックスにテンプレート名とアイコンを表示できるように、プロジェクトテンプレートフォルダーの場所を visual studio に指示します。

### <a name="to-test-the-template-registration"></a>テンプレートの登録をテストするには

1. **F5** キーを押して、Visual Studio の実験用インスタンスのデバッグを開始します。

2. 実験用インスタンスで、新しく作成したプロジェクトの種類の新しいプロジェクトを作成します。 [**新しいプロジェクト**] ダイアログボックスで、[**インストールされたテンプレート**] の下に **simpleproject** が表示されます。

   これで、プロジェクトファクトリが登録されました。 ただし、まだプロジェクトを作成することはできません。 プロジェクトパッケージとプロジェクトファクトリが連携して、プロジェクトを作成および初期化します。

## <a name="add-the-managed-package-framework-code"></a>マネージパッケージフレームワークコードを追加する
 プロジェクトパッケージとプロジェクトファクトリ間の接続を実装します。

- マネージパッケージフレームワークのソースコードファイルをインポートします。

    1. SimpleProject プロジェクトをアンロードし ( **ソリューションエクスプローラー** でプロジェクトノードを選択し、コンテキストメニューの [ **プロジェクトのアンロード**] をクリックします)、XML エディターでプロジェクトファイルを開きます。

    2. 次のブロックをプロジェクトファイル (ブロックのすぐ上) に追加 \<Import> します。 `ProjectBasePath`ダウンロードしたマネージパッケージフレームワークコードで、 *projectbase. files* ファイルの場所をに設定します。 場合によっては、パス名に円記号を追加する必要があります。 そうしないと、プロジェクトはマネージパッケージフレームワークのソースコードを見つけることができない可能性があります。

        ```
        <PropertyGroup>
             <ProjectBasePath>your path here\</ProjectBasePath>
             <RegisterWithCodebase>true</RegisterWithCodebase>
          </PropertyGroup>
          <Import Project="$(ProjectBasePath)\ProjectBase.Files" />
        ```

        > [!IMPORTANT]
        > パスの末尾に円記号を忘れないでください。

    3. プロジェクトを再度読み込みます。

    4. 次のアセンブリへの参照を追加します。

        - `Microsoft.VisualStudio.Designer.Interfaces`( *\<VSSDK install> \VisualStudioIntegration\Common\Assemblies\v2.0* 内)

        - `WindowsBase`

        - `Microsoft.Build.Tasks.v4.0`

### <a name="to-initialize-the-project-factory"></a>プロジェクトファクトリを初期化するには

1. *SimpleProjectPackage.cs* ファイルで、次のディレクティブを追加し `using` ます。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

2. からクラスを派生させ `SimpleProjectPackage` `Microsoft.VisualStudio.Package.ProjectPackage` ます。

    ```csharp
    public sealed class SimpleProjectPackage : ProjectPackage
    ```

3. プロジェクトファクトリを登録します。 の直後に、メソッドに次の行を追加し `SimpleProjectPackage.Initialize` `base.Initialize` ます。

    ```csharp
    base.Initialize();
    this.RegisterProjectFactory(new SimpleProjectFactory(this));
    ```

4. 抽象プロパティを実装し `ProductUserContext` ます。

    ```csharp
    public override string ProductUserContext
        {
            get { return ""; }
    }
    ```

5. *SimpleProjectFactory.cs* で、既存のディレクティブの後に次のディレクティブを追加し `using` `using` ます。

    ```csharp
    using Microsoft.VisualStudio.Project;
    ```

6. からクラスを派生させ `SimpleProjectFactory` `ProjectFactory` ます。

    ```csharp
    class SimpleProjectFactory : ProjectFactory
    ```

7. 次のダミーメソッドをクラスに追加し `SimpleProjectFactory` ます。 このメソッドは、後のセクションで実装します。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        return null;
    }
    ```

8. 次のフィールドとコンストラクターをクラスに追加し `SimpleProjectFactory` ます。 この `SimpleProjectPackage` 参照は、サービスプロバイダーサイトの設定時に使用できるように、プライベートフィールドにキャッシュされます。

    ```csharp
    private SimpleProjectPackage package;

    public SimpleProjectFactory(SimpleProjectPackage package)
        : base(package)
    {
        this.package = package;
    }
    ```

9. ソリューションをリビルドし、エラーなしでビルドされることを確認します。

## <a name="test-the-project-factory-implementation"></a>プロジェクトファクトリの実装をテストする
 プロジェクトファクトリの実装のコンストラクターが呼び出されているかどうかをテストします。

### <a name="to-test-the-project-factory-implementation"></a>プロジェクトファクトリの実装をテストするには

1. *SimpleProjectFactory.cs* ファイルで、コンストラクターの次の行にブレークポイントを設定し `SimpleProjectFactory` ます。

    ```csharp
    this.package = package;
    ```

2. **F5** キーを押して、Visual Studio の実験用インスタンスを開始します。

3. 実験用インスタンスで、新しいプロジェクトの作成を開始します。 [ **新しいプロジェクト** ] ダイアログボックスで、 **simpleproject** プロジェクトの種類を選択し、[ **OK**] をクリックします。 ブレークポイントで実行が停止します。

4. ブレークポイントをクリアし、デバッグを停止します。 プロジェクトノードをまだ作成していないため、プロジェクトの作成コードでも例外がスローされます。

## <a name="extend-the-projectnode-class"></a>ProjectNode クラスの拡張
 クラスから派生したクラスを実装できるようになりました `SimpleProjectNode` `ProjectNode` 。 `ProjectNode`基本クラスは、プロジェクト作成の次のタスクを処理します。

- プロジェクトテンプレートファイル *simpleproject* を新しいプロジェクトフォルダーにコピーします。 [ **新しいプロジェクト** ] ダイアログボックスに入力された名前に従って、コピーの名前が変更されます。 `ProjectGuid`プロパティ値は新しい GUID に置き換えられます。

- プロジェクトテンプレートファイルの MSBuild 要素である *simpleproject* を走査し、要素を検索し `Compile` ます。 `Compile`ターゲットファイルごとに、によって新しいプロジェクトフォルダーにファイルがコピーされます。

  派生クラスは、 `SimpleProjectNode` 次のタスクを処理します。

- **ソリューションエクスプローラー** 内のプロジェクトノードとファイルノードのアイコンを作成または選択できるようにします。

- 追加のプロジェクトテンプレートパラメーターの置換を指定できるようにします。

### <a name="to-extend-the-projectnode-class"></a>ProjectNode クラスを拡張するには

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

   この `SimpleProjectNode` クラスの実装には、次のオーバーライドされたメソッドがあります。

- `ProjectGuid`。これにより、プロジェクトファクトリ GUID が返されます。

- `ProjectType`。プロジェクトの種類のローカライズされた名前を返します。

- `AddFileFromTemplate`。選択したファイルをテンプレートフォルダーからコピー先のプロジェクトにコピーします。 このメソッドは、後のセクションでさらに実装されます。

  コンストラクターはコンストラクターと同様に、 `SimpleProjectNode` `SimpleProjectFactory` `SimpleProjectPackage` 後で使用するためにプライベートフィールドに参照をキャッシュします。

  クラスをクラスに接続するには、 `SimpleProjectFactory` `SimpleProjectNode` メソッドで新しいをインスタンス化 `SimpleProjectNode` し、後で使用できるように `SimpleProjectFactory.CreateProject` プライベートフィールドにキャッシュする必要があります。

### <a name="to-connect-the-project-factory-class-and-the-node-class"></a>プロジェクトファクトリクラスと node クラスを接続するには

1. *SimpleProjectFactory.cs* ファイルで、次のディレクティブを追加し `using` ます。

    ```csharp
    using IOleServiceProvider =    Microsoft.VisualStudio.OLE.Interop.IServiceProvider;
    ```

2. `SimpleProjectFactory.CreateProject`次のコードを使用して、メソッドを置き換えます。

    ```csharp
    protected override ProjectNode CreateProject()
    {
        SimpleProjectNode project = new SimpleProjectNode(this.package);

        project.SetSite((IOleServiceProvider)        ((IServiceProvider)this.package).GetService(            typeof(IOleServiceProvider)));
        return project;
    }
    ```

3. ソリューションをリビルドし、エラーなしでビルドされることを確認します。

## <a name="test-the-projectnode-class"></a>ProjectNode クラスのテスト
 プロジェクトファクトリをテストして、プロジェクトの階層が作成されているかどうかを確認します。

### <a name="to-test-the-projectnode-class"></a>ProjectNode クラスをテストするには

1. **F5** キーを押してデバッグを開始します。 実験用インスタンスで、新しい SimpleProject を作成します。

2. プロジェクトを作成するには、Visual Studio でプロジェクトファクトリを呼び出す必要があります。

3. Visual Studio の実験用インスタンスを終了します。

## <a name="add-a-custom-project-node-icon"></a>[カスタムプロジェクトノードの追加] アイコン
 前のセクションの [プロジェクトノード] アイコンは既定のアイコンです。 カスタムアイコンに変更することができます。

### <a name="to-add-a-custom-project-node-icon"></a>カスタムプロジェクトノードアイコンを追加するには

1. **Resources** フォルダーに、 *SimpleProjectNode.bmp* という名前のビットマップファイルを追加します。

2. [ **プロパティ** ] ウィンドウで、ビットマップを 16 x 16 ピクセルに縮小します。 ビットマップを区別できるようにします。

    ![単純なプロジェクト Comm](../extensibility/media/simpleprojprojectcomm.png "SimpleProjProjectComm")

3. [ **プロパティ** ] ウィンドウで、ビットマップの [ **ビルド] アクション** を [ **埋め込みリソース**] に変更します。

4. *SimpleProjectNode.cs* で、次のディレクティブを追加し `using` ます。

   ```csharp
   using System.Drawing;
   using System.Windows.Forms;
   ```

5. 次の静的フィールドとコンストラクターをクラスに追加し `SimpleProjectNode` ます。

   ```csharp
   private static ImageList imageList;

   static SimpleProjectNode()
   {
       imageList =        Utilities.GetImageList(            typeof(SimpleProjectNode).Assembly.GetManifestResourceStream(                "SimpleProject.Resources.SimpleProjectNode.bmp"));
   }
   ```

6. 次のプロパティをクラスの先頭に追加し `SimpleProjectNode` ます。

   ```csharp
   internal static int imageIndex;
      public override int ImageIndex
      {
          get { return imageIndex; }
      }
   ```

7. インスタンスコンストラクターを次のコードに置き換えます。

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

   静的構築中に、は `SimpleProjectNode` アセンブリマニフェストリソースからプロジェクトノードビットマップを取得し、後で使用できるようにプライベートフィールドにキャッシュします。 イメージパスの構文に注意して <xref:System.Reflection.Assembly.GetManifestResourceStream%2A> ください。 アセンブリに埋め込まれているマニフェストリソースの名前を表示するには、メソッドを使用し <xref:System.Reflection.Assembly.GetManifestResourceNames%2A> ます。 このメソッドがアセンブリに適用されると、結果は次のようになり `SimpleProject` ます。

- *SimpleProject .resources .resources*

- *VisualStudio*

- *SimpleProject*

- *Resources.imagelis.bmp*

- *VisualStudio (Microsoft. プロジェクトのプロパティ)*

- *VisualStudio を参照してください。*

- *SimpleProject.Resources.SimpleProjectNode.bmp*

  インスタンスの構築時に、 `ProjectNode` 基底クラスは *Resources.imagelis.bmp* を読み込みます。この場合、 *Resources\imagelis.bmp* から 16 x 16 のビットマップが埋め込まれています。 このビットマップリストは、で使用できるようになり `SimpleProjectNode` `ImageHandler.ImageList` ます。 `SimpleProjectNode` プロジェクトノードのビットマップをリストに追加します。 イメージリスト内のプロジェクトノードビットマップのオフセットは、後でパブリックプロパティの値として使用できるようにキャッシュされ `ImageIndex` ます。 Visual Studio では、このプロパティを使用して、プロジェクトノードアイコンとして表示するビットマップを決定します。

## <a name="test-the-custom-project-node-icon"></a>[カスタムプロジェクトノードをテストする] アイコン
 プロジェクトファクトリをテストして、カスタムプロジェクトノードアイコンを持つプロジェクト階層が作成されているかどうかを確認します。

### <a name="to-test-the-custom-project-node-icon"></a>カスタムプロジェクトノードのアイコンをテストするには

1. デバッグを開始し、実験用インスタンスで新しい SimpleProject を作成します。

2. 新しく作成されたプロジェクトで、 *SimpleProjectNode.bmp* がプロジェクトノードアイコンとして使用されていることを確認します。

     ![単純なプロジェクト New Project ノード](../extensibility/media/simpleprojnewprojectnode.png "SimpleProjNewProjectNode")

3. コード エディターで *Program.cs* を開きます。 次のコードのようなソースコードが表示されます。

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

     テンプレートパラメーター $nameSpace $ および $className $ に新しい値がないことに注意してください。 テンプレートパラメーターの置換を実装する方法については、次のセクションで説明します。

## <a name="substitute-template-parameters"></a>テンプレートパラメーターの置換
 前のセクションでは、属性を使用して、プロジェクトテンプレートを Visual Studio に登録しました `ProvideProjectFactory` 。 この方法でテンプレートフォルダーのパスを登録すると、クラスをオーバーライドして展開することで、基本的なテンプレートパラメーターの置換を有効にすることができ `ProjectNode.AddFileFromTemplate` ます。 詳細については、「 [新しいプロジェクトの生成: 内部的にはパート 2](../extensibility/internals/new-project-generation-under-the-hood-part-two.md)」を参照してください。

 次に、クラスに置換コードを追加 `AddFileFromTemplate` します。

### <a name="to-substitute-template-parameters"></a>テンプレートパラメーターを置き換えるには

1. *SimpleProjectNode.cs* ファイルで、次のディレクティブを追加し `using` ます。

   ```csharp
   using System.IO;
   ```

2. `AddFileFromTemplate`次のコードを使用して、メソッドを置き換えます。

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

3. メソッドで、代入ステートメントの直後にブレークポイントを設定し `className` ます。

   代入ステートメントによって、名前空間と新しいクラス名に適切な値が決定されます。 2つの `ProjectNode.FileTemplateProcessor.AddReplace` メソッド呼び出しは、これらの新しい値を使用して、対応するテンプレートパラメーターの値を置き換えます。

## <a name="test-the-template-parameter-substitution"></a>テンプレートパラメーターの代入をテストする
 テンプレートパラメーターの置換をテストできるようになりました。

### <a name="to-test-the-template-parameter-substitution"></a>テンプレートパラメーターの置換をテストするには

1. デバッグを開始し、実験用インスタンスで新しい SimpleProject を作成します。

2. 実行は、メソッド内のブレークポイントで停止 `AddFileFromTemplate` します。

3. パラメーターとパラメーターの値を確認し `nameSpace` `className` ます。

   - `nameSpace` には、 \<RootNamespace> *\Templates\Projects\SimpleProject\SimpleProject.myproj* プロジェクトテンプレートファイル内の要素の値が指定されます。 この場合、値は `MyRootNamespace` です。

   - `className` には、ファイル名拡張子のないクラスソースファイル名の値が指定されています。 この場合、コピー先のフォルダーにコピーされる最初のファイルは *AssemblyInfo.cs* です。このため、className の値はに `AssemblyInfo` なります。

4. ブレークポイントを削除し、 **F5** キーを押して実行を続行します。

    Visual Studio によってプロジェクトの作成が完了します。

5. コード エディターで *Program.cs* を開きます。 次のコードのようなソースコードが表示されます。

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

    名前空間がになり、クラス名がになっていることに注意して `MyRootNamespace` `Program` ください。

6. プロジェクトのデバッグを開始します。 新しいプロジェクトは、"Hello VSX!!!" をコンパイルして実行し、表示する必要があります。 コンソール ウィンドウに表示します。

    ![単純なプロジェクト コマンド](../extensibility/media/simpleprojcommand.png "SimpleProjCommand")

   お疲れさまでした。 基本的なマネージプロジェクトシステムを実装しました。
