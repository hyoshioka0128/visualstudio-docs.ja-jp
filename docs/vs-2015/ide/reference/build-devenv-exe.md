---
title: -Build (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- builds [Team System], command-line
- /build Devenv switch
- Devenv, /build switch
- build Devenv switch
ms.assetid: ced21627-7653-455b-8821-3e31c6a448cf
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 419716d750771908a43318d051cb0b4681d35149
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660980"
---
# <a name="build-devenvexe"></a>/Build (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定したソリューションの構成ファイルを使用してソリューションをビルドします。

## <a name="syntax"></a>構文

```
Devenv SolutionName /build SolnConfigName [/project ProjName [/projectconfig ProjConfigName]]
```

## <a name="arguments"></a>引数
 `SolutionName` 必須。 ソリューション ファイルの完全パスと名前。

 `SolnConfigName` 必須。 `SolutionName` で指定されたソリューションのビルドに使用されるソリューション構成の名前。

 /project `ProjName` 省略可能。 ソリューション内のプロジェクト ファイルのパスと名前です。 `SolutionName` フォルダーからプロジェクト ファイルへの相対パス、プロジェクトの表示名、またはプロジェクト ファイルの完全なパスと名前を入力できます。

 /projectconfig `ProjConfigName` 省略可能。 指定した `/project` のビルド時に使用されるプロジェクトのビルド構成の名前。

## <a name="remarks"></a>解説
 このスイッチは、統合開発環境 (IDE) 内の **[ソリューションのビルド]** メニュー コマンドと同じ機能を実行します。

 空白を含む文字列を二重引用符で囲みます。

 エラーなどのビルドの概要情報は、 **[コマンド]** ウィンドウ、または `/out` スイッチで指定された任意のログ ファイルに表示できます。

 このコマンドは、最後のビルド以降に変更されたプロジェクトのみをビルドします。 ソリューション内のすべてのプロジェクトをビルドするには、[/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md) を使用します。

## <a name="example"></a>例
 この例では、`Debug` プロジェクトのビルド構成を使用して、`MySolution` の `Debug` ソリューション構成内でプロジェクト `CSharpConsoleApp` をビルドします。

```
devenv "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /build Debug /project "CSharpWinApp\CSharpWinApp.csproj" /projectconfig Debug
```

## <a name="see-also"></a>関連項目
 [Visual Studio でのプロジェクトとソリューションのビルドとクリーンアップ](../../ide/building-and-cleaning-projects-and-solutions-in-visual-studio.md) [Devenv コマンドラインスイッチ](../../ide/reference/devenv-command-line-switches.md) [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md) [/Clean (devenv.exe](../../ide/reference/clean-devenv-exe.md) ) [/out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
