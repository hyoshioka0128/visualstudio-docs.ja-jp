---
title: -Runexit (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- runexit Devenv switch
- Devenv, /runexit switch
- /runexit Devenv switch
ms.assetid: bfc94875-5fc0-4110-b961-d59c0b403790
caps.latest.revision: 13
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 6d1158a12de8b8adfe20fa6d045b756abf8d7b3c
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665493"
---
# <a name="runexit-devenvexe"></a>/Runexit (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定したプロジェクトまたはソリューションをコンパイルおよび実行してから、統合開発環境 (IDE) を閉じます。

## <a name="syntax"></a>構文

```
devenv /runexit {SolutionName|ProjectName}
```

## <a name="arguments"></a>引数
 `SolutionName` 必須。 ソリューション ファイルの完全パスと名前。

 `ProjectName` 必須。 プロジェクト ファイルの完全パスと名前。

## <a name="remarks"></a>解説
 アクティブなソリューション構成に対して指定された設定に従って、指定したプロジェクトまたはソリューションをコンパイルして実行します。 このスイッチはプロジェクトまたはソリューションの実行中に IDE を最小化し、プロジェクトまたはソリューションの実行の完了後に IDE を閉じます。

- 空白を含む文字列を二重引用符で囲みます。

- エラーなどの概要情報は、 **[コマンド]** ウィンドウ、または `/out`スイッチで指定した任意のログ ファイルに表示できます。

## <a name="example"></a>例
 この例では、アクティブな配置構成を使用し、IDE を最小化した状態でソリューション `MySolution` を実行してから IDE を閉じます。

```
devenv /runexit "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln"
```

## <a name="see-also"></a>関連項目
 [Devenv コマンドラインスイッチ $](../../ide/reference/devenv-command-line-switches.md) [(devenv.exe)](../../ide/reference/run-devenv-exe.md) [/Build (devenv.exe](../../ide/reference/build-devenv-exe.md) ) [/Rebuild (](../../ide/reference/rebuild-devenv-exe.md) devenv.exe) [/out (devenv.exe](../../ide/reference/out-devenv-exe.md) ) (devenv.exe)
