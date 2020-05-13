---
title: デバッグ構成とリリース構成を設定する |Microsoft Docs
ms.date: 10/05/2018
ms.topic: reference
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
ms.openlocfilehash: 75acf0a3a821b4d2561ea14e583e71761b8b476e
ms.sourcegitcommit: 5216c15e9f24d1d5db9ebe204ee0e7ad08705347
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68925475"
---
# <a name="set-debug-and-release-configurations-in-visual-studio"></a>Visual Studio でのデバッグおよびリリース構成の設定

Visual Studio プロジェクトでは、ご使用のプログラムに対応するリリースとデバッグ構成を個別に用意しています。 デバッグ用のデバッグバージョンと、最終リリース配布用のリリースバージョンをビルドします。

デバッグ構成では、プログラムは完全なシンボリックデバッグ情報と共にコンパイルされ、最適化は行われません。 ソース コードと生成された命令の関係は非常に複雑であり、最適化を行うとデバッグが困難になるためです。

プログラムのリリース構成にシンボリックデバッグ情報がなく、完全に最適化されています。 マネージコードとC++コードでは、使用される[コンパイラオプションに応じて](#BKMK_symbols_release)、.pdb ファイルにデバッグ情報を生成できます。 .Pdb ファイルを作成すると、後でリリースバージョンをデバッグする必要がある場合に便利です。

ビルド構成の詳細については、「[ビルド構成について](../ide/understanding-build-configurations.md)」を参照してください。

ビルド構成は、 **[ビルド]** メニュー、ツールバー、またはプロジェクトのプロパティ ページを使用して変更できます。 プロジェクト プロパティ ページは、言語固有のページです。 次の手順では、メニューとツールバーからビルド構成を変更する方法を示します。 さまざまな言語のプロジェクトでビルド構成を変更する方法の詳細については、以下の[「](#see-also)関連項目」セクションを参照してください。

## <a name="change-the-build-configuration"></a>ビルド構成の変更

ビルド構成を変更するには、次のいずれかの方法を実行します。

* **[ビルド]** メニューの **[Configuration Manager]** を選択し、 **[デバッグ]** または **[リリース]** を選択します。

または

* ツールバーの場合は、 **[ソリューション構成]** リスト ボックスから **[デバッグ]** または **[リリース]** をクリックします。

  ![ツールバーのビルド構成](../debugger/media/toolbarbuildconfiguration.png "Toolbarbuildconfiguration")

## <a name="BKMK_symbols_release"></a>ビルド (C#、 C++、Visual Basic、) のシンボル (.pdb) ファイルを生成F#します

シンボル (.pdb) ファイルと、含めるデバッグ情報を生成するように選択できます。 ほとんどの種類のプロジェクトでは、コンパイラはデバッグビルドとリリースビルドのシンボルファイルを既定で生成しますが、その他の既定の設定はプロジェクトの種類と Visual Studio のバージョンによって異なります。

> [!IMPORTANT]
> デバッガーは、実行可能ファイルがビルドされたときに作成された .pdb ファイルと正確に一致する実行可能ファイルの .pdb ファイルのみ読み込みます (つまり .pdb ファイルはオリジナルまたはオリジナルのコピーであることが必要)。 詳細については、「 [Visual Studio が、ビルドされたバイナリファイルと完全に一致する必要](https://blogs.msdn.microsoft.com/jimgries/2007/07/06/why-does-visual-studio-require-debugger-symbol-files-to-exactly-match-the-binary-files-that-they-were-built-with/)があるのはなぜですか」を参照してください。

プロジェクトの種類ごとに、これらのオプションを設定する方法が異なる場合があります。

### <a name="generate-symbol-files-for-a-c-aspnet-or-visual-basic-project"></a>、ASP.NET、またはC#Visual Basic プロジェクトのシンボルファイルを生成する

または Visual Basic でC#のデバッグ構成のプロジェクト設定の詳細については、「デバッグ構成の[プロジェクトC# ](../debugger/project-settings-for-csharp-debug-configurations.md)設定」または「 [Visual Basic デバッグ構成のプロジェクト](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)設定」を参照してください。

1. ソリューション エクスプローラーでプロジェクトを選択します。

2. **[プロパティ]** アイコンを選択します (または**Alt + enter**キーを押します)。

3. サイドペインで、 **[ビルド]** (または Visual Basic で**コンパイル**) を選択します。

4. **構成**の一覧で、 **[デバッグ]** または **[リリース]** を選択します。

5. **[詳細設定]** ボタン (または Visual Basic の **[詳細コンパイルオプション]** ボタン) を選択します。

6. **デバッグ情報**の一覧 (または Visual Basic の **[デバッグ情報の生成]** の一覧) で、 **[完全]** 、 **[Pdb のみ]** 、または **[ポータブル]** を選択します。

   ポータブル形式は、.NET Core の最新のクロスプラットフォーム形式です。 オプションの詳細については、「 [[ビルドの詳細C#設定] ダイアログボックス」 ()](../ide/reference/advanced-build-settings-dialog-box-csharp.md)を参照してください。

   ![ビルドC#の pdb を生成する](../debugger/media/dbg_project_properties_pdb_csharp.png "GeneratePDBsForCSharp")

7. プロジェクトをビルドします。

   コンパイラは、実行可能ファイルまたはメイン出力ファイルと同じフォルダーにシンボルファイルを作成します。

### <a name="generate-symbol-files-for-a-c-project"></a>プロジェクトのシンボルファイルをC++生成する

1. ソリューション エクスプローラーでプロジェクトを選択します。

2. **[プロパティ]** アイコンを選択します (または**Alt + enter**キーを押します)。

3. **構成**の一覧で、 **[デバッグ]** または **[リリース]** を選択します。

4. サイドペインで、 **[リンカー > デバッグ]** を選択し、 **[デバッグ情報の生成]** のオプションを選択します。

   のC++デバッグ構成のプロジェクト設定の詳細については、「 [ C++デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)」を参照してください。

5. **プログラムデータベースファイルを生成**するためのオプションを構成します。

   ほとんどC++のプロジェクトでは、既定値`$(OutDir)$(TargetName).pdb`はであり、出力フォルダーに .pdb ファイルが生成されます。

   ![ビルドC++の pdb を生成する](../debugger/media/dbg_project_properties_pdb_cplusplus.png "GeneratePDBsforCPlusPlus")

6. プロジェクトをビルドします。

   コンパイラは、実行可能ファイルまたはメイン出力ファイルと同じフォルダーにシンボルファイルを作成します。

## <a name="see-also"></a>関連項目

- [Visual Studio デバッガーでのシンボル (.pdb) ファイルとソースファイルの指定](../debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger.md)<br/>
- [デバッガーの設定と準備](../debugger/debugger-settings-and-preparation.md)<br/>
- [C++ デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-cpp-debug-configuration.md)<br/>
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)<br/>
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)<br/>
- [方法: 構成を作成および編集する](../ide/how-to-create-and-edit-configurations.md)
