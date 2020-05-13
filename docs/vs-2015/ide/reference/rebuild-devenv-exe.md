---
title: -Rebuild (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /rebuild switch
- rebuild Devenv switch (/rebuild)
- projects [Visual Studio], rebuilding
- /rebuild Devenv switch
- applications [Visual Studio], rebuilding
ms.assetid: c5a8a4bf-0e2b-46eb-a44a-8aeb29b92c32
caps.latest.revision: 15
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 008169829a6cf76e959d00f010959239a5f390b5
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665648"
---
# <a name="rebuild-devenvexe"></a>/Rebuild (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定したソリューション構成を消去してからビルドします。

## <a name="syntax"></a>構文

```
devenv SolutionName /rebuild SolnConfigName [/project ProjName] [/projectconfig ProjConfigName]
```

## <a name="arguments"></a>引数
 `SolnConfigName` 必須。 `SolutionName` で指定されたソリューションのリビルドに使用されるソリューション構成の名前。

 `SolutionName` 必須。 ソリューション ファイルの完全パスと名前。

 /project `ProjName` 省略可能。 ソリューション内のプロジェクト ファイルのパスと名前です。 `SolutionName` フォルダーからプロジェクト ファイルへの相対パス、プロジェクトの表示名、またはプロジェクト ファイルの完全なパスと名前を入力できます。

 /projectconfig `ProjConfigName` 省略可能。 指定した `/project` のリビルド時に使用されるプロジェクトのビルド構成の名前。

## <a name="remarks"></a>解説

- このスイッチは、統合開発環境 (IDE) 内の **[ソリューションのリビルド]** メニュー コマンドと同じ機能を実行します。

- 空白を含む文字列を二重引用符で囲みます。

- エラーを含むクリーンとビルドの概要情報は、 **[コマンド]** ウィンドウ、または `/out` スイッチで指定された任意のログ ファイルに表示できます。

## <a name="example"></a>例
 この例では、`Debug` プロジェクトのビルド構成を使用して、`MySolution` の `Debug` ソリューション構成内でプロジェクト `CSharpWinApp` を消去してリビルドします。

```
devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /rebuild Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>関連項目
 [Devenv コマンドラインスイッチ](../../ide/reference/devenv-command-line-switches.md)の[/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md) [/Clean (devenv.exe](../../ide/reference/clean-devenv-exe.md) ) [/out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
