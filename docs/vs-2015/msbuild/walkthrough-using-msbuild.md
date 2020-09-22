---
title: 'チュートリアル: MSBuild の使用 | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tutorial
ms.assetid: b8a8b866-bb07-4abf-b9ec-0b40d281c310
caps.latest.revision: 34
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b6e77934f8e565800eb4a7a753df4beb3b003fbb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841609"
---
# <a name="walkthrough-using-msbuild"></a>チュートリアル: MSBuild の使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

MSBuild は Microsoft および Visual Studio のビルド プラットフォームです。 このチュートリアルでは、MSBuild のビルド ブロックについて説明し、MSBuild プロジェクトを記述、操作、およびデバッグする方法について説明します。 ここで学習する内容を以下に示します。  
  
- プロジェクト ファイルの作成と操作  
  
- ビルド プロパティの使用方法  
  
- ビルド項目の使用方法  
  
  MSBuild は、Visual Studio から実行することも、コマンド ウィンドウから実行することもできます。 このチュートリアルでは、Visual Studio を使用して MSBuild プロジェクト ファイルを作成し、 そのプロジェクト ファイルを Visual Studio で編集した後、コマンド ウィンドウを使用してプロジェクトをビルドして、結果を確認します。  
  
## <a name="creating-an-msbuild-project"></a>MSBuild プロジェクトの作成  
 Visual Studio プロジェクト システムは MSBuild に基づいています。 そのため、Visual Studio を使用して新しいプロジェクト ファイルを作成するのは簡単です。 このセクションでは、Visual C# プロジェクト ファイルを作成します。 代わりに、Visual Basic プロジェクト ファイルを作成することもできます。 このチュートリアルのコンテキストでは、2 つのプロジェクト ファイルにはわずかな違いしかありません。  
  
#### <a name="to-create-a-project-file"></a>プロジェクト ファイルを作成するには  
  
1. Visual Studio を開きます。  
  
2. **[ファイル]** メニューの **[新規作成]** をポイントし、 **[プロジェクト]** をクリックします。  
  
3. **[新しいプロジェクト]** ダイアログ ボックスで、プロジェクトの種類として Visual C# を選択し、**[Windows フォーム アプリケーション]** テンプレートをクリックします。 **[名前]** ボックスに「 `BuildApp`」と入力します。 **[場所]** ボックスにソリューションの場所を入力します (「`D:\`」など)。 それ以外は、既定値をそのまま使用します (**[ソリューションのディレクトリを作成]** はオン、**[ソース管理に追加]** はオフ、**[ソリューション名]** は `BuildApp`)。  
  
     **[OK]** をクリックして、プロジェクト ファイルを作成します。  
  
## <a name="examining-the-project-file"></a>プロジェクト ファイルの確認  
 前のセクションでは、Visual Studio を使用して Visual C# プロジェクト ファイルを作成しました。 このプロジェクト ファイルは、BuildApp という名前のプロジェクト ノードとして**ソリューション エクスプローラー**に表示されます。 Visual Studio Code エディターを使用してこのプロジェクト ファイルを確認できます。  
  
#### <a name="to-examine-the-project-file"></a>プロジェクト ファイルを確認するには  
  
1. **ソリューションエクスプローラー**で、buildapp というプロジェクトノードをクリックします。  
  
2. [ **プロパティ** ] ブラウザーで、" **プロジェクトファイル** " プロパティが buildapp になっていることを確認します。 プロジェクト ファイルはすべて、名前に "proj" というサフィックスが付いています。 Visual Basic プロジェクトを作成した場合は、プロジェクト ファイルの名前が "BuildApp.vbproj" になります。  
  
3. プロジェクト ノードを右クリックし、**[プロジェクトのアンロード]** をクリックします。  
  
4. プロジェクト ノードを再度右クリックし、 **[BuildApp.csproj の編集]** をクリックします。  
  
     コード エディターにプロジェクト ファイルが表示されます。  
  
## <a name="targets-and-tasks"></a>ターゲットとタスク  
 プロジェクト ファイルは XML 形式のファイルで、ルート ノードは [Project](../msbuild/project-element-msbuild.md) です。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<Project ToolsVersion="12.0" DefaultTargets="Build"  xmlns="http://schemas.microsoft.com/developer/msbuild/2003">  
