---
title: -ProjectConfig (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- /projectconfig Devenv switch
- configurations, rebuilding
- deployment projects, creating
- configurations, cleaning
- deployment projects, specifying
- deployment projects, adding
- build configurations, specifying
- Devenv, /projectconfig switch
- projectconfig Devenv switch (/projectconfig)
- projects [Visual Studio], build configuration
- projects [Visual Studio], cleaning
ms.assetid: 6b54ef59-ffed-4f62-a645-1279ede97ebf
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a33c7cbaef473e75631bb4ac6c0d217198cbf250
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72662084"
---
# <a name="projectconfig-devenvexe"></a>/ProjectConfig (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

`/project` 引数で指定されたプロジェクトをビルド、消去、リビルド、または展開する際に適用されるプロジェクトのビルド構成を指定します。

## <a name="syntax"></a>構文

```
devenv SolutionName {/build|/clean|/rebuild|/deploy} SolnConfigName [/project ProjName] [/projectconfig ProjConfigName]
```

## <a name="arguments"></a>引数
 /build は、によって指定されたプロジェクトをビルドし `/project` `ProjName` ます。

 /clean は、ビルド中に作成されたすべての中間ファイルと出力ディレクトリを消去します。

 /rebuild は、によって指定されたプロジェクトをビルドし `/project` `ProjName` ます。

 /配置は、ビルドまたはリビルド後にプロジェクトを配置することを指定します。

 `SolnConfigName` 必須。 `SolutionName` で指定されたソリューションに適用されるソリューション構成の名前。

 `SolutionName` 必須。 ソリューション ファイルの完全パスと名前。

 /project `ProjName` 省略可能。 ソリューション内のプロジェクト ファイルのパスと名前です。 `SolutionName` フォルダーからプロジェクト ファイルへの相対パス、プロジェクトの表示名、またはプロジェクト ファイルの完全なパスと名前を入力できます。

 /projectconfig `ProjConfigName` 省略可能。 指定した `/project` に適用されるプロジェクトのビルド構成の名前。

## <a name="remarks"></a>注釈

- `devenv /build`、/`clean`、`/rebuild`、または `/deploy` コマンドの一部として `/project` スイッチとともに使用する必要があります。

- 空白を含む文字列を二重引用符で囲みます。

- エラーなどのビルドの概要情報は、**[コマンド]** ウィンドウ、または `/out` スイッチで指定された任意のログ ファイルに表示できます。

## <a name="example"></a>例
 この例では、`Debug` プロジェクトのビルド構成を使用して、`MySolution` の `Debug` ソリューション構成内でプロジェクト `CSharpConsoleApp` をビルドします。

```
devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>参照
 [Devenv コマンドラインスイッチ](../../ide/reference/devenv-command-line-switches.md) [/Project (devenv.exe)](../../ide/reference/project-devenv-exe.md) [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md) [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md) [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md) [/配置 (devenv.exe)](../../ide/reference/deploy-devenv-exe.md) [/out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
