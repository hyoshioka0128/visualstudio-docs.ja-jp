---
title: -Project (devenv.exe)
description: devenv の Project コマンド ライン スイッチを使用して、プロジェクトをビルド、クリーンアップ、リビルド、または配置するために、指定したソリューション構成内の 1 つのプロジェクトを識別する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- /Project Devenv switch
- projects [Visual Studio], rebuilding
- projects [Visual Studio], building
- deployment projects, specifying
- Project Devenv switch (/Project)
- Devenv, /Project switch
- projects [Visual Studio], cleaning
ms.assetid: 8b07859c-3439-436d-9b9a-a8ee744eee30
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 90c1cdf37ddda7209b4f951e42ad07720e5cc40b
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96040110"
---
# <a name="project-devenvexe"></a>/Project (devenv.exe)

指定したソリューション構成内の単一のプロジェクトを、ビルド、クリーン、リビルド、または配置対象として指定します。

## <a name="syntax"></a>構文

```shell
devenv SolutionName {/Build|/Clean|/Deploy|/Rebuild} [SolnConfigName [/Project ProjName [/ProjectConfig ProjConfigName]] [/Out OutputFilename]]
```

## <a name="arguments"></a>引数

- *SolutionName*

  必須。 ソリューション ファイルの完全パスと名前。

- {`/Build`|`/Clean`|`/Deploy`|`/Rebuild`}

  必須。 プロジェクトの[ビルド](build-devenv-exe.md)、[消去](clean-devenv-exe.md)、[配置](deploy-devenv-exe.md)、または[リビルド](rebuild-devenv-exe.md)を行います。

- *SolnConfigName*

  省略可能。 *SolutionName* で指定されたソリューションに適用されるソリューション構成の名前 (`Debug`、`Release` など)。 複数のソリューション プラットフォームが利用できる場合、プラットフォームも指定する必要があります (`Debug|Win32` など)。 この引数が指定されていないか空の文字列 (`""`) の場合、ソリューションのアクティブな構成が使用されます。

- `/Project` *ProjName*

  省略可能。 ソリューション内のプロジェクト ファイルのパスと名前です。 プロジェクトの表示名または *SolutionName* フォルダーからプロジェクト ファイルへの相対パスを入力できます。 プロジェクト ファイルの完全なパスと名前を入力することもできます。

- `/ProjectConfig` *ProjConfigName*

  省略可能。 指定した `/Project` に適用されるプロジェクトのビルド構成名 (`Debug`、`Release` など)。 複数のソリューション プラットフォームが利用できる場合、プラットフォームも指定する必要があります (`Debug|Win32` など)。

- `/Out` *OutputFilename*

  省略可能。 ツールの出力を送信する先のファイル名。 このファイルが既に存在する場合、ファイルの末尾に出力が追加されます。

## <a name="remarks"></a>注釈

- `devenv` `/Build`、`/Clean`、`/Rebuild`、または `/Deploy` コマンドの一部として使用する必要があります。

- 空白を含む文字列を二重引用符で囲みます。

- エラーなどのビルドの概要情報は、 **[コマンド]** ウィンドウ、または `/Out` スイッチで指定された任意のログ ファイルに表示できます。

## <a name="example"></a>例

この例では、`MySolution` 内の `Debug` プロジェクト ビルド構成を使用して、プロジェクト `CSharpWinApp` をビルドします。

```shell
devenv "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
- [/ProjectConfig (devenv.exe)](../../ide/reference/projectconfig-devenv-exe.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Deploy (devenv.exe)](../../ide/reference/deploy-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