```  
  
 Project 要素で xmlns 名前空間を指定する必要があります。  
  
 アプリケーションをビルドする作業は、[Target](../msbuild/target-element-msbuild.md) 要素と [Task](../msbuild/task-element-msbuild.md) 要素を使用して行われます。  
  
- タスクとは、作業の最小単位であり、ビルドの "原子" のようなものです。 タスクは独立した実行可能コンポーネントで、入力と出力を持つ場合もあります。 現在このプロジェクト ファイルで参照または定義されているタスクはありません。 後ほど、このプロジェクト ファイルにタスクを追加します。 詳細については、「[MSBuild タスク](../msbuild/msbuild-tasks.md)」をご覧ください。  
  
- ターゲットとは、一連のタスクに名前を付けたものです。 このプロジェクト ファイルには、末尾に BeforeBuild と AfterBuild という 2 つのターゲットがあります。これらは現在、HTML コメントに囲まれています。  
  
  ```  
  <Target Name="BeforeBuild">  
  </Target>  
  <Target Name="AfterBuild">  
  </Target>  
  ```  
  
   詳細については、「[MSBuild ターゲット](../msbuild/msbuild-targets.md)」をご覧ください。  
  
  Project ノードには、DefaultTargets という省略可能な属性があります。この属性は、ビルドする既定のターゲットを選択します。ここでは Build が選択されています。  
  
```  
<Project ToolsVersion="12.0" DefaultTargets="Build" ...  
```  
  
 Build ターゲットは、このプロジェクト ファイルには定義されていません。 [Import](../msbuild/import-element-msbuild.md) 要素を使用して Microsoft.CSharp.targets ファイルからインポートされています。  
  
```  
<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />  
```  
  
 インポートされたファイルは、実質的には、プロジェクト ファイルで参照されている場所に挿入されます。  
  
 MSBuild ではビルドのターゲットが追跡されるため、個々のターゲットが複数回ビルドされることはありません。  
  
## <a name="adding-a-target-and-a-task"></a>ターゲットとタスクの追加  
 プロジェクト ファイルにターゲットを追加し、 そのターゲットに、メッセージを出力するタスクを追加します。  
  
#### <a name="to-add-a-target-and-a-task"></a>ターゲットとタスクを追加するには  
  
1. プロジェクト ファイルの Import ステートメントの直後に以下の行を追加します。  
  
   ```  
   <Target Name="HelloWorld">  
   </Target>  
   ```  
  
    これにより、HelloWorld というターゲットが作成されます。 プロジェクト ファイルの編集時には Intellisense がサポートされます。  
  
2. セクションが次のようになるように、HelloWorld ターゲットに行を追加します。  
  
   ```  
   <Target Name="HelloWorld">  
     <Message Text="Hello"></Message>  <Message Text="World"></Message>  
   </Target>  
   ```  
  
3. プロジェクト ファイルを保存します。  
  
   Message タスクは、MSBuild に含まれている数多くのタスクの 1 つです。 使用可能なタスクと使用方法の詳細な一覧については、「 [タスクリファレンス](../msbuild/msbuild-task-reference.md)」を参照してください。  
  
   Message タスクは、Text 属性の文字列値を入力として受け取り、それを出力デバイスに表示します。 HelloWorld ターゲットでは、Message タスクが 2 回実行されます。1 回目の実行で "Hello" と表示され、2 回目の実行で "World" と表示されます。  
  
## <a name="building-the-target"></a>ターゲットのビルド  
 **Visual Studio コマンド プロンプト**から MSBuild を実行して、上で定義した HelloWorld ターゲットをビルドします。 ターゲットを選択するには、コマンド ライン スイッチの /target または /t を使用します。  
  
> [!NOTE]
> 以降では、**Visual Studio コマンド プロンプト**を**コマンド ウィンドウ**と呼びます。  
  
#### <a name="to-build-the-target"></a>ターゲットをビルドするには  
  
1. **[スタート]** ボタンをクリックし、**[すべてのプログラム]** をクリックします。 **[Visual Studio Tools]** フォルダーで **[Visual Studio コマンド プロンプト]** をクリックします。  
  
2. コマンド ウィンドウで、プロジェクト ファイルを含むフォルダー (この場合は D:\BuildApp\BuildApp) に移動します。  
  
3. コマンド ライン スイッチ /t:HelloWorld を使用して msbuild を実行します。 HelloWorld ターゲットが選択されてビルドされます。  
  
    ```  
    msbuild buildapp.csproj /t:HelloWorld  
    ```  
  
4. **コマンド ウィンドウ**で出力を確認します。 "Hello" と "World" の 2 つの行が表示されます。  
  
    ```  
    Hello  
    World  
    ```  
  
> [!NOTE]
> "`The target "HelloWorld" does not exist in the project`" と表示される場合は、コード エディターでプロジェクト ファイルが保存されていない可能性があります。 ファイルを保存して、やり直してください。  
  
 コード エディターとコマンド ウィンドウを交互に使用すると、プロジェクト ファイルを変更してすばやく結果を確認できます。  
  
> [!NOTE]
> コマンド ライン スイッチの /t を使用せずに msbuild を実行すると、Project 要素の DefaultTarget 属性で指定されているターゲット (この場合は "Build") がビルドされます。 これによって、Windows フォーム アプリケーションの BuildApp.exe がビルドされます。  
  
## <a name="build-properties"></a>ビルド プロパティ  
 ビルド プロパティは、ビルドを制御する名前と値のペアです。 このプロジェクト ファイルの先頭には、既にいくつかのビルド プロパティが定義されています。  
  
```  
<PropertyGroup>  
...  
  <ProductVersion>10.0.11107</ProductVersion>  
  <SchemaVersion>2.0</SchemaVersion>  
  <ProjectGuid>{30E3C9D5-FD86-4691-A331-80EA5BA7E571}</ProjectGuid>  
  <OutputType>WinExe</OutputType>  
