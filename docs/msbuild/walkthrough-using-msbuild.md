---
title: 'チュートリアル: MSBuild の使用 | Microsoft Docs'
ms.date: 03/20/2019
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, tutorial
ms.assetid: b8a8b866-bb07-4abf-b9ec-0b40d281c310
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: c3e3f0ec3938136370daf15954d8c13da5905ba4
ms.sourcegitcommit: 96737c54162f5fd5c97adef9b2d86ccc660b2135
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2020
ms.locfileid: "77631082"
---
# <a name="walkthrough-use-msbuild"></a>チュートリアル: MSBuild の使用

MSBuild は Microsoft および Visual Studio のビルド プラットフォームです。 このチュートリアルでは、MSBuild のビルド ブロックについて説明し、MSBuild プロジェクトを記述、操作、およびデバッグする方法について説明します。 ここで学習する内容を以下に示します。

- プロジェクト ファイルの作成と操作

- ビルド プロパティの使用方法

- ビルド項目の使用方法

MSBuild は、Visual Studio から実行することも、**コマンド ウィンドウ**から実行することもできます。 このチュートリアルでは、Visual Studio を使用して MSBuild プロジェクト ファイルを作成し、 そのプロジェクト ファイルを Visual Studio で編集した後、**コマンド ウィンドウ**を使用してプロジェクトをビルドして、結果を確認します。

## <a name="create-an-msbuild-project"></a>MSBuild プロジェクトの作成

 Visual Studio プロジェクト システムは MSBuild に基づいています。 そのため、Visual Studio を使用して新しいプロジェクト ファイルを作成するのは簡単です。 このセクションでは、Visual C# プロジェクト ファイルを作成します。 代わりに、Visual Basic プロジェクト ファイルを作成することもできます。 このチュートリアルのコンテキストでは、2 つのプロジェクト ファイルにはわずかな違いしかありません。

**プロジェクト ファイルを作成するには**

