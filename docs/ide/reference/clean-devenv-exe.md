---
title: -Clean (devenv.exe)
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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: ac184f25d79a47814fee52b99bce1cddce247fc5
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75570467"
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

  任意。 `Debug`SolutionName`Release` で指定されたソリューションの中間ファイルの消去に使用される構成 ( *、* など)。 複数のソリューション プラットフォームが利用できる場合、プラットフォームも指定する必要があります (`Debug|Win32` など)。 この引数が指定されていないか空の文字列 (`""`) の場合、ソリューションのアクティブな構成が使用されます。

- `/Project` *ProjName*

  任意。 ソリューション内のプロジェクト ファイルのパスと名前です。 プロジェクトの表示名または *SolutionName* フォルダーからプロジェクト ファイルへの相対パスを入力できます。 プロジェクト ファイルの完全なパスと名前を入力することもできます。

- `/ProjectConfig` *ProjConfigName*

  任意。 指定した `Debug` の消去時に使用されるプロジェクトのビルド構成名 (`Release`、`/Project` など)。 複数のソリューション プラットフォームが利用できる場合、プラットフォームも指定する必要があります (`Debug|Win32` など)。 このスイッチを指定すると、*Config* 引数はオーバーライドされます。

- `/Out` *OutputFilename*

  任意。 ツールの出力を送信する先のファイル名。 このファイルが既に存在する場合、ファイルの末尾に出力が追加されます。

## <a name="remarks"></a>解説

このスイッチを指定すると、IDE 内の **[ソリューションのクリーン]** メニュー コマンドと同じ処理が実行されます。

空白を含む文字列を二重引用符で囲みます。

エラーを含む消去およびビルド時の概要情報は、 **[コマンド]** ウィンドウ、または [/Out](out-devenv-exe.md) スイッチで指定された任意のログ ファイルに表示できます。

`/Project` スイッチが指定されていない場合、*FileName* がプロジェクト ファイルとして指定されていても、消去アクションはソリューション内のすべてのプロジェクトに対して行われます。

## <a name="example"></a>例

最初の例では、ソリューション ファイルで指定された既定の構成を使用して、`MySolution` ソリューションを消去します。

2 つ目の例では、`CSharpWinApp` 内の `Debug` プロジェクト ビルド構成を使用して、プロジェクト `MySolution` を消去します。

```shell
devenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /Clean

devenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /Clean "Debug" /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig "Debug"
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