...  
</PropertyGroup>  
```  
  
 すべてのプロパティは、PropertyGroup 要素の子要素です。 子要素の名前がプロパティの名前になり、子要素のテキスト要素がプロパティの値になります。 たとえば、オブジェクトに適用された  
  
```  
<TargetFrameworkVersion>v12.0</TargetFrameworkVersion>  
```  
  
 ここでは、TargetFrameworkVersion という名前のプロパティを定義して、文字列値 "v12.0" を割り当てています。  
  
 ビルド プロパティはいつでも再定義できます。 If  
  
```  
<TargetFrameworkVersion>v3.5</TargetFrameworkVersion>  
```  
  
 上の行が、プロジェクト ファイルの後半に含まれていたり、プロジェクト ファイルの後半でインポートされるファイルに含まれていたりした場合は、TargetFrameworkVersion に "v3.5" という新しい値が割り当てられます。  
  
## <a name="examining-a-property-value"></a>プロパティ値の確認  
 プロパティの値を取得するには、次の構文を使用します。ここで、PropertyName はプロパティの名前です。  
  
```  
$(PropertyName)  
```  
  
 この構文を使用して、プロジェクト ファイルのいくつかのプロパティを確認します。  
  
#### <a name="to-examine-a-property-value"></a>プロパティ値を確認するには  
  
1. コード エディターで、HelloWorld ターゲットを次のコードに置き換えます。  
  
    ```  
    <Target Name="HelloWorld">  
      <Message Text="Configuration is $(Configuration)" />  
      <Message Text="MSBuildToolsPath is $(MSBuildToolsPath)" />  
    </Target>  
    ```  
  
2. プロジェクト ファイルを保存します。  
  
3. **コマンド ウィンドウ**で、次の行を入力して実行します。  
  
    ```  
    msbuild buildapp.csproj /t:HelloWorld  
    ```  
  
4. 出力を調べます。 次の 2 つの行が表示されます (.NET Framework のバージョンが異なる場合もあります)。  
  
    ```  
    Configuration is Debug  
    MSBuildToolsPath is C:\Program Files\MSBuild\12.0\bin  
    ```  
  
> [!NOTE]
> これらの行が表示されない場合は、コード エディターでプロジェクト ファイルが保存されていない可能性があります。 ファイルを保存して、やり直してください。  
  
### <a name="conditional-properties"></a>条件付きプロパティ  
 Configuration など、多くのプロパティは、Condition 属性を使用して条件付きで定義されます。 条件付きプロパティは、条件が "true" と評価された場合にのみ定義 (または再定義) されます。 未定義のプロパティには、既定値として空の文字列が割り当てられます。 たとえば、オブジェクトに適用された  
  
```  
<Configuration   Condition=" '$(Configuration)' == '' ">Debug</Configuration>  
```  
  
 これは、"Configuration プロパティが定義されていない場合に、それを定義して値を 'Debug' に設定する" という意味になります。  
  
 Condition 属性は MSBuild のほぼすべての要素に設定できます。 Condition 属性の使用の詳細については、「[MSBuild Conditions (MSBuild の条件)](../msbuild/msbuild-conditions.md)」をご覧ください。  
  
### <a name="reserved-properties"></a>予約済みのプロパティ  
 MSBuild では、プロジェクト ファイルに関する情報や MSBuild のバイナリに関する情報を保持するために、いくつかのプロパティ名が予約されています。 たとえば、MSBuildToolsPath も予約済みのプロパティの 1 つです。 予約済みのプロパティは、他のプロパティと同じように $ 表記で参照できます。 詳細については、「 [方法: プロジェクトファイルの名前または場所を参照する](../msbuild/how-to-reference-the-name-or-location-of-the-project-file.md) 」および「 [MSBuild の予約済みおよび既知のプロパティ](../msbuild/msbuild-reserved-and-well-known-properties.md)」を参照してください。  
  
### <a name="environment-variables"></a>環境変数  
 プロジェクト ファイルで環境変数を参照する場合も、ビルド プロパティを参照するときと同じ方法を使用します。 たとえば、プロジェクト ファイルで PATH 環境変数を使用するには、$(Path) と記述します。 プロジェクト ファイルに、環境変数と同じ名前のプロパティが定義されている場合、環境変数の値はプロジェクト内のプロパティによってオーバーライドされます。 詳細については、「 [方法: ビルドで環境変数を使用する](../msbuild/how-to-use-environment-variables-in-a-build.md)」を参照してください。  
  
## <a name="setting-properties-from-the-command-line"></a>コマンドラインからのプロパティの設定  
 プロパティは、コマンド ライン スイッチの /property または /p を使用してコマンド ラインで定義することもできます。 プロジェクト ファイルに設定されたプロパティ値や環境変数として設定されたプロパティ値は、コマンド ラインから渡されたプロパティ値によってオーバーライドされます。  
  
#### <a name="to-set-a-property-value-from-the-command-line"></a>コマンド ラインからプロパティ値を設定するには  
  
1. **コマンド ウィンドウ**で、次の行を入力して実行します。  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld /p:Configuration=Release  
   ```  
  
