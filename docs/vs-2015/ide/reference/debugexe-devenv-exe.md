---
title: -DebugExe (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- Devenv, /DebugExe switch
- DebugExe switch
- /DebugExe [devenv.exe]
ms.assetid: cd700006-1648-418f-924b-4b1e5c1412ab
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: f472add6b821693d1d48397e878db19e707e2868
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660801"
---
# <a name="debugexe-devenvexe"></a>/DebugExe (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

指定したデバッグ対象の実行可能ファイルを開きます。

## <a name="syntax"></a>構文

```
Devenv /debugexe ExecutableFile
```

## <a name="arguments"></a>引数
 `ExecutableFile` 必須。 .exe ファイルのパスとファイル名。

 .exe ファイルが見つからない場合、または存在しない場合、警告やエラーは表示されず、[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] は通常どおり起動します。

## <a name="remarks"></a>解説
 `ExecutableFile` パラメーターに続くどの文字列もそのファイルに引数として渡されます。

## <a name="example"></a>例
 次の例では、デバッグするために `MyApplication.exe` ファイルを開きます。

```
Devenv.exe /debugexe MyApplication.exe
```

## <a name="see-also"></a>関連項目
 [Devenv コマンド ライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