1. Visual Studio を開き、プロジェクトを作成します。

    ::: moniker range=">=vs-2019"
    **Esc** キーを押してスタート ウィンドウを閉じます。 **Ctrl + Q** キーを押して検索ボックスを開き、「**winforms**」と入力します。 **[新しい Windows フォーム アプリの作成 (.NET Framework)]** を選択します。 表示されたダイアログ ボックスで、 **[作成]** を選択します。

    **[名前]** ボックスに「 `BuildApp`」と入力します。 **[場所]** ボックスにソリューションの場所を入力します (「*D:\\* 」など)。 **[ソリューション]** 、 **[ソリューション名]** (**BuildApp**)、および **[フレームワーク]** の既定値をそのまま使用します。
    ::: moniker-end
    ::: moniker range="vs-2017"
    上部のメニュー バーから、 **[ファイル]**  >  **[新規作成]**  >  **[プロジェクト]** の順に選択します。 **[新しいプロジェクト]** ダイアログ ボックスの左側のウィンドウで **[Visual C#]**  >  **[Windows Desktop]** を展開し、 **[Windows フォーム アプリ (.NET Framework)]** を選択します。 次に、 **[OK]** を選択します。

    **[名前]** ボックスに「 `BuildApp`」と入力します。 **[場所]** ボックスにソリューションの場所を入力します (「*D:\\* 」など)。 それ以外は、既定値をそのまま使用します ( **[ソリューションのディレクトリを作成]** はオン、 **[ソース管理に追加]** はオフ、 **[ソリューション名]** は **BuildApp**)。
    ::: moniker-end

1. **[OK]** または **[作成]** をクリックして、プロジェクト ファイルを作成します。

## <a name="examine-the-project-file"></a>プロジェクト ファイルを確認する

 前のセクションでは、Visual Studio を使用して Visual C# プロジェクト ファイルを作成しました。 このプロジェクト ファイルは、BuildApp という名前のプロジェクト ノードとして**ソリューション エクスプローラー**に表示されます。 Visual Studio Code エディターを使用してこのプロジェクト ファイルを確認できます。

**プロジェクト ファイルを確認するには**

1. **ソリューション エクスプローラー**で、**BuildApp** というプロジェクト ノードをクリックします。

2. **プロパティ** ブラウザーで、 **[プロジェクト ファイル]** プロパティが *BuildApp.csproj* になっていることを確認します。 プロジェクト ファイルはすべて、名前に *proj* というサフィックスが付いています。 Visual Basic プロジェクトを作成した場合は、プロジェクト ファイルの名前が *BuildApp.vbproj* になります。

3. プロジェクト ノードを右クリックし、 **[プロジェクトのアンロード]** をクリックします。

4. プロジェクト ノードを再度右クリックし、 **[BuildApp.csproj の編集]** をクリックします。

     コード エディターにプロジェクト ファイルが表示されます。

## <a name="targets-and-tasks"></a>ターゲットとタスク

プロジェクト ファイルは XML 形式のファイルで、ルート ノードは [Project](../msbuild/project-element-msbuild.md) です。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="15.0"  xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
```

Project 要素で xmlns 名前空間を指定する必要があります。 `ToolsVersion` が新しいプロジェクトに存在する場合は、"15.0" でなければなりません。

アプリケーションをビルドする作業は、[Target](../msbuild/target-element-msbuild.md) 要素と [Task](../msbuild/task-element-msbuild.md) 要素を使用して行われます。

- タスクとは、作業の最小単位であり、ビルドの "原子" のようなものです。 タスクは独立した実行可能コンポーネントで、入力と出力を持つ場合もあります。 現在このプロジェクト ファイルで参照または定義されているタスクはありません。 後ほど、このプロジェクト ファイルにタスクを追加します。 詳細については、「[MSBuild タスク](../msbuild/msbuild-tasks.md)」をご覧ください。

- ターゲットとは、一連のタスクに名前を付けたものです。 詳細については、「[MSBuild ターゲット](../msbuild/msbuild-targets.md)」をご覧ください。

既定のターゲットは、このプロジェクト ファイルでは定義されていません。 代わりに、インポートされるプロジェクトで指定されています。 [Import](../msbuild/import-element-msbuild.md) 要素は、インポートされたプロジェクトを指定します。 たとえば、C# プロジェクトでは、既定のターゲットが *Microsoft.CSharp.targets* ファイルからインポートされます。

```xml
<Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
```

インポートされたファイルは、実質的には、プロジェクト ファイルで参照されている場所に挿入されます。

> [!NOTE]
> .NET Core などの一部のプロジェクトの種類では、`ToolsVersion` の代わりに `Sdk` を使う簡素化されたスキーマが使われます。 これらのプロジェクトには、暗黙的なインポートと、異なる既定の属性値があります。

MSBuild ではビルドのターゲットが追跡されるため、個々のターゲットが複数回ビルドされることはありません。

## <a name="add-a-target-and-a-task"></a>ターゲットとタスクを追加する

 プロジェクト ファイルにターゲットを追加し、 そのターゲットに、メッセージを出力するタスクを追加します。

**ターゲットとタスクを追加するには**

1. プロジェクト ファイルの Import ステートメントの直後に以下の行を追加します。

    ```xml
    <Target Name="HelloWorld">
    </Target>
    ```

     これにより、HelloWorld というターゲットが作成されます。 プロジェクト ファイルの編集時には IntelliSense がサポートされます。

2. セクションが次のようになるように、HelloWorld ターゲットに行を追加します。

    ```xml
    <Target Name="HelloWorld">
      <Message Text="Hello"></Message>  <Message Text="World"></Message>
    </Target>
    ```

3. プロジェクト ファイルを保存します。

Message タスクは、MSBuild に含まれている数多くのタスクの 1 つです。 使用可能なすべてのタスクと使用法については、「[タスク リファレンス](../msbuild/msbuild-task-reference.md)」をご覧ください。

Message タスクは、Text 属性の文字列値を入力として受け取り、それを出力デバイスに表示します。 HelloWorld ターゲットでは、Message タスクが 2 回実行されます。1 回目の実行で "Hello" と表示され、2 回目の実行で "World" と表示されます。

## <a name="build-the-target"></a>ターゲットをビルドする

 Visual Studio の**開発者コマンド プロンプト**から MSBuild を実行して、上で定義した HelloWorld ターゲットをビルドします。 ターゲットを選択するには、コマンド ライン スイッチの -target または -t を使用します。

> [!NOTE]
> 以降では、**開発者コマンド プロンプト**を**コマンド ウィンドウ**と呼びます。

**ターゲットをビルドするには**

1. **コマンド ウィンドウ**を開きます。

   (Windows 10) タスクバーの検索ボックスに、`dev` や `developer command prompt` など、ツールの名前を入力します。 検索パターンに一致する、インストールされているアプリの一覧が表示されます。

   手動で検索する必要がある場合、ファイルは *<visualstudio installation folder\>\<バージョン>\Common7\Tools* フォルダー内の *LaunchDevCmd.bat* です。

2. コマンド ウィンドウで、プロジェクト ファイルを含むフォルダー (この場合は *D:\BuildApp\BuildApp*) に移動します。

3. コマンド ライン スイッチ -t:HelloWorld を使用して msbuild を実行します。 HelloWorld ターゲットが選択されてビルドされます。

    ```cmd
    msbuild buildapp.csproj -t:HelloWorld
    ```

4. **コマンド ウィンドウ**で出力を確認します。 "Hello" と "World" の 2 つの行が表示されます。

    ```
    Hello
    World
    ```

> [!NOTE]
> "`The target "HelloWorld" does not exist in the project`" と表示される場合は、コード エディターでプロジェクト ファイルが保存されていない可能性があります。 ファイルを保存して、やり直してください。

 コード エディターとコマンド ウィンドウを交互に使用すると、プロジェクト ファイルを変更してすばやく結果を確認できます。

## <a name="build-properties"></a>ビルド プロパティ

 ビルド プロパティは、ビルドを制御する名前と値のペアです。 このプロジェクト ファイルの先頭には、既にいくつかのビルド プロパティが定義されています。

```xml
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

```xml
<TargetFrameworkVersion>v15.0</TargetFrameworkVersion>
```

 ここでは、TargetFrameworkVersion という名前のプロパティを定義して、文字列値 "v15.0" を割り当てています。

 ビルド プロパティはいつでも再定義できます。 If

```xml
<TargetFrameworkVersion>v3.5</TargetFrameworkVersion>
```

 上の行が、プロジェクト ファイルの後半に含まれていたり、プロジェクト ファイルの後半でインポートされるファイルに含まれていたりした場合は、TargetFrameworkVersion に "v3.5" という新しい値が割り当てられます。

## <a name="examine-a-property-value"></a>プロパティ値を確認する

 プロパティの値を取得するには、次の構文を使用します。ここで、PropertyName はプロパティの名前です。

```xml
$(PropertyName)
```

 この構文を使用して、プロジェクト ファイルのいくつかのプロパティを確認します。

**プロパティ値を確認するには**

1. コード エディターで、HelloWorld ターゲットを次のコードに置き換えます。

    ```xml
    <Target Name="HelloWorld">
      <Message Text="Configuration is $(Configuration)" />
      <Message Text="MSBuildToolsPath is $(MSBuildToolsPath)" />
    </Target>
    ```

2. プロジェクト ファイルを保存します。

3. **コマンド ウィンドウ**で、次の行を入力して実行します。

    ```cmd
    msbuild buildapp.csproj -t:HelloWorld
    ```

4. 出力を調べます。 次の 2 つの行が表示されます (.NET Framework のバージョンが異なる場合もあります)。

    ::: moniker range=">=vs-2019"

    ```
    Configuration is Debug
    MSBuildToolsPath is C:\Program Files (x86)\Microsoft Visual Studio\2019\<Visual Studio SKU>\MSBuild\15.0\Bin
    ```

    ::: moniker-end
    ::: moniker range="vs-2017"

    ```
    Configuration is Debug
    MSBuildToolsPath is C:\Program Files (x86)\Microsoft Visual Studio\2017\<Visual Studio SKU>\MSBuild\15.0\Bin
    ```

    ::: moniker-end

> [!NOTE]
> これらの行が表示されない場合は、コード エディターでプロジェクト ファイルが保存されていない可能性があります。 ファイルを保存して、やり直してください。

### <a name="conditional-properties"></a>条件付きプロパティ

 Configuration など、多くのプロパティは、Condition 属性を使用して条件付きで定義されます。 条件付きプロパティは、条件が "true" と評価された場合にのみ定義 (または再定義) されます。 未定義のプロパティには、既定値として空の文字列が割り当てられます。 たとえば、オブジェクトに適用された

```xml
<Configuration   Condition=" '$(Configuration)' == '' ">Debug</Configuration>
```

 これは、"Configuration プロパティが定義されていない場合に、それを定義して値を 'Debug' に設定する" という意味になります。

 Condition 属性は MSBuild のほぼすべての要素に設定できます。 Condition 属性の使用の詳細については、「[MSBuild Conditions (MSBuild の条件)](../msbuild/msbuild-conditions.md)」をご覧ください。

### <a name="reserved-properties"></a>予約済みのプロパティ

 MSBuild では、プロジェクト ファイルに関する情報や MSBuild のバイナリに関する情報を保持するために、いくつかのプロパティ名が予約されています。 たとえば、MSBuildToolsPath も予約済みのプロパティの 1 つです。 予約済みのプロパティは、他のプロパティと同じように $ 表記で参照できます。 詳細については、[プロジェクト ファイルの名前または場所を参照する](../msbuild/how-to-reference-the-name-or-location-of-the-project-file.md)」および「[MSBuild の予約済みおよび既知のプロパティ](../msbuild/msbuild-reserved-and-well-known-properties.md)」をご覧ください。

### <a name="environment-variables"></a>環境変数

 プロジェクト ファイルで環境変数を参照する場合も、ビルド プロパティを参照するときと同じ方法を使用します。 たとえば、プロジェクト ファイルで PATH 環境変数を使用するには、$(Path) と記述します。 プロジェクト ファイルに、環境変数と同じ名前のプロパティが定義されている場合、環境変数の値はプロジェクト内のプロパティによってオーバーライドされます。 詳細については、[ビルドで環境変数を使用する](../msbuild/how-to-use-environment-variables-in-a-build.md)」をご覧ください。

## <a name="set-properties-from-the-command-line"></a>コマンドラインからプロパティを設定する

 プロパティは、コマンド ライン スイッチの -property または -p を使用してコマンド ラインで定義することもできます。 プロジェクト ファイルに設定されたプロパティ値や環境変数として設定されたプロパティ値は、コマンド ラインから渡されたプロパティ値によってオーバーライドされます。

**コマンド ラインからプロパティ値を設定するには**

1. **コマンド ウィンドウ**で、次の行を入力して実行します。

    ```cmd
    msbuild buildapp.csproj -t:HelloWorld -p:Configuration=Release
    ```

2. 出力を調べます。 次の行が表示されます。

    ```
    Configuration is Release.
    ```

Configuration プロパティが作成されて、値が "Release" に設定されます。

## <a name="special-characters"></a>特殊文字

 MSBuild プロジェクト ファイルでは、特定の文字が特殊な意味を持ちます。 そのような文字の例として、セミコロン (;) およびアスタリスク (*) があります。 これらの特殊文字をプロジェクト ファイル内でリテラルとして使用するには、構文 %\<xx> でそれらの文字を指定する必要があります。ここで、\<xx> は文字の ASCII 16 進値を表します。

 Message タスクに変更を加えて、特殊文字を使用して Configuration プロパティの値を読みやすくします。

**Message タスクで特殊文字を使用するには**

1. コード エディターで、両方の Message タスクを次の行に置き換えます。

    ```xml
    <Message Text="%24(Configuration) is %22$(Configuration)%22" />
    ```

2. プロジェクト ファイルを保存します。

3. **コマンド ウィンドウ**で、次の行を入力して実行します。

    ```cmd
    msbuild buildapp.csproj -t:HelloWorld
    ```

4. 出力を調べます。 次の行が表示されます。

    ```
    $(Configuration) is "Debug"
    ```

詳細については、「[MSBuild の特殊文字](../msbuild/msbuild-special-characters.md)」をご覧ください。

## <a name="build-items"></a>ビルド項目

 項目とは、ファイル名など、ビルド システムへの入力として使用される情報です。 たとえば、ソース ファイルを表す項目のコレクションを Compile という名前のタスクに渡して、アセンブリにコンパイルする場合などがあります。

 すべての項目は、ItemGroup 要素の子要素です。 子要素の名前が項目の名前になり、子要素の Include 属性の値が項目の値になります。 同じ名前を持つ項目の値は、その名前の項目の種類に収集されます。  たとえば、オブジェクトに適用された

```xml
<ItemGroup>
    <Compile Include="Program.cs" />
    <Compile Include="Properties\AssemblyInfo.cs" />
</ItemGroup>
```

 ここでは、2 つの項目を含む項目グループを定義しています。 Compile 項目の種類には、2 つの値があります。*Program.cs* と *Properties\AssemblyInfo.cs* です。

 次のコードでは、両方のファイルをセミコロンで区切って 1 つの Include 属性で宣言することで、同じ項目の種類を作成しています。

```xml
<ItemGroup>
    <Compile Include="Program.cs;Properties\AssemblyInfo.cs" />
</ItemGroup>
```

詳細については、「[MSBuild 項目](../msbuild/msbuild-items.md)」をご覧ください。

> [!NOTE]
> ファイル パスは、MSBuild プロジェクト ファイルを含むフォルダーに対する相対パスです。

## <a name="examine-item-type-values"></a>項目の種類の値を確認する

 項目の種類の値を取得するには、次の構文を使用します。ここで、ItemType は項目の種類の名前です。

```xml
@(ItemType)
```

 この構文を使用して、プロジェクト ファイルの項目の種類 Compile を確認します。

**項目の種類の値を確認するには**

1. コード エディターで、HelloWorld ターゲット タスクを次のコードに置き換えます。

    ```xml
    <Target Name="HelloWorld">
      <Message Text="Compile item type contains @(Compile)" />
    </Target>
    ```

2. プロジェクト ファイルを保存します。

3. **コマンド ウィンドウ**で、次の行を入力して実行します。

    ```cmd
    msbuild buildapp.csproj -t:HelloWorld
    ```

4. 出力を調べます。 次の長い行が表示されます。

    ```
    Compile item type contains Form1.cs;Form1.Designer.cs;Program.cs;Properties\AssemblyInfo.cs;Properties\Resources.Designer.cs;Properties\Settings.Designer.cs
    ```

項目の種類の値は、既定ではセミコロンで区切られます。

項目の種類の区切り記号を変更するには、次の構文を使用します。ここで、ItemType は項目の種類、Separator は 1 文字以上の区切り記号です。

```xml
@(ItemType, Separator)
```

Message タスクに変更を加えて、復帰と改行 (%0A%0D) を使用して Compile 項目を 1 行に 1 つずつ表示します。

**項目の種類の値を 1 行に 1 つずつ表示するには**

1. コード エディターで、Message タスクを次の行に置き換えます。

    ```xml
    <Message Text="Compile item type contains @(Compile, '%0A%0D')" />
    ```

2. プロジェクト ファイルを保存します。

3. **コマンド ウィンドウ**で、次の行を入力して実行します。

    ```cmd
    msbuild buildapp.csproj -t:HelloWorld
    ```

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

```xml
<Photos Include="images\*.jpeg" />
```

 この例では、*images* フォルダーにある拡張子が *.jpeg* のすべてのファイルが項目の種類 Photos に追加されます。もう 1 つ例を見てましょう。

```xml
<Photos Include="images\**\*.jpeg" />
```

 この例では、*images* フォルダーとそのすべてのサブフォルダーにある拡張子が *.jpeg* のすべてのファイルが項目の種類 Photos に追加されます。 その他の例については、「[方法:ビルドするファイルを選択する](../msbuild/how-to-select-the-files-to-build.md)」をご覧ください。

 項目を宣言すると、それらが項目の種類に追加されます。 たとえば、オブジェクトに適用された

```xml
<Photos Include="images\*.jpeg" />
<Photos Include="images\*.gif" />
```

 この例では、*image* フォルダーにある拡張子が *.jpeg* または *.gif* のすべてのファイルを含む、Photos という名前の項目の種類 が作成されます。 次の行も同じ結果をもたらします。

```xml
<Photos Include="images\*.jpeg;images\*.gif" />
```

 項目の種類から項目を除外するには、Exclude 属性を使用します。 たとえば、オブジェクトに適用された

```xml
<Compile Include="*.cs" Exclude="*Designer*">
```

 この例では、拡張子が *.cs* のすべてのファイルが項目の種類 Compile に追加されますが、名前に文字列 *Designer* が含まれているファイルは除外されます。 その他の例については、「[方法:ビルドからファイルを除外する](../msbuild/how-to-exclude-files-from-the-build.md)」をご覧ください。

Exclude 属性は、同一の項目要素内にある Include 属性によって追加された項目のみに作用します。 たとえば、オブジェクトに適用された

```xml
<Compile Include="*.cs" />
<Compile Include="*.res" Exclude="Form1.cs">
```

この例では、*Form1.cs* ファイルは前の項目要素で追加されているため、除外されません。

**項目を追加および除外するには**

1. コード エディターで、Message タスクを次の行に置き換えます。

    ```xml
    <Message Text="XFiles item type contains @(XFiles)" />
    ```

2. Import 要素の直後に次の項目グループを追加します。

    ```xml
    <ItemGroup>
       <XFiles Include="*.cs;properties/*.resx" Exclude="*Designer*" />
    </ItemGroup>
    ```

3. プロジェクト ファイルを保存します。

4. **コマンド ウィンドウ**で、次の行を入力して実行します。

    ```cmd
    msbuild buildapp.csproj -t:HelloWorld
    ```

5. 出力を調べます。 次の行が表示されます。

    ```
    XFiles item type contains Form1.cs;Program.cs;Properties/Resources.resx
    ```

## <a name="item-metadata"></a>項目メタデータ

 項目には、Include および Exclude 属性から収集した情報に加えて、メタデータが含まれます。 このメタデータは、項目の値だけでなく項目に関する詳細情報を必要とするタスクで使用できます。

 アイテム メタデータは、そのメタデータ名を名前に持つ要素を、項目の子として作成することにより、プロジェクト ファイルで宣言します。 項目には 0 以上のメタデータ値を指定できます。 たとえば、次の CSFile 項目には、値 "Fr" の Culture メタデータがあります。

```xml
<ItemGroup>
    <CSFile Include="main.cs">
        <Culture>Fr</Culture>
    </CSFile>
</ItemGroup>
```

 項目の種類のメタデータ値を取得するには、次の構文を使用します。ここで、ItemType は項目の種類の名前、MetaDataName はメタデータの名前です。

```xml
%(ItemType.MetaDataName)
```

**項目メタデータを確認するには**

1. コード エディターで、Message タスクを次の行に置き換えます。

    ```xml
    <Message Text="Compile.DependentUpon: %(Compile.DependentUpon)" />
    ```

2. プロジェクト ファイルを保存します。

3. **コマンド ウィンドウ**で、次の行を入力して実行します。

    ```cmd
    msbuild buildapp.csproj -t:HelloWorld
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

 項目リストに追加した項目には、既知のメタデータが割り当てられます。 たとえば、項目のファイル名を返す %(Filename) などです。 すべての既知のメタデータの一覧については、「[MSBuild 既知のアイテム メタデータ](../msbuild/msbuild-well-known-item-metadata.md)」をご覧ください。

**既知のメタデータを確認するには**

1. コード エディターで、Message タスクを次の行に置き換えます。

    ```xml
    <Message Text="Compile Filename: %(Compile.Filename)" />
    ```

2. プロジェクト ファイルを保存します。

3. **コマンド ウィンドウ**で、次の行を入力して実行します。

    ```cmd
    msbuild buildapp.csproj -t:HelloWorld
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

 既存の項目リストを新しい項目リストに変換できます。 項目リストを変換するには、次の構文を使用します。ここで、\<ItemType> は項目の種類の名前、\<MetadataName> はメタデータの名前です。

```xml
@(ItemType -> '%(MetadataName)')
```

たとえば、`@(SourceFiles -> '%(Filename).obj')` のような式を使用すると、ソース ファイルの項目リストをオブジェクト ファイルのコレクションに変換できます。 詳細については、「[MSBuild 変換](../msbuild/msbuild-transforms.md)」をご覧ください。

**メタデータを使用して項目を変換するには**

1. コード エディターで、Message タスクを次の行に置き換えます。

    ```xml
    <Message Text="Backup files: @(Compile->'%(filename).bak')" />
    ```

2. プロジェクト ファイルを保存します。

3. **コマンド ウィンドウ**で、次の行を入力して実行します。

    ```cmd
    msbuild buildapp.csproj -t:HelloWorld
    ```

4. 出力を調べます。 次の行が表示されます。

    ```
    Backup files: Form1.bak;Form1.Designer.bak;Program.bak;AssemblyInfo.bak;Resources.Designer.bak;Settings.Designer.bak
    ```

この構文で表されるメタデータではバッチ処理は行われないことに注意してください。

## <a name="whats-next"></a>次の内容

 簡単なプロジェクト ファイルを 1 ステップずつ作成する方法については、「[チュートリアル:MSBuild プロジェクト ファイルのゼロからの作成](../msbuild/walkthrough-creating-an-msbuild-project-file-from-scratch.md)」をお試しください。

## <a name="see-also"></a>関連項目

- [MSBuild の概要](../msbuild/msbuild.md)
- [MSBuild リファレンス](../msbuild/msbuild-reference.md)
