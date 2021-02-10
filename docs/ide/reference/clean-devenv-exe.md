---
title: -Clean (devenv.exe)
description: devenv の Clean コマンド ライン スイッチを使用して、すべての中間ファイルと出力ディレクトリをクリーンアップする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- builds [Team System], cleaning files
- Clean Devenv switch
- /Clean Devenv switch
- Devenv, /Clean switch
ms.assetid: 79929dfd-22c9-4cec-a0d0-a16f15b8f7e4
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d4c3fdc30737a2266241e19ae40f840a41784cc1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99963290"
---
# <a name="clean-devenvexe"></a>/Clean (devenv.exe)

すべての中間ファイルと出力ディレクトリを消去します。

## <a name="syntax"></a>構文

```shell
devenv SolutionName /Clean [Config [/Project ProjName [/ProjectConfig ProjConfigName]] [/Out OutputFilename]]
```

## <a name="arguments"></a>引数

- *SolutionName*

  必須。 ソリューション ファイルの完全パスと名前。

- *構成*

  任意。 *SolutionName* で指定されたソリューションの中間ファイルの消去に使用される構成 (`Debug`、`Release` など)。 複数のソリューション プラットフォームが利用できる場合、プラットフォームも指定する必要があります (`Debug|Win32` など)。 この引数が指定されていないか空の文字列 (`""`) の場合、ソリューションのアクティブな構成が使用されます。

- `/Project` *ProjName*

  省略可能。 ソリューション内のプロジェクト ファイルのパスと名前です。 プロジェクトの表示名または *SolutionName* フォルダーからプロジェクト ファイルへの相対パスを入力できます。 プロジェクト ファイルの完全なパスと名前を入力することもできます。

- `/ProjectConfig` *ProjConfigName*

  省略可能。 指定した `/Project` の消去時に使用されるプロジェクトのビルド構成名 (`Debug`、`Release` など)。 複数のソリューション プラットフォームが利用できる場合、プラットフォームも指定する必要があります (`Debug|Win32` など)。 このスイッチを指定すると、*Config* 引数はオーバーライドされます。

- `/Out` *OutputFilename*

  省略可能。 ツールの出力を送信する先のファイル名。 このファイルが既に存在する場合、ファイルの末尾に出力が追加されます。

## <a name="remarks"></a>注釈

このスイッチを指定すると、IDE 内の **[ソリューションのクリーン]** メニュー コマンドと同じ処理が実行されます。

空白を含む文字列を二重引用符で囲みます。

エラーを含む消去およびビルド時の概要情報は、**[コマンド]** ウィンドウ、または [/Out](out-devenv-exe.md) スイッチで指定された任意のログ ファイルに表示できます。

`/Project` スイッチが指定されていない場合、*FileName* がプロジェクト ファイルとして指定されていても、消去アクションはソリューション内のすべてのプロジェクトに対して行われます。

## <a name="example"></a>例

最初の例では、ソリューション ファイルで指定された既定の構成を使用して、`MySolution` ソリューションを消去します。

2 つ目の例では、`MySolution` 内の `Debug` プロジェクト ビルド構成を使用して、プロジェクト `CSharpWinApp` を消去します。

```shell
devenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /Clean

devenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /Clean "Debug" /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig "Debug"
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
