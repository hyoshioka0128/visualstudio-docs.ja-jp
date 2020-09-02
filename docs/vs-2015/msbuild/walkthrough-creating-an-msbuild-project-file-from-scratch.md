---
title: 'チュートリアル: MSBuild プロジェクト ファイルのゼロからの作成 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tutorial
ms.assetid: e3acff7c-cb4e-4ae1-8be2-a871bcff847b
caps.latest.revision: 22
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: eb49e6c51c1e51d002683099797d940cb2d24556
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65682370"
---
# <a name="walkthrough-creating-an-msbuild-project-file-from-scratch"></a>チュートリアル: MSBuild プロジェクト ファイルのゼロからの作成
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

.NET Framework を対象とするプログラミング言語は、MSBuild プロジェクト ファイルを使用してアプリケーションのビルド プロセスを記述および制御します。 Visual Studio を使用して MSBuild プロジェクト ファイルを作成すると、適切な XML が自動的に追加されますが、 その XML がどのように構成されているかや、それに変更を加えてビルドを制御するにはどうすればよいかを知っておくことも有用です。  
  
 C++ プロジェクトのプロジェクト ファイルを作成する方法の詳細については、「[MSBuild (Visual C++)](https://msdn.microsoft.com/library/7a1be7ff-0312-4669-adf2-5f5bf507d560)」をご覧ください。  
  
 このチュートリアルでは、テキスト エディターのみを使用して、基本的なプロジェクト ファイルをインクリメント方式で作成する方法について説明します。 このチュートリアルの手順を以下に示します。  
  
- 最低限の内容のみを含むアプリケーション ソース ファイルを作成します。  
  
- 最低限の内容のみを含む MSBuild プロジェクト ファイルを作成します。  
  
- MSBuild が含まれるように PATH 環境変数を拡張します。  
  
- プロジェクト ファイルを使用してアプリケーションをビルドします。  
  
- ビルドを制御するためのプロパティを追加します。  
  
- プロパティの値を変更してビルドを制御します。  
  
- ビルド ターゲットを追加します。  
  
- ターゲットを指定してビルドを制御します。  
  
- インクリメンタル ビルドを実行します。  
  
  このチュートリアルでは、コマンド プロンプトでプロジェクトをビルドして結果を確認する方法を説明します。 MSBuild の詳細および MSBuild をコマンド プロンプトで実行する方法の詳細については、「[チュートリアル: MSBuild の使用](../msbuild/walkthrough-using-msbuild.md)」をご覧ください。  
  
  このチュートリアルを実行するには、.NET Framework (Version 2.0、3.5、4.0、または 4.5) がインストールされている必要があります。これらには、このチュートリアルに必要な MSBuild と Visual C# コンパイラが含まれています。  
  
## <a name="creating-a-minimal-application"></a>最低限の内容のみを含むアプリケーションを作成する  
 ここでは、最低限の内容のみを含む Visual C# アプリケーション ソース ファイルをテキスト エディターで作成する方法を説明します。  
  
#### <a name="to-create-the-minimal-application"></a>最低限の内容のみを含むアプリケーションを作成するには  
  
1. コマンド プロンプトで、アプリケーションを作成するフォルダーに移動します (\My Documents\、\Desktop\\ など)。  
  
2. 「**md HelloWorld**」と入力して、 \HelloWorld\\ というサブフォルダーを作成します。  
  
3. 「**cd HelloWorld**」と入力して、その新しいフォルダーに移動します。  
  
4. メモ帳またはその他のテキスト エディターを起動して、次のコードを入力します。  
  
    ```  
    using System;  
  
    class HelloWorld  
    {  
        static void Main()  
        {  
    #if DebugConfig  
            Console.WriteLine("WE ARE IN THE DEBUG CONFIGURATION");  
    #endif  
  
            Console.WriteLine("Hello, world!");  
        }  
    }  
    ```  
  
5. このソース コード ファイルを Helloworld.cs という名前で保存します。  
  
6. コマンド プロンプトで「**csc helloworld.cs**」と入力して、アプリケーションをビルドします。  
  
7. コマンド プロンプトで「**helloworld**」と入力して、アプリケーションをテストします。  
  
     "**Hello, world!** " というメッセージが表示されます。  
  
8. コマンド プロンプトで「**del helloworld.exe**」と入力して、アプリケーションを削除します。  
  
## <a name="creating-a-minimal-msbuild-project-file"></a>最低限の内容のみを含む MSBuild プロジェクト ファイルを作成する  
 最低限の内容のみを含むアプリケーション ソース ファイルを作成できたので、次に、そのアプリケーションをビルドするための最低限の内容のみを含むプロジェクト ファイルを作成します。 このプロジェクト ファイルに含まれる要素は次のとおりです。  
  
- 必須のルート `Project` ノード  
  
- 項目要素を格納する `ItemGroup` ノード  
  
- アプリケーション ソース ファイルを参照する項目要素  
  
- アプリケーションをビルドするために必要なタスクを格納する `Target` ノード  
  
- アプリケーションをビルドするために Visual C# コンパイラを起動する `Task` 要素  
  
#### <a name="to-create-a-minimal-msbuild-project-file"></a>最低限の内容のみを含む MSBuild プロジェクト ファイルを作成するには  
  
1. テキスト エディターで、既存のテキストを次の 2 つの行に置き換えます。  
  
   ```  
   <Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   </Project>  
   ```  
  
2. 次の `ItemGroup` ノードを `Project` ノードの子要素として挿入します。  
  
   ```  
   <ItemGroup>  
     <Compile Include="helloworld.cs" />  
   </ItemGroup>  
   ```  
  
    この `ItemGroup` には既に項目要素が含まれています。  
  
3. `Target` ノードの子要素として `Project` ノードを追加します。 そのノードに `Build` という名前を付けます。  
  
   ```  
   <Target Name="Build">  
   </Target>  
   ```  
  
4. 次のタスク要素を `Target` ノードの子要素として挿入します。  
  
   ```  
   <Csc Sources="@(Compile)"/>  
   ```  
  
5. このプロジェクト ファイルを Helloworld.csproj という名前で保存します。  
  
   最低限の内容のみを含むプロジェクト ファイルが完成すると、コードが次のようになります。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <ItemGroup>  
    <Compile Include="helloworld.cs" />  
  </ItemGroup>  
  <Target Name="Build">  
    <Csc Sources="@(Compile)"/>    
  </Target>  
</Project>  
```  
  
 Build ターゲットのタスクは順番に実行されます。 ここでは、Visual C# コンパイラの `Csc` タスクが唯一のタスクです。 このタスクは、コンパイルするソース ファイルのリストを受け取ります。これは、`Compile` 項目の値によって渡されます。 `Compile` 項目は、Helloworld.cs という 1 つのソース ファイルのみを参照しています。  
  
> [!NOTE]
> 項目要素でワイルドカード文字のアスタリスク (*) を使用して、拡張子 .cs を持つすべてのファイルを参照することもできます。次に例を示します。  
>   
> `<Compile Include="*.cs" />`  
>   
> ただし、ワイルドカード文字を使用すると、ソース ファイルを追加または削除した場合にデバッグやターゲットの選択が困難になるため、できるだけ使用しないようにしてください。  
  
## <a name="extending-the-path-to-include-msbuild"></a>MSBuild が含まれるようにパスを拡張する  
 MSBuild を使用するには、.NET Framework フォルダーが含まれるように PATH 環境変数を拡張する必要があります。  
  
#### <a name="to-add-msbuild-to-your-path"></a>MSBuild をパスに追加するには  
  
- Visual Studio 2013 では、MSBuild フォルダー (32 ビット オペレーティング システムの場合は `%ProgramFiles%\MSBuild`、64 ビット オペレーティング システムの場合は `%ProgramFiles(x86)%\MSBuild`) 内に MSBuild.exe があります。  
  
     コマンド プロンプトで、「**set PATH=%PATH%;%ProgramFiles%\MSBuild**」または「**set PATH=%PATH%;%ProgramFiles(x86)%\MSBuild**」と入力します。  
  
     Visual Studio がインストールされている場合は、**Visual Studio コマンド プロンプト**を使用することもできます。Visual Studio コマンド プロンプトでは、MSBuild フォルダーへのパスが設定されています。  
  
## <a name="using-the-project-file-to-build-the-application"></a>プロジェクト ファイルを使用してアプリケーションをビルドする  
 次に、先ほど作成したプロジェクト ファイルを使用してアプリケーションをビルドします。  
  
#### <a name="to-build-the-application"></a>アプリケーションをビルドするには  
  
1. コマンドプロンプトで、「 **msbuild helloworld. .csproj/t: Build**」と入力します。  
  
     Visual C# コンパイラが呼び出され、Helloworld プロジェクト ファイルの Build ターゲットがビルドされて、Helloworld アプリケーションが作成されます。  
  
2. 「**helloworld**」と入力してアプリケーションをテストします。  
  
     "**Hello, world!** " というメッセージが表示されます。  
  
> [!NOTE]
> 詳細レベルを上げると、ビルドの詳細情報を表示できます。 詳細レベルを "detailed" に設定するには、コマンド プロンプトで次のいずれかのコマンドを入力します。  
>   
> **msbuild helloworld. .csproj/t: Build/verbosity: detailed**  
  
## <a name="adding-build-properties"></a>ビルド プロパティを追加する  
 プロジェクト ファイルにビルド プロパティを追加すると、ビルドをさらに細かく制御できます。 ここでは、次のプロパティを追加します。  
  
- アプリケーションの名前を指定する `AssemblyName` プロパティ  
  
- アプリケーションを格納するフォルダーを指定する `OutputPath` プロパティ  
  
#### <a name="to-add-build-properties"></a>ビルド プロパティを追加するには  
  
1. コマンド プロンプトで「**del helloworld.exe**」と入力して、既存のアプリケーションを削除します。  
  
2. プロジェクト ファイルで、次の `PropertyGroup` 要素を開始 `Project` 要素の直後に挿入します。  
  
   ```  
   <PropertyGroup>  
     <AssemblyName>MSBuildSample</AssemblyName>  
     <OutputPath>Bin\</OutputPath>  
   </PropertyGroup>  
   ```  
  
3. 次のタスクを Build ターゲットの `Csc` タスクの直前に追加します。  
  
   ```  
   <MakeDir Directories="$(OutputPath)"      Condition="!Exists('$(OutputPath)')" />  
   ```  
  
    この `MakeDir` タスクは、`OutputPath` プロパティによって指定されるフォルダーを、同名のフォルダーが存在しない場合に作成します。  
  
4. 次の `OutputAssembly` 属性を `Csc` タスクに追加します。  
  
   ```  
   <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />  
   ```  
  
    この属性は、Visual C# コンパイラに対して、`AssemblyName` プロパティによって指定されるアセンブリを生成し、`OutputPath` プロパティによって指定されるフォルダーに配置するように指定します。  
  
5. 変更内容を保存します。  
  
   プロジェクト ファイルのコードが次のようになります。  
  
```  
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <PropertyGroup>  
    <AssemblyName>MSBuildSample</AssemblyName>  
    <OutputPath>Bin\</OutputPath>  
  </PropertyGroup>  
  <ItemGroup>  
    <Compile Include="helloworld.cs" />  
  </ItemGroup>  
  <Target Name="Build">  
    <MakeDir Directories="$(OutputPath)" Condition="!Exists('$(OutputPath)')" />  
    <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />  
  </Target>  
</Project>  
```  
  
> [!NOTE]
> パス区切り記号の円記号 (\\) は、`Csc` タスクの `OutputAssembly` 属性に追加するのではなく、`OutputPath` 要素で指定するフォルダー名の末尾に追加することをお勧めします。 次に例を示します。  
>   
> `<OutputPath>Bin\</OutputPath>`  
>   
> `OutputAssembly=="$(OutputPath)$(AssemblyName).exe" />`  
>   
> この形式が次の形式より推奨されます。  
>   
> `<OutputPath>Bin</OutputPath>`  
>   
> `OutputAssembly=="$(OutputPath)\$(AssemblyName).exe" />`  
  
## <a name="testing-the-build-properties"></a>ビルド プロパティをテストする  
 次に、ビルド プロパティで出力フォルダーとアプリケーション名を指定したプロジェクト ファイルを使用してアプリケーションをビルドします。  
  
#### <a name="to-test-the-build-properties"></a>ビルド プロパティをテストするには  
  
1. コマンドプロンプトで、「 **msbuild helloworld. .csproj/t: Build**」と入力します。  
  
     \Bin\ フォルダーが作成され、Visual C# コンパイラが呼び出されて、MSBuildSample アプリケーションが作成されて \Bin\ フォルダーに配置されます。  
  
2. \ Bin\ フォルダーが作成されていること、および MSBuildSample アプリケーションが含まれていることを確認するには、「 **Dir Bin**」と入力します。  
  
3. 「**Bin\MSBuildSample**」と入力してアプリケーションをテストします。  
  
     "**Hello, world!** " というメッセージが表示されます。  
  
## <a name="adding-build-targets"></a>ビルド ターゲットを追加する  
 次に、次の 2 つのターゲットをプロジェクト ファイルに追加します。  
  
- 古いファイルを削除する Clean ターゲット  
  
- `DependsOnTargets` 属性を使用して Build タスクの前に強制的に Clean タスクを実行する Rebuild ターゲット  
  
  ターゲットが複数になるので、Build ターゲットを既定のターゲットに設定します。  
  
#### <a name="to-add-build-targets"></a>ビルド ターゲットを追加するには  
  
1. プロジェクト ファイルで、Build ターゲットの直後に次の 2 つのターゲットを追加します。  
  
   ```  
   <Target Name="Clean" >  
     <Delete Files="$(OutputPath)$(AssemblyName).exe" />  
   </Target>  
   <Target Name="Rebuild" DependsOnTargets="Clean;Build" />  
   ```  
  
    Clean ターゲットは、Delete タスクを呼び出してアプリケーションを削除します。 Rebuild ターゲットは、Clean ターゲットと Build ターゲットの両方が実行されるまで実行されません。 Rebuild ターゲットにはタスクは含まれていませんが、このターゲットにより、Build ターゲットの前に Clean ターゲットが実行されるようになります。  
  
2. 次の `DefaultTargets` 属性を開始 `Project` 要素に追加します。  
  
   ```  
   <Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
   ```  
  
    これにより、Build ターゲットが既定のターゲットに設定されます。  
  
   プロジェクト ファイルのコードが次のようになります。  
  
```  
<Project DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
  <PropertyGroup>  
    <AssemblyName>MSBuildSample</AssemblyName>  
    <OutputPath>Bin\</OutputPath>  
  </PropertyGroup>  
  <ItemGroup>  
    <Compile Include="helloworld.cs" />  
  </ItemGroup>  
  <Target Name="Build">  
    <MakeDir Directories="$(OutputPath)" Condition="!Exists('$(OutputPath)')" />  
    <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />  
  </Target>  
  <Target Name="Clean" >  
    <Delete Files="$(OutputPath)$(AssemblyName).exe" />  
  </Target>  
  <Target Name="Rebuild" DependsOnTargets="Clean;Build" />  
</Project>  
```  
  
## <a name="testing-the-build-targets"></a>ビルド ターゲットをテストする  
 新しいビルド ターゲットを使用して、プロジェクト ファイルの以下の機能をテストします。  
  
- 既定のビルドをビルドする。  
  
- コマンド プロンプトでアプリケーション名を設定する。  
  
- 別のアプリケーションをビルドする前にアプリケーションを削除する。  
  
- 別のアプリケーションをビルドせずにアプリケーションを削除する。  
  
#### <a name="to-test-the-build-targets"></a>ビルド ターゲットをテストするには  
  
1. コマンドプロンプトで、「 **msbuild helloworld. .csproj/p: AssemblyName = 応答**」と入力します。  
  
     ターゲットを明示的に設定するために **/t** スイッチを使用していなかったため、MSBuild は既定のビルドターゲットを実行します。 **/P**スイッチはプロパティをオーバーライド `AssemblyName` し、新しい値を指定し `Greetings` ます。 これにより、Greetings.exe という新しいアプリケーションが \Bin\ フォルダーに作成されます。  
  
2. \ Bin\ フォルダーに MSBuildSample アプリケーションと新しい応答アプリケーションの両方が含まれていることを確認するには、「 **Dir Bin**」と入力します。  
  
3. 「**Bin\Greetings**」と入力して、Greetings アプリケーションをテストします。  
  
     "**Hello, world!** " というメッセージが表示されます。  
  
4. 「 **Msbuild helloworld. .csproj/t: clean**」と入力して、MSBuildSample アプリケーションを削除します。  
  
     Clean タスクが実行されて、`AssemblyName` プロパティの値が既定値の `MSBuildSample` になっているアプリケーションが削除されます。  
  
5. 「 **Msbuild helloworld. .csproj/t: clean/p: AssemblyName = 応答**」と入力して、応答アプリケーションを削除します。  
  
     Clean タスクが実行されて、**AssemblyName** プロパティの値が、指定した値 `Greetings` になっているアプリケーションが削除されます。  
  
6. \ Bin\ フォルダーが空になっていることを確認するには、「 **Dir Bin**」と入力します。  
  
7. 「**msbuild**」と入力します。  
  
     プロジェクト ファイルが指定されていませんが、現在のフォルダーにはプロジェクト ファイルが 1 つしかないため、helloworld.csproj ファイルがビルドされます。 その結果、\Bin\ フォルダーに MSBuildSample アプリケーションが作成されます。  
  
     \ Bin\ フォルダーに MSBuildSample アプリケーションが含まれていることを確認するには、「 **Dir Bin**」と入力します。  
  
## <a name="building-incrementally"></a>インクリメンタル ビルドを実行する  
 MSBuild では、ターゲットが依存しているソース ファイルやターゲット ファイルが変更された場合にのみターゲットをビルドすることができます。 ファイルが変更されているかどうかはファイルのタイム スタンプを使用して特定されます。  
  
#### <a name="to-build-incrementally"></a>インクリメンタル ビルドを実行するには  
  
1. プロジェクト ファイルで、開始 Build ターゲットに次の属性を追加します。  
  
    ```  
    Inputs="@(Compile)" Outputs="$(OutputPath)$(AssemblyName).exe"  
    ```  
  
     ここでは、`Compile` 項目グループに指定されている入力ファイルに Build ターゲットが依存していること、出力対象がアプリケーション ファイルであることを指定しています。  
  
     この結果、Build ターゲットのコードは次のようになります。  
  
    ```  
    <Target Name="Build" Inputs="@(Compile)" Outputs="$(OutputPath)$(AssemblyName).exe">  
      <MakeDir Directories="$(OutputPath)" Condition="!Exists('$(OutputPath)')" />  
      <Csc Sources="@(Compile)" OutputAssembly="$(OutputPath)$(AssemblyName).exe" />  
    </Target>  
    ```  
  
2. コマンドプロンプトで **「msbuild/v: d** 」と入力して、ビルドターゲットをテストします。  
  
     helloworld.csproj が既定のプロジェクト ファイルであること、Build が既定のターゲットであることに注意してください。  
  
     **/V: d**スイッチは、ビルド処理の詳細な説明を指定します。  
  
     以下の行が表示されます。  
  
     **すべての出力ファイルが入力ファイルに対して最新なので、ターゲット "Build" を省略します。**  
  
     **入力ファイル:HelloWorld.cs**  
  
     **出力ファイル:BinMSBuildSample.exe**  
  
     アプリケーションがビルドされてから変更されたソース ファイルがないため、Build ターゲットはスキップされます。  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例は、[!INCLUDE[csprcs](../includes/csprcs-md.md)] アプリケーションをコンパイルし、出力ファイル名を含むメッセージを記録するプロジェクト ファイルを示しています。  
  
### <a name="code"></a>コード  
  
```csharp  
<Project DefaultTargets = "Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
  
    <!-- Set the application name as a property -->  
    <PropertyGroup>  
        <appname>HelloWorldCS</appname>  
    </PropertyGroup>  
  
    <!-- Specify the inputs by type and file name -->  
    <ItemGroup>  
        <CSFile Include = "consolehwcs1.cs"/>  
    </ItemGroup>  
  
    <Target Name = "Compile">  
        <!-- Run the Visual C# compilation using input files of type CSFile -->  
        <CSC  
            Sources = "@(CSFile)"  
            OutputAssembly = "$(appname).exe">  
            <!-- Set the OutputAssembly attribute of the CSC task  
            to the name of the executable file that is created -->  
            <Output  
                TaskParameter = "OutputAssembly"  
                ItemName = "EXEFile" />  
        </CSC>  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
</Project>  
```  
  
### <a name="comments"></a>説明  
  
## <a name="example"></a>例  
  
### <a name="description"></a>説明  
 次の例は、[!INCLUDE[vbprvb](../includes/vbprvb-md.md)] アプリケーションをコンパイルし、出力ファイル名を含むメッセージを記録するプロジェクト ファイルを示しています。  
  
### <a name="code"></a>コード  
  
```vb  
<Project DefaultTargets = "Compile"  
    xmlns="http://schemas.microsoft.com/developer/msbuild/2003" >  
  
    <!-- Set the application name as a property -->  
    <PropertyGroup>  
        <appname>HelloWorldVB</appname>  
    </PropertyGroup>  
  
    <!-- Specify the inputs by type and file name -->  
    <ItemGroup>  
        <VBFile Include = "consolehwvb1.vb"/>  
    </ItemGroup>  
  
    <Target Name = "Compile">      
        <!-- Run the Visual Basic compilation using input files of type VBFile -->  
        <VBC  
            Sources = "@(VBFile)"  
            OutputAssembly= "$(appname).exe">  
            <!-- Set the OutputAssembly attribute of the VBC task  
            to the name of the executable file that is created -->  
            <Output  
                TaskParameter = "OutputAssembly"  
                ItemName = "EXEFile" />  
        </VBC>  
        <!-- Log the file name of the output file -->  
        <Message Text="The output file is @(EXEFile)"/>  
    </Target>  
</Project>  
```  
  
## <a name="whats-next"></a>次は何をすればよいですか?  
 このチュートリアルで説明した作業の大半は、Visual Studio で自動的に実行できます。 Visual Studio を使用して MSBuild プロジェクト ファイルを作成、編集、ビルド、およびテストする方法については、「[チュートリアル: MSBuild の使用](../msbuild/walkthrough-using-msbuild.md)」をご覧ください。  
  
## <a name="see-also"></a>参照  
[MSBuild の概要](msbuild.md)  
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)
