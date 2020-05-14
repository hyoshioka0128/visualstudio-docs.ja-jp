---
title: -Out (devenv.exe) | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
helpviewer_keywords:
- errors [Visual Studio], builds
- Devenv, /out switch
- builds [Visual Studio], logs
- error logs [Visual Studio], command-line build errors
- error logs [Visual Studio]
- /out Devenv switch
- out Devenv switch
- builds [Visual Studio], errors
- output files, build errors
ms.assetid: 9002d8c2-36d4-451c-b489-8f01932f31f7
caps.latest.revision: 14
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 075746353440462a66133cd83ed9158470d8de5b
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72662209"
---
# <a name="out-devenvexe"></a>/Out (devenv.exe)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

ソリューションを実行、ビルド、リビルド、または配置したときに、エラーを格納し表示するファイルを指定します。

## <a name="syntax"></a>構文

```
devenv /out FileName
```

## <a name="arguments"></a>引数
 `FileName` 必須。 実行可能ファイルのビルド時にエラーを受け取るファイルのパスと名前です。

## <a name="remarks"></a>解説
 指定したファイル名が存在しない場合は、自動的に作成されます。 ファイルが既に存在する場合、結果はファイルの既存の内容に追加されます。

 コマンド ラインのビルド エラーは、 **[コマンド]** ウィンドウと **[出力]** ウィンドウの [ソリューション ビルダー] ビューに表示されます。 このオプションは、無人操作でビルドを実行して結果を表示する必要がある場合に便利です。

## <a name="example"></a>例
 次の例では、`MySolution` を実行し、エラーをファイル `MyErrorLog.txt` に書き込みます。

```
devenv /run "C:\Documents and Settings\someuser\My Documents\Visual Studio\Projects\MySolution\MySolution.sln" /out "C:\MyErrorLog.txt"
```

## <a name="see-also"></a>関連項目
 [Devenv コマンドラインスイッチ (](../../ide/reference/devenv-command-line-switches.md) [devenv.exe)](../../ide/reference/run-devenv-exe.md) [/Build (devenv.exe](../../ide/reference/build-devenv-exe.md) ) [/Rebuild (](../../ide/reference/rebuild-devenv-exe.md) devenv.exe) [/Deploy (devenv.exe](../../ide/reference/deploy-devenv-exe.md) ) を実行します。
