---
title: -Diff (devenv.exe)
description: Diff devenv コマンド ライン スイッチを使用して 2 つのファイルを比較する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Devenv, /Diff switch
- /Diff Devenv switch
- Diff Devenv switch
ms.assetid: 5377fedb-632a-4e86-a947-7c11c86451e7
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: b1a8c4c8868de187b9e9aa5183e44c29145220e1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99882148"
---
# <a name="diff-devenvexe"></a>/Diff (devenv.exe)

2 つのファイルを比較します。 相違点は特殊な Visual Studio のウィンドウに表示されます。

## <a name="syntax"></a>構文

```shell
devenv /Diff SourceFile TargetFile [SourceDisplayName [TargetDisplayName]]
```

## <a name="arguments"></a>引数

- *SourceFile*

  必須。 比較する最初のファイルの完全パスと名前。

- *TargetFile*

  必須。 比較する 2 つ目のファイルの完全なパスと名前。

- *SourceDisplayName*

  任意。 最初のファイルの表示名。

- *TargetDisplayName*

  任意。 2 番目のファイルの表示名。

## <a name="remarks"></a>注釈

IDE のインスタンスが既に開かれている場合は、現在の IDE のタブにファイルの比較が表示されます。

## <a name="example"></a>例

最初の例では、表示名を変更せずに 2 つのファイルを比較します。 2 つ目の例では、両方の表示名を変更してファイルを比較します。 3 つ目と 4 つ目の例では、2 つのファイルを比較しますが、最初のファイルまたは 2 つ目のファイルにのみエイリアスを適用します。

```shell
devenv /diff File1.txt File2.txt

devenv /diff File1.txt File2.txt FirstAlias "Second Alias"

devenv /diff File1.txt File2.txt "File One"

devenv /diff File1.txt File2.txt "" FileTwo
```

## <a name="see-also"></a>参照

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
