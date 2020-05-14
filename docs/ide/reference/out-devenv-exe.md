---
title: -Out (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- errors [Visual Studio], builds
- Devenv, /Out switch
- builds [Visual Studio], logs
- error logs [Visual Studio], command-line build errors
- error logs [Visual Studio]
- /Out Devenv switch
- Out Devenv switch
- builds [Visual Studio], errors
- output files, build errors
ms.assetid: 9002d8c2-36d4-451c-b489-8f01932f31f7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: cda81d37be0246c1181b4d82cbd17c3119b94437
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "75568012"
---
# <a name="out-devenvexe"></a>/Out (devenv.exe)

ソリューションの[実行](run-devenv-exe.md)、[実行と終了](runexit-devenv-exe.md)、[アップグレード](upgrade-devenv-exe.md)、[ビルド](build-devenv-exe.md)、[リビルド](rebuild-devenv-exe.md)、[消去](clean-devenv-exe.md)、または[配置](deploy-devenv-exe.md)を行ったときに、エラーを格納し表示するファイルを指定します。

## <a name="syntax"></a>構文

```shell
devenv /Out FileName
```

## <a name="arguments"></a>引数

- *FileName*

  必須。 実行可能ファイルのビルド時に出力を受け取るファイルのパスと名前です。

## <a name="remarks"></a>解説

指定したファイル名が存在しない場合は、ファイルが自動的に作成されます。 ファイルが既に存在する場合、結果はファイルの既存の内容に追加されます。

コマンドラインのビルド エラーは、 **[コマンド]** ウィンドウと **[出力]** ウィンドウの [ソリューション ビルダー] ビューに表示されます。 このスイッチは、自動ビルドの結果を表示する場合に便利です。

## <a name="example"></a>例

次の例では、`MySolution` を実行し、エラーをファイル `MyErrorLog.txt` に書き込みます。

```shell
devenv /run "%USERPROFILE%\source\repos\MySolution\MySolution.sln" /out "C:\MyErrorLog.txt"
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
- [/Run (devenv.exe)](../../ide/reference/run-devenv-exe.md)
- [/RunExit (devenv.exe)](runexit-devenv-exe.md)
- [/Upgrade (devenv.exe)](upgrade-devenv-exe.md)
- [/Clean (devenv.exe)](clean-devenv-exe.md)
- [/Build (devenv.exe)](../../ide/reference/build-devenv-exe.md)
- [/Rebuild (devenv.exe)](../../ide/reference/rebuild-devenv-exe.md)
- [/Deploy (devenv.exe)](../../ide/reference/deploy-devenv-exe.md)
