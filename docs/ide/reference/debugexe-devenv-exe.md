---
title: -DebugExe (devenv.exe)
description: devenv の DebugExe コマンドライン スイッチを使用して、指定したデバッグ対象の実行可能ファイルを開く方法について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 5cdf770446b78b1a1bb4b55d61f4c3e9f50c4035
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894609"
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

## <a name="remarks"></a>注釈

*ExecutableFile* パラメーターに続くどの文字列もそのファイルに引数として渡されます。

## <a name="example"></a>例

次の例では、デバッグするために `MyApplication.exe` ファイルを開きます。

```shell
devenv /debugexe MyApplication.exe
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