2. 出力を調べます。 次の行が表示されます。  
  
   ```  
   Configuration is Release.  
   ```  
  
   Configuration プロパティが作成されて、値が "Release" に設定されます。  
  
## <a name="special-characters"></a>特殊文字  
 MSBuild プロジェクト ファイルでは、特定の文字が特殊な意味を持ちます。 そのような文字の例として、セミコロン (;) およびアスタリスク (*) があります。 これらの特殊文字をプロジェクト ファイル内でリテラルとして使用するには、構文 %xx でそれらの文字を指定する必要があります。xx は文字の ASCII 16 進値を表します。  
  
 Message タスクに変更を加えて、特殊文字を使用して Configuration プロパティの値を読みやすくします。  
  
#### <a name="to-use-special-characters-in-the-message-task"></a>Message タスクで特殊文字を使用するには  
  
1. コード エディターで、両方の Message タスクを次の行に置き換えます。  
  
   ```  
   <Message Text="%24(Configuration) is %22$(Configuration)%22" />  
   ```  
  
2. プロジェクト ファイルを保存します。  
  
3. **コマンド ウィンドウ**で、次の行を入力して実行します。  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. 出力を調べます。 次の行が表示されます。  
  
   ```  
   $(Configuration) is "Debug"  
   ```  
  
   詳細については、「 [MSBuild の特殊文字](../msbuild/msbuild-special-characters.md)」を参照してください。  
  
