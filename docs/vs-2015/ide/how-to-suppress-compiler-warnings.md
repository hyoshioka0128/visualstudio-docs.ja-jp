---
title: '方法: コンパイラの警告を非表示にする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
ms.assetid: 31827b17-f933-413d-b28a-b19f903b64ca
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: aeb404c479edec5dec89f28e80584d435f5c370a
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670640"
---
# <a name="how-to-suppress-compiler-warnings"></a>方法: コンパイラ警告を非表示にする

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

必要のないコンパイラの警告の種類を指定することで、ビルド ログを見やすくすることができます。 たとえば、この方法を使って、ビルド ログの詳細さを標準、詳細、または診断に設定したときに自動的に生成される情報の全部ではなく一部だけを確認できます。 詳細さについて詳しくは「[方法: ビルド ログ ファイルを表示、保存、および構成する](../ide/how-to-view-save-and-configure-build-log-files.md)」をご覧ください。

### <a name="to-suppress-specific-warnings-for-visual-c-or-f"></a>Visual C#または F \# の特定の警告を非表示にするには

1. **ソリューション エクスプローラー**で、警告を抑制するプロジェクトを選びます。

2. メニュー バーの **[表示]** 、 **[プロパティ ページ]** の順にクリックします。

3. **[ビルド]** ページを選びます。

4. **[警告の表示なし]** ボックスで表示しない警告のエラー コードをセミコロンで区切って指定した後、ソリューションをリビルドします。

### <a name="to-suppress-specific-warnings-for-visual-c"></a>Visual C++ の特定の警告を抑制するには

1. **ソリューション エクスプローラー**で、警告を抑制するプロジェクトまたはソース ファイルを選びます。

2. メニュー バーの **[表示]** 、 **[プロパティ ページ]** の順にクリックします。

3. **[構成プロパティ]** カテゴリを選び、 **[C/C++]** カテゴリを選んだ後、 **[詳細設定]** ページを選びます。

4. 次のいずれかの操作を実行します。

    - **[指定の警告を無効にする]** ボックスで表示しない警告のエラー コードをセミコロンで区切って指定します。

    - **[指定の警告を無効にする]** ボックスで、 **[編集]** を選んで他のオプションを表示します。

5. **[OK]** ボタンを選び、ソリューションをリビルドします。

## <a name="suppressing-warnings-for-visual-basic"></a>Visual Basic の警告の抑制

プロジェクトの .vbproj ファイルを編集することで、Visual Basic コンパイラの特定の警告を非表示にできます。 また、[プロジェクト デザイナーの [コンパイル] ページ](../ide/reference/compile-page-project-designer-visual-basic.md)を使って、カテゴリ単位で警告を抑制することもできます。 詳しくは、「[Visual Basic での警告の構成](../ide/configuring-warnings-in-visual-basic.md)」をご覧ください。

#### <a name="to-suppress-specific-warnings-for-visual-basic"></a>Visual Basic の特定の警告を抑制するには

1. **ソリューション エクスプローラー**で、警告を抑制するプロジェクトを選びます。

2. メニュー バーから、 **[プロジェクト]** 、 **[プロジェクトのアンロード]** の順に選びます。

3. **ソリューション エクスプローラー**で、プロジェクトのショートカット メニューを開き、 **[<** _プロジェクト名_ **>.vbproj の編集]** を選びます。

    コード エディターでプロジェクト ファイルが開かれます。

4. ビルドしているビルド構成で `<NoWarn></NoWarn>` 要素を探します。

    次の例では、x86 プラットフォームでのデバッグ ビルド構成の `<NoWarn></NoWarn>` 要素を太字で示してあります。

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
       <NoWarn></NoWarn>
       <WarningLevel>1</WarningLevel>
     </PropertyGroup>
   ```

5. `<NoWarn>` 要素の値として、1 つ以上の警告番号を追加します。 複数の警告番号を指定する場合は、次の例のようにコンマで区切ります。

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

6. 変更を .vbproj ファイルに保存します。

7. メニュー バーから、 **[プロジェクト]** 、 **[プロジェクトの再読み込み]** の順に選びます。

8. メニュー バーから、 **[ビルド]** 、 **[ソリューションのリビルド]** の順に選びます。

    指定した警告が、 **[出力]** ウィンドウに表示されなくなります。

   詳しくは、「[/nowarn](https://msdn.microsoft.com/library/7ebf2106-0652-4fdc-bf60-70fc86465d83)」をご覧ください。

## <a name="see-also"></a>参照

- [チュートリアル: アプリケーションをビルドする](../ide/walkthrough-building-an-application.md)
- [方法: ビルド ログ ファイルを表示、保存、および構成する](../ide/how-to-view-save-and-configure-build-log-files.md)
- [コードのコンパイルとビルド](../ide/compiling-and-building-in-visual-studio.md)
