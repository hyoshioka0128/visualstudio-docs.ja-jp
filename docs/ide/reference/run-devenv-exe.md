---
title: -Run (devenv.exe)
description: devenv の Run コマンドライン スイッチを使用して、指定したプロジェクトまたはソリューションをコンパイルして実行する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- /Run Devenv
- Run Devenv switch
- applications [Visual Studio], running
- /R Devenv switch
- Devenv, /Run switch
- R Devenv switch (/R)
ms.assetid: b1f22f9d-39a5-4918-8a2a-4b5c1e872665
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 34e9f50f864f8f2908a3822befda0652df6a3340
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99957921"
---
# <a name="run-devenvexe"></a>/Run (devenv.exe)

指定したプロジェクトまたはソリューションをコンパイルして実行します。

## <a name="syntax"></a>構文

```shell
devenv {/Run|/R} {SolutionName|ProjectName} [/Out OutputFilename]
```

## <a name="arguments"></a>引数

- *SolutionName*

  ソリューション ファイルの完全パスと名前。

- *ProjectName*

  プロジェクト ファイルの完全パスと名前。

- `/Out` *OutputFilename*

  省略可能。 ツールの出力を送信する先のファイル名。 このファイルが既に存在する場合、ファイルの末尾に出力が追加されます。

## <a name="remarks"></a>注釈

アクティブなソリューション構成に対して指定された設定に従って、指定したプロジェクトまたはソリューションをコンパイルして実行します。 このスイッチを指定すると、IDE が起動され、プロジェクトまたはソリューションの実行が完了しても IDE がアクティブな状態のままになります。

- 空白を含む文字列を二重引用符で囲みます。

- エラーなどの概要情報は、**[コマンド]** ウィンドウ、または `/Out`スイッチで指定した任意のログ ファイルに表示できます。

## <a name="example"></a>例

この例では、アクティブな配置構成を使用して、ソリューション `MySolution` を実行します。

```shell
devenv /run "%USERPROFILE%\source\repos\MySolution\MySolution.sln"
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
- [/Runexit (devenv.exe)](../../ide/reference/runexit-devenv-exe.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Out (devenv.exe)](../../ide/reference/out-devenv-exe.md)
