---
title: -DebugExe (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /DebugExe switch
- DebugExe switch
- /DebugExe [devenv.exe]
- debugging executables
ms.assetid: cd700006-1648-418f-924b-4b1e5c1412ab
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: aeae28288936b6723b53e826142a4888ad0bc8b4
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75570142"
---
# <a name="debugexe-devenvexe"></a>/DebugExe (devenv.exe)

指定したデバッグ対象の実行可能ファイルを開きます。

## <a name="syntax"></a>構文

```shell
devenv /DebugExe ExecutableFile
```

## <a name="arguments"></a>引数

- *ExecutableFile*

  必須。 `.exe` ファイルのパスとファイル名。 `.exe` ファイルが見つからない場合、または存在しない場合、警告やエラーは表示されず、Visual Studio は通常どおり起動します。

## <a name="remarks"></a>解説

*ExecutableFile* パラメーターに続くどの文字列もそのファイルに引数として渡されます。

## <a name="example"></a>例

次の例では、デバッグするために `MyApplication.exe` ファイルを開きます。

```shell
devenv /debugexe MyApplication.exe
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
