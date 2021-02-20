---
title: '方法: プロジェクトを構成してターゲット プラットフォームを設定する'
description: 64 ビット プラットフォームを含むさまざまなプラットフォーム向けの、Visual Studio を使用したアプリケーションの設定について説明します。
ms.custom: SEO-VS-2020
ms.date: 08/16/2019
ms.technology: vs-ide-compile
ms.topic: how-to
helpviewer_keywords:
- project settings [Visual Studio], targeting platforms
- platforms, targeting specific CPUs
- project properties [Visual Studio], targeting platforms
- projects [Visual Studio], targeting platforms
- 64-bit [Visual Studio]
- 64-bit programming [Visual Studio]
- CPUs, targeting specific
- 64-bit applications [Visual Studio]
ms.assetid: 845302fc-273d-4f81-820a-7296ce91bd76
author: ghogen
ms.author: ghogen
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: f8a298f19f247c45740e87074804755f6ca691ec
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99969868"
---
# <a name="how-to-configure-projects-to-target-platforms"></a>方法: プロジェクトを構成してターゲット プラットフォームを設定する

Visual Studio では、64 ビット プラットフォームを含む、さまざまなプラットフォーム向けにアプリケーションを設定できます。 Visual Studio での 64 ビット プラットフォームのサポートについて詳しくは、「[64 ビット アプリケーション](/dotnet/framework/64-bit-apps)」を参照してください。

## <a name="target-platforms-with-the-configuration-manager"></a>構成マネージャーを使用して対象プラットフォームを指定する

**構成マネージャー** を使うと、プロジェクトの対象となる新しいプラットフォームをすばやく追加できます。 Visual Basic に用意されているプラットフォームのいずれかを選択すると、プロジェクトのプロパティは、選択したプラットフォーム向けにプロジェクトをビルドするように変更されます。

### <a name="to-configure-a-project-to-target-a-64-bit-platform"></a>64 ビット プラットフォームを対象とするようにプロジェクトを構成するには

1. メニュー バーで **[ビルド]**  >  **[構成マネージャー]** の順に選択します。

2. **[アクティブ ソリューション プラットフォーム]** ボックスの一覧で、ソリューションの対象となる 64 ビット プラットフォームを選び、 **[閉じる]** を選びます。

    1. 必要なプラットフォームが表示されない場合は、 **[アクティブ ソリューション プラットフォーム]** ボックスの一覧の **[新規作成]** を選びます。

         **[新しいソリューション プラットフォーム]** ダイアログ ボックスが表示されます。

    2. **[新しいプラットフォームを入力または選択してください]** ボックスの一覧で、 **[x64]** を選びます。

        > [!NOTE]
        > 構成に新しい名前を指定する場合は、 **[プロジェクト デザイナー]** で適切なプラットフォームを対象にするよう設定の変更が必要になることがあります。

    3. 現在のプラットフォーム構成から設定をコピーする場合は、構成を選んでから **[OK]** を選びます。

64 ビット プラットフォームを対象とするすべてのプロジェクトのプロパティが更新され、プロジェクトの次のビルドは 64 ビット プラットフォーム用に最適化されます。

> [!NOTE]
> **Win32** プラットフォーム名は、C++ プロジェクトに使用され、**x86** を意味します。 Visual Studio では、プロジェクトレベルのプラットフォームとソリューションレベルのプラットフォームの両方が考慮され、プロジェクト プラットフォームは言語固有のプロジェクト システムから取得されます。 C++ プロジェクトでは **Win32** と **x64** が使用されますが、ソリューション プラットフォームでは **x86** と **x64** が使用されます。 ソリューション構成として **x86** を選択すると、Visual Studio によって C++ プロジェクトに **Win32** プラットフォームが選択されます。 プロジェクトレベルのプラットフォームとソリューションレベルのプラットフォームの両方の設定を表示するには、 **[構成マネージャー]** を開き、2 つのプラットフォームの設定を確認します。 ソリューションレベルのプラットフォームは **[アクティブ ソリューション プラットフォーム]** ドロップダウンに表示され、テーブルには各プロジェクトのプロジェクトレベルのプラットフォームが表示されます。
> ![ソリューション プラットフォームとプロジェクト プラットフォームを示すスクリーンショット](media/project-platform-win32.png)