## <a name="build-items"></a>ビルド項目  
 項目とは、ファイル名など、ビルド システムへの入力として使用される情報です。 たとえば、ソース ファイルを表す項目のコレクションを Compile という名前のタスクに渡して、アセンブリにコンパイルする場合などがあります。  
  
 すべての項目は、ItemGroup 要素の子要素です。 子要素の名前が項目の名前になり、子要素の Include 属性の値が項目の値になります。 同じ名前を持つ項目の値は、その名前の項目の種類に収集されます。  たとえば、オブジェクトに適用された  
  
```  
<ItemGroup>  
    <Compile Include="Program.cs" />  
    <Compile Include="Properties\AssemblyInfo.cs" />  
</ItemGroup>  
```  
  
 ここでは、2 つの項目を含む項目グループを定義しています。 項目の種類 Compile には、"Program.cs" と "Properties\AssemblyInfo.cs" の 2 つの値があります。  
  
 次のコードでは、両方のファイルをセミコロンで区切って 1 つの Include 属性で宣言することで、同じ項目の種類を作成しています。  
  
```  
<ItemGroup>  
    <Compile Include="Program.cs;Properties\AssemblyInfo.cs" />  
</ItemGroup>  
```  
  
 詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。  
  
> [!NOTE]
> ファイル パスは、MSBuild プロジェクト ファイルを含むフォルダーに対する相対パスです。  
  
## <a name="examining-item-type-values"></a>項目の種類の値の確認  
 項目の種類の値を取得するには、次の構文を使用します。ここで、ItemType は項目の種類の名前です。  
  
```  
@(ItemType)  
```  
  
 この構文を使用して、プロジェクト ファイルの項目の種類 Compile を確認します。  
  
#### <a name="to-examine-item-type-values"></a>項目の種類の値を確認するには  
  
1. コード エディターで、HelloWorld ターゲット タスクを次のコードに置き換えます。  
  
   ```  
   <Target Name="HelloWorld">  
     <Message Text="Compile item type contains @(Compile)" />  
   </Target>  
   ```  
  
2. プロジェクト ファイルを保存します。  
  
3. **コマンド ウィンドウ**で、次の行を入力して実行します。  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. 出力を調べます。 次の長い行が表示されます。  
  
   ```  
   Compile item type contains Form1.cs;Form1.Designer.cs;Program.cs;Properties\AssemblyInfo.cs;Properties\Resources.Designer.cs;Properties\Settings.Designer.cs  
   ```  
  
   項目の種類の値は、既定ではセミコロンで区切られます。  
  
   項目の種類の区切り記号を変更するには、次の構文を使用します。ここで、ItemType は項目の種類、Separator は 1 文字以上の区切り記号です。  
  
```  
@(ItemType, Separator)  
```  
  
 Message タスクに変更を加えて、復帰と改行 (%0A%0D) を使用して Compile 項目を 1 行に 1 つずつ表示します。  
  
#### <a name="to-display-item-type-values-one-per-line"></a>項目の種類の値を 1 行に 1 つずつ表示するには  
  
1. コード エディターで、Message タスクを次の行に置き換えます。  
  
    ```  
    <Message Text="Compile item type contains @(Compile, '%0A%0D')" />  
    ```  
  
2. プロジェクト ファイルを保存します。  
  
3. **コマンド ウィンドウ**で、次の行を入力して実行します。  
  
     `msbuild buildapp.csproj /t:HelloWorld`  
  
4. 出力を調べます。 次の行が表示されます。  
  
    ```  
    Compile item type contains Form1.cs  
    Form1.Designer.cs  
    Program.cs  
    Properties\AssemblyInfo.cs  
    Properties\Resources.Designer.cs  
    Properties\Settings.Designer.cs  
    ```  
  
### <a name="include-exclude-and-wildcards"></a>Include、Exclude、およびワイルドカード  
 Include 属性でワイルドカード ("*"、"\*\*"、および "?") を使用して、項目を項目の種類に追加できます。 たとえば、オブジェクトに適用された  
  
