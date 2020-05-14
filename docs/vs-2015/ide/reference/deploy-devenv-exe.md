---
title: -Deploy (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /deploy switch
- deploy Devenv switch
- deploying applications [Visual Studio], after build
- /deploy Devenv switch
ms.assetid: e47c8723-df08-4645-aa2d-0c956e7ccca2
caps.latest.revision: 16
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 620be9ea458d55a8c9610079b357cc9466a03f56
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660781"
---
# <a name="deploy-devenvexe"></a>/Deploy (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ビルドまたはリビルド後にソリューションを配置します。 マネージド コード プロジェクトにのみ適用されます。

## <a name="syntax"></a>構文

```
devenv SolutionName /deploy SolnConfigName [/project ProjName] [/projectconfig ProjConfigName] [/out LogFileName]
```

## <a name="arguments"></a>引数
 `SolnConfigName` 必須。 `SolutionName` で指定されたソリューションのビルドに使用されるソリューション構成の名前。

 `SolutionName` 必須。 ソリューション ファイルの完全パスと名前。

 /project `ProjName` 省略可能。 ソリューション内のプロジェクト ファイルのパスと名前です。 `SolutionName` フォルダーからプロジェクト ファイルへの相対パス、プロジェクトの表示名、またはプロジェクト ファイルの完全なパスと名前を入力できます。

 /projectconfig `ProjConfigName` 省略可能。 指定した `/project` のビルド時に使用されるプロジェクトのビルド構成の名前。

## <a name="remarks"></a>解説
 指定するプロジェクトは、配置プロジェクトである必要があります。 指定したプロジェクトが配置プロジェクトでない場合に、ビルド済みのプロジェクトを渡して配置しようとすると、エラーが発生して配置は失敗します。

 空白を含む文字列を二重引用符で囲みます。

 エラーなどのビルドの概要情報は、 **[コマンド]** ウィンドウ、または `/out` スイッチで指定された任意のログ ファイルに表示できます。

## <a name="example"></a>例
 この例では、`Release` プロジェクトのビルド構成を使用して、`MySolution` の `Release` ソリューション構成内でプロジェクト `CSharpConsoleApp` を配置します。

```
devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /deploy Release /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Release
```

## <a name="see-also"></a>関連項目
 [Devenv コマンドラインスイッチ](../../ide/reference/devenv-command-line-switches.md) [/Project (devenv.exe)](../../ide/reference/project-devenv-exe.md) [/Build (devenv.exe](../../ide/reference/build-devenv-exe.md) ) [/Clean (devenv.exe)](../../ide/reference/clean-devenv-exe.md) [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md) [/out (devenv.exe](../../ide/reference/out-devenv-exe.md) ) を実行します。
