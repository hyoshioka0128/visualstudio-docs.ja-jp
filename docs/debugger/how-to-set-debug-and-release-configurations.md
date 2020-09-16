---
title: デバッグおよびリリース構成を設定する | Microsoft Docs
ms.date: 10/05/2018
ms.topic: how-to
f1_keywords:
- vs.debug.builds
dev_langs:
- CSharp
- VB
- FSharp
- C++
- JScript
helpviewer_keywords:
- configurations, release
- build configurations, release
- projects [Visual Studio], release configurations
- debugging [Visual Studio], release configurations
- release builds, changing settings
- debug builds
- debug builds, switching to release build
- debug builds, changing configuration settings
- debugging [Visual Studio], debug configurations
- projects [Visual Studio], debug configurations
- build configurations, debug
- debug configurations
- release builds, switching to debug build
- Visual Basic projects, debug and release builds
ms.assetid: 57b6bbb7-f2af-48f7-8773-127d75034ed2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e85f7c67f8dc25bb69f7de07a19286b5c63e938a
ms.sourcegitcommit: ed4372bb6f4ae64f1fd712b2b253bf91d9ff96bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89599895"
---
# <a name="set-debug-and-release-configurations-in-visual-studio"></a>Visual Studio でのデバッグおよびリリース構成の設定

Visual Studio プロジェクトでは、ご使用のプログラムに対応するリリースとデバッグ構成を個別に用意しています。 デバッグ バージョンはデバッグ用に、リリース バージョンは最終リリース配布用にビルドします。

デバッグ構成では、プログラムのコンパイルにシンボリック デバッグ情報が完全に含まれ、最適化は行われません。 ソース コードと生成された命令の関係は非常に複雑であり、最適化を行うとデバッグが困難になるためです。

プログラムのリリース構成は、シンボリック デバッグ情報を含まず、完全に最適化されます。 マネージド コードと C++ コードの場合、使用している[コンパイラ オプションによっては](#BKMK_symbols_release)、デバッグ情報が .pdb ファイル内に生成される場合があります。 .pdb ファイルを作成すると、後でリリース バージョンをデバッグする際に役立つことがあります。

ビルド構成の詳細については、「[ビルド構成について](../ide/understanding-build-configurations.md)」を参照してください。

ビルド構成は、 **[ビルド]** メニュー、ツールバー、またはプロジェクトのプロパティ ページを使用して変更できます。 プロジェクト プロパティ ページは、言語固有のページです。 次の手順では、メニューとツールバーからビルド構成を変更する方法を示します。 各種言語のプロジェクトでビルド構成を変更する方法の詳細については、以下の「[関連項目](#see-also)」を参照してください。

## <a name="change-the-build-configuration"></a>ビルド構成を変更する

ビルド構成を変更するには、次のどちらかを行います。

* **[ビルド]** メニューからの場合は、 **[構成マネージャー]** を選択し、 **[デバッグ]** または **[リリース]** を選択します。

or

* ツールバーの場合は、 **[ソリューション構成]** リスト ボックスから **[デバッグ]** または **[リリース]** をクリックします。

  ![ツール バー ビルド構成](../debugger/media/toolbarbuildconfiguration.png "ToolbarBuildConfiguration")

## <a name="generate-symbol-pdb-files-for-a-build-c-c-visual-basic-f"></a><a name="BKMK_symbols_release"></a>ビルド (C#、C++、Visual Basic、F#) のシンボル (.pdb) ファイルを生成する

シンボル (.pdb) ファイルと、それに含めるデバッグ情報を生成するように選択できます。 ほとんどのプロジェクト タイプでは、コンパイラはデバッグ ビルドとリリース ビルドのシンボル ファイルを既定で生成しますが、その他の既定の設定はプロジェクト タイプと Visual Studio のバージョンによって異なります。

> [!IMPORTANT]
> デバッガーは、実行可能ファイルがビルドされたときに作成された .pdb ファイルと正確に一致する実行可能ファイルの .pdb ファイルのみ読み込みます (つまり .pdb ファイルはオリジナルまたはオリジナルのコピーであることが必要)。 詳細については、「[Why does Visual Studio require debugger symbol files to exactly match the binary files that they were built with?](/archive/blogs/jimgries/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with)」 (ビルドに使用したバイナリ ファイルと完全に一致させるために、Visual Studio でデバッガー シンボル ファイルが必要な理由) を参照してください。

プロジェクト タイプごとに、これらのオプションを設定する方法が異なる場合があります。

### <a name="generate-symbol-files-for-a-c-aspnet-or-visual-basic-project"></a>C#、ASP.NET、または Visual Basic プロジェクトのシンボル ファイルを生成する

C# または Visual Basic のデバッグ構成の、プロジェクト設定の詳細については、「[C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)」または「[Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)」を参照してください。

1. ソリューション エクスプローラーでプロジェクトを選択します。

2. **[プロパティ]** アイコンを選択します (または **Alt + Enter** キーを押します)。

3. サイド ペインで、 **[ビルド]** (または Visual Basic の **[コンパイル]** ) を選択します。

4. **[構成]** ボックスの一覧の **[デバッグ]** または **[リリース]** をクリックします。

5. **[詳細]** ボタン (または Visual Basic の **[詳細コンパイル オプション]** ) を選択します。

6. **[デバッグ情報]** ボックスの一覧 (または Visual Basic の **[デバッグ情報の生成]** ボックスの一覧) で、 **[完全]** 、 **[pdb のみ]** 、または **[移植可能]** を選択します。

   .NET Core の最新のクロスプラットフォーム形式が移植可能です。 詳細については、「[[ビルドの詳細設定] ダイアログ ボックス (C#)](../ide/reference/advanced-build-settings-dialog-box-csharp.md)」を参照してください。

   ![C# でビルドの PDB を生成する](../debugger/media/dbg_project_properties_pdb_csharp.png "GeneratePDBsForCSharp")

7. プロジェクトをビルドします。

   コンパイラは、実行可能ファイルまたはメイン出力ファイルと同じフォルダーにシンボル ファイルを作成します。

### <a name="generate-symbol-files-for-a-c-project"></a>C++ プロジェクトのシンボル ファイルを生成する

1. ソリューション エクスプローラーでプロジェクトを選択します。

2. **[プロパティ]** アイコンを選択します (または **Alt + Enter** キーを押します)。

3. **[構成]** ボックスの一覧の **[デバッグ]** または **[リリース]** をクリックします。

4. サイド ペインで、 **[リンカー] > [デバッグ]** を選択し、 **[デバッグ情報の生成]** のオプションを選択します。

   C++ のデバッグ構成の、プロジェクト設定の詳細については、「[C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)」を参照してください。

5. **プログラム データベース ファイルを生成する**ためのオプションを構成します。

   ほとんどの C++ プロジェクトでは、既定値は `$(OutDir)$(TargetName).pdb` です。これにより、出力フォルダーに .pdb ファイルが生成されます。

   ![C++ でビルドの PDB を生成する](../debugger/media/dbg_project_properties_pdb_cplusplus.png "GeneratePDBsforCPlusPlus")

6. プロジェクトをビルドします。

   コンパイラは、実行可能ファイルまたはメイン出力ファイルと同じフォルダーにシンボル ファイルを作成します。

## <a name="see-also"></a><a name="see-also"></a>関連項目

- [Visual Studio デバッガーでシンボル (.pdb) ファイルとソース ファイルを指定する](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)<br/>
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)<br/>
- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)<br/>
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)<br/>
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)<br/>
- [方法: 構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)