```  
<Photos Include="images\*.jpeg" />  
```  
  
 この例では、images フォルダーにある拡張子が ".jpeg" のすべてのファイルが項目の種類 Photos に追加されます。もう 1 つ例を見てましょう。  
  
```  
<Photos Include="images\**.jpeg" />  
```  
  
 この例では、images フォルダーとそのすべてのサブフォルダーにある拡張子が ".jpeg" のすべてのファイルが項目の種類 Photos に追加されます。 その他の例については、「 [方法: ビルドするファイルを選択する](../msbuild/how-to-select-the-files-to-build.md)」を参照してください。  
  
 項目を宣言すると、それらが項目の種類に追加されます。 たとえば、オブジェクトに適用された  
  
```  
<Photos Include="images\*.jpeg" />  
<Photos Include="images\*.gif" />  
```  
  
 この例では、image フォルダーにある拡張子が ".jpeg" または ".gif" のすべてのファイルを含む項目の種類 Photos が作成されます。 次の行も同じ結果をもたらします。  
  
```  
<Photos Include="images\*.jpeg;images\*.gif" />  
```  
  
 項目の種類から項目を除外するには、Exclude 属性を使用します。 たとえば、オブジェクトに適用された  
  
```  
<Compile Include="*.cs" Exclude="*Designer*">  
```  
  
 この例では、拡張子が ".cs" のすべてのファイルが項目の種類 Compile に追加されますが、名前に文字列 "Designer" が含まれているファイルは除外されます。 その他の例については、「 [方法: ビルドからファイルを除外する](../msbuild/how-to-exclude-files-from-the-build.md)」を参照してください。  
  
 Exclude 属性は、同一の項目要素内にある Include 属性によって追加された項目のみに作用します。 たとえば、オブジェクトに適用された  
  
```  
<Compile Include="*.cs" />  
<Compile Include="*.res" Exclude="Form1.cs">  
```  
  
 この例では、Form1.cs ファイルは前の項目要素で追加されているため、除外されません。  
  
##### <a name="to-include-and-exclude-items"></a>項目を追加および除外するには  
  
1. コード エディターで、Message タスクを次の行に置き換えます。  
  
    ```  
    <Message Text="Compile item type contains @(XFiles)" />  
    ```  
  
2. Import 要素の直後に次の項目グループを追加します。  
  
    ```  
    <ItemGroup>  
       <XFiles Include="*.cs;properties/*.resx" Exclude="*Designer*" />  
    </ItemGroup>  
    ```  
  
3. プロジェクト ファイルを保存します。  
  
4. **コマンド ウィンドウ**で、次の行を入力して実行します。  
  
    ```  
    msbuild buildapp.csproj /t:HelloWorld  
    ```  
  
5. 出力を調べます。 次の行が表示されます。  
  
    ```  
    Compile item type contains Form1.cs;Program.cs;Properties/Resources.resx  
    ```  
  
## <a name="item-metadata"></a>アイテム メタデータ  
 項目には、Include および Exclude 属性から収集した情報に加えて、メタデータが含まれます。 このメタデータは、項目の値だけでなく項目に関する詳細情報を必要とするタスクで使用できます。  
  
 アイテム メタデータは、そのメタデータ名を名前に持つ要素を、項目の子として作成することにより、プロジェクト ファイルで宣言します。 項目には 0 以上のメタデータ値を指定できます。 たとえば、次の CSFile 項目には、値 "Fr" の Culture メタデータがあります。  
  
```  
<ItemGroup>  
    <CSFile Include="main.cs">  
        <Culture>Fr</Culture>  
    </CSFile>  
</ItemGroup>  
```  
  
 項目の種類のメタデータ値を取得するには、次の構文を使用します。ここで、ItemType は項目の種類の名前、MetaDataName はメタデータの名前です。  
  
```  
%(ItemType.MetaDataName)  
```  
  
#### <a name="to-examine-item-metadata"></a>項目メタデータを確認するには  
  