## <a name="target-platforms-in-the-project-designer"></a>プロジェクト デザイナーで対象プラットフォームを指定する

**プロジェクト デザイナー** にも、さまざまなプラットフォームをプロジェクトの対象にする方法が用意されています。 **[新しいソリューション プラットフォーム]** ダイアログ ボックスの一覧にあるプラットフォームのいずれかを選んでも、ソリューションで機能しない場合は、カスタム構成名を作成し、**プロジェクト デザイナー** で設定を変更して、適切なプラットフォームを対象にすることができます。

このタスクの実行方法は、使用するプログラミング言語によって異なります。 詳細については、次のリンクを参照してください。

- [!INCLUDE[vbprvb](../code-quality/includes/vbprvb_md.md)] プロジェクトについては、「[/platform (Visual Basic)](/dotnet/visual-basic/reference/command-line-compiler/platform)」をご覧ください。

- [!INCLUDE[csprcs](../data-tools/includes/csprcs_md.md)] プロジェクトについては、「[[ビルド] ページ (プロジェクト デザイナー) (C#)](../ide/reference/build-page-project-designer-csharp.md)」を参照してください。

- [!INCLUDE[vcprvc](../code-quality/includes/vcprvc_md.md)] プロジェクトについては、「[/clr (Common Language Runtime compilation)](/cpp/build/reference/clr-common-language-runtime-compilation)」(/clr (共通言語ランタイムのコンパイル)) を参照してください。

## <a name="manually-editing-the-project-file"></a>プロジェクト ファイルを手動で編集する

カスタムの構成によっては、プロジェクト ファイルを手動で編集しなければならないことがあります。 たとえば、次の例のように、2 つの異なるプラットフォームで異なっている参照など、IDE で指定できない条件があるときです。

### <a name="example-referencing-x86-and-x64-assemblies-and-dlls"></a>例:x86 アセンブリ、x64 アセンブリ、DLL を参照する

x86 バージョンと x64 バージョンの両方を持つ .NET アセンブリまたは DLL がある場合があります。 これらの参照を使用するようにプロジェクトを設定するには、まず参照を追加し、次にプロジェクト ファイルを開いて編集し、構成とターゲット プラットフォームの両方を参照する条件を含む `ItemGroup` を追加します。  たとえば、参照しているバイナリが ClassLibrary1 のとき、デバッグ構成とリリース構成に異なるパスがあり、さらに x86 バージョンと x64 バージョンがあります。  その場合、次のように、設定の全組み合わせで 4 つの `ItemGroup` 要素を使用します。

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <OutputType>Exe</OutputType>
    <TargetFramework>netcoreapp2.0</TargetFramework>
    <Platforms>AnyCPU;x64;x86</Platforms>
  </PropertyGroup>

  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x64'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x64\Debug\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>

  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|x64'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x64\Release\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>

  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x86\Debug\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>
  
  <ItemGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|x86'">
    <Reference Include="ClassLibrary1">
      <HintPath>..\..\ClassLibrary1\ClassLibrary1\bin\x86\Release\netstandard2.0\ClassLibrary1.dll</HintPath>
    </Reference>
  </ItemGroup>
</Project>
```

::: moniker range="vs-2017"
> [!NOTE]
> Visual Studio 2017 では、プロジェクト ファイルを編集するには先にプロジェクトをアンロードする必要があります。 プロジェクトをアンロードするには、プロジェクト ノードを右クリックし、 **[プロジェクトのアンロード]** を選択します。 編集が完了したら、変更内容を保存し、プロジェクト ノードを右クリックして **[プロジェクトの再読み込み]** を選択してプロジェクトを再度読み込みます。
::: moniker-end

プロジェクト ファイルの詳細は、「[MSBuild プロジェクト ファイル スキーマ リファレンス](../msbuild/msbuild-project-file-schema-reference.md)」を参照してください。

## <a name="see-also"></a>関連項目

- [ビルド プラットフォームについて](../ide/understanding-build-platforms.md)
- [/platform (C# コンパイラ オプション)](/dotnet/csharp/language-reference/compiler-options/platform-compiler-option)
- [64 ビット アプリケーション](/dotnet/framework/64-bit-apps)
- [Visual Studio IDE の 64 ビット サポート](../ide/visual-studio-ide-64-bit-support.md)
- [プロジェクト ファイルについて](/aspnet/web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file)
