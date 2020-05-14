---
title: プロジェクトと NuGet パッケージのコンパイラの警告を非表示にする
ms.date: 01/24/2018
ms.technology: vs-ide-compile
ms.topic: conceptual
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: b604f6a1392353d304897a233b74c0d81fc258df
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "76114512"
---
# <a name="how-to-suppress-compiler-warnings"></a>方法: コンパイラの警告を非表示にする

1 つまたは複数の種類のコンパイラの警告を除外して、ビルド ログをまとめることができます。 たとえば、ビルド ログの詳細さを**標準**、**詳細**、または**診断**に設定したときに生成される出力の一部だけを確認できます。 詳細さについて詳しくは「[方法: ビルド ログ ファイルを表示、保存、および構成する](../ide/how-to-view-save-and-configure-build-log-files.md)」をご覧ください。

## <a name="suppress-specific-warnings-for-visual-c-or-f"></a>Visual C# または F\# の特定の警告を非表示にする

C# または F# プロジェクトの特定の警告を非表示にするには、 **[ビルド]** プロパティ ページを使用します。

1. **ソリューション エクスプローラー**で、警告を抑制するプロジェクトを選びます。

1. メニュー バーで **[表示]**  >  **[プロパティ ページ]** の順に選びます。

1. **[ビルド]** ページを選びます。

1. **[警告の表示なし]** ボックスで表示しない警告のエラー コードをセミコロンで区切って指定します。

1. ソリューションをリビルドします。

## <a name="suppress-specific-warnings-for-c"></a>C++ の特定の警告を非表示にする

C++ プロジェクトの特定の警告を非表示にするには、 **[構成プロパティ]** プロパティ ページを使用します。

1. **ソリューション エクスプローラー**で、警告を抑制するプロジェクトまたはソース ファイルを選びます。

1. メニュー バーで **[表示]**  >  **[プロパティ ページ]** の順に選びます。

1. **[構成プロパティ]** カテゴリを選び、 **[C/C++]** カテゴリを選んだ後、 **[詳細設定]** ページを選びます。

1. 次のいずれかの操作を実行します。

    - **[指定の警告を無効にする]** ボックスで表示しない警告のエラー コードをセミコロンで区切って指定します。

    - **[指定の警告を無効にする]** ボックスで、 **[編集]** を選んで他のオプションを表示します。

1. **[OK]** ボタンを選び、ソリューションをリビルドします。

## <a name="suppress-warnings-for-visual-basic"></a>Visual Basic の警告を非表示にする

プロジェクトの *.vbproj* ファイルを編集することで、Visual Basic の特定のコンパイラの警告を非表示にできます。 *カテゴリ*で警告を非表示にするには、[コンパイル プロパティ ページ](../ide/reference/compile-page-project-designer-visual-basic.md)を使用できます。 詳細については、「[Visual Basic での警告の構成](../ide/configuring-warnings-in-visual-basic.md)」を参照してください。

### <a name="to-suppress-specific-warnings-for-visual-basic"></a>Visual Basic の特定の警告を抑制するには

この例は、 *.vbproj* ファイルを編集して特定のコンパイラの警告を非表示にする方法を示しています。

1. **ソリューション エクスプローラー**で、警告を抑制するプロジェクトを選びます。

1. メニュー バーから、 **[プロジェクト]**  >  **[プロジェクトのアンロード]** の順に選びます。

1. **ソリューション エクスプローラー**で、プロジェクトの右クリックまたはショートカット メニューを開き、 **[\<プロジェクト名>.vbproj の編集]** を選びます。

    コード エディターに XML プロジェクト ファイルが開きます。

1. ビルドに使用するビルド構成の `<NoWarn>` 要素を見つけ、`<NoWarn>` 要素の値として 1 つまたは複数の警告番号を追加します。 複数の警告番号を指定する場合は、コンマで区切ります。

     次の例では、2 つのコンパイラの警告が非表示にされた、x86 プラットフォームでの`<NoWarn>`デバッグ*ビルド構成の* 要素を太字で示してあります。

    ```xml
    <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|x86' ">
        <PlatformTarget>x86</PlatformTarget>
        <DebugSymbols>true</DebugSymbols>
        <DebugType>full</DebugType>
        <Optimize>false</Optimize>
        <OutputPath>bin\Debug\</OutputPath>
        <DefineDebug>true</DefineDebug>
        <DefineTrace>true</DefineTrace>
        <ErrorReport>prompt</ErrorReport>
        <NoWarn>40059,42024</NoWarn>
        <WarningLevel>1</WarningLevel>
      </PropertyGroup>
    ```

   > [!NOTE]
   > 既定では、.NET Core プロジェクトにはビルド構成プロパティ グループは含まれません。 .NET Core プロジェクトで警告を非表示にするには、手動でビルド構成セクションをファイルに追加します。 次に例を示します。
   >
   > ```xml
   > <Project Sdk="Microsoft.NET.Sdk">
   >   <PropertyGroup>
   >     <OutputType>Exe</OutputType>
   >     <TargetFramework>netcoreapp2.0</TargetFramework>
   >     <RootNamespace>VBDotNetCore_1</RootNamespace>
   >   </PropertyGroup>
   >   <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
   >     <NoWarn>42016,41999,42017</NoWarn>
   >   </PropertyGroup>
   > </Project>
   > ```

1. 変更を *.vbproj* ファイルに保存します。

1. メニュー バーから、 **[プロジェクト]**  >  **[プロジェクトの再読み込み]** の順に選びます。

1. メニュー バーから、 **[ビルド]**  >  **[ソリューションのリビルド]** の順に選びます。

    指定した警告が、 **[出力]** ウィンドウに表示されなくなります。

詳細については、Visual Basic のコマンド ライン コンパイラの [/nowarn コンパイラ オプション](/dotnet/visual-basic/reference/command-line-compiler/nowarn)を参照してください。

## <a name="suppress-warnings-for-nuget-packages"></a>NuGet パッケージの警告を非表示にする

場合によっては、プロジェクト全体ではなく、1 つの NuGet パッケージに対して NuGet コンパイラの警告を非表示にしたい場合があります。 警告は役に立つため、プロジェクト レベルで非表示にしたくない場合があります。 たとえば、NuGet 警告のうちの 1 つは、パッケージがプロジェクトと完全に互換性がない可能性を示します。 これをプロジェクト レベルで非表示にし、後で追加の NuGet パッケージを追加すると、互換性に関する警告が生成されたかどうかがわからなくなります。

### <a name="to-suppress-a-specific-warning-for-a-single-nuget-package"></a>1 つの NuGet パッケージに対して特定の警告を非表示にするには

1. **ソリューション エクスプローラー**で、コンパイラの警告を非表示にする NuGet パッケージを選択します。

   ![ソリューション エクスプローラーの NuGet パッケージ](media/nuget-package-with-warning.png)

1. 右クリックまたはコンテキスト メニューから、 **[プロパティ]** を選択します。

1. パッケージのプロパティの **[NoWarn]** ボックスで、このパッケージに対して非表示にする警告番号を入力します。 複数の警告を非表示にする場合は、コンマを使用して警告番号を区切ります。

   ![NuGet パッケージのプロパティ](media/nuget-properties-nowarn.png)

   **ソリューション エクスプローラー**と**エラー一覧**から警告が消えます。

## <a name="see-also"></a>参照

- [チュートリアル: アプリケーションをビルドする](../ide/walkthrough-building-an-application.md)
- [方法: ビルド ログ ファイルを表示、保存、および構成する](../ide/how-to-view-save-and-configure-build-log-files.md)
- [コンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