1. コード エディターで、Message タスクを次の行に置き換えます。  
  
   ```  
   <Message Text="Compile.DependentUpon: %(Compile.DependentUpon)" />  
   ```  
  
2. プロジェクト ファイルを保存します。  
  
3. **コマンド ウィンドウ**で、次の行を入力して実行します。  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. 出力を調べます。 次の行が表示されます。  
  
   ```  
   Compile.DependentUpon:  
   Compile.DependentUpon: Form1.cs  
   Compile.DependentUpon: Resources.resx  
   Compile.DependentUpon: Settings.settings  
   ```  
  
   "Compile.DependentUpon" というフレーズが何回か出現しています。 ターゲット内でメタデータを使用する際にこの構文を使用すると、"バッチ処理" が行われます。 バッチ処理では、ターゲット内のタスクが各メタデータ値について 1 回だけ実行されます。 これは、一般的なプログラミング構造の "for ループ" に相当します。 詳細については、「[MSBuild バッチ](../msbuild/msbuild-batching.md)」をご覧ください。  
  
### <a name="well-known-metadata"></a>既知のメタデータ  
 項目リストに追加した項目には、既知のメタデータが割り当てられます。 たとえば、項目のファイル名を返す %(Filename) などです。 既知のメタデータの完全な一覧については、「 [既知の項目メタデータ](../msbuild/msbuild-well-known-item-metadata.md)」を参照してください。  
  
##### <a name="to-examine-well-known-metadata"></a>既知のメタデータを確認するには  
  
1. コード エディターで、Message タスクを次の行に置き換えます。  
  
   ```  
   <Message Text="Compile Filename: %(Compile.Filename)" />  
   ```  
  
2. プロジェクト ファイルを保存します。  
  
3. **コマンド ウィンドウ**で、次の行を入力して実行します。  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. 出力を調べます。 次の行が表示されます。  
  
   ```  
   Compile Filename: Form1  
   Compile Filename: Form1.Designer  
   Compile Filename: Program  
   Compile Filename: AssemblyInfo  
   Compile Filename: Resources.Designer  
   Compile Filename: Settings.Designer  
   ```  
  
   この例を前の例と比較すると、DependentUpon メタデータは項目の種類 Compile のすべての項目には含まれていないのに対し、既知のメタデータ Filename はすべての項目に含まれていることがわかります。  
  
### <a name="metadata-transformations"></a>メタデータの変換  
 既存の項目リストを新しい項目リストに変換できます。 項目リストを変換するには、次の構文を使用します。ここで、ItemType は項目の種類の名前、MetadataName はメタデータの名前です。  
  
```  
@(ItemType -> '%(MetadataName)')  
```  
  
 たとえば、`@(SourceFiles -> '%(Filename).obj')` のような式を使用すると、ソース ファイルの項目リストをオブジェクト ファイルのコレクションに変換できます。 詳細については、「[MSBuild 変換](../msbuild/msbuild-transforms.md)」をご覧ください。  
  
##### <a name="to-transform-items-using-metadata"></a>メタデータを使用して項目を変換するには  
  
1. コード エディターで、Message タスクを次の行に置き換えます。  
  
   ```  
   <Message Text="Backup files: @(Compile->'%(filename).bak')" />  
   ```  
  
2. プロジェクト ファイルを保存します。  
  
3. **コマンド ウィンドウ**で、次の行を入力して実行します。  
  
   ```  
   msbuild buildapp.csproj /t:HelloWorld  
   ```  
  
4. 出力を調べます。 次の行が表示されます。  
  
   ```  
   Backup files: Form1.bak;Form1.Designer.bak;Program.bak;AssemblyInfo.bak;Resources.Designer.bak;Settings.Designer.bak  
   ```  
  
   この構文で表されるメタデータではバッチ処理は行われないことに注意してください。  
  
## <a name="whats-next"></a>次は何をすればよいですか?  
 単純なプロジェクトファイルを一度に1ステップずつ作成する方法については、 [「チュートリアル: MSBuild プロジェクトファイルを最初から作成](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)する」を参照してください。  
  
## <a name="see-also"></a>参照
[MSBuild の概要](msbuild.md)  
 [MSBuild リファレンス](../msbuild/msbuild-reference.md)
