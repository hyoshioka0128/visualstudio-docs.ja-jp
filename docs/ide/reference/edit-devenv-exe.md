---
title: -Edit (devenv.exe)
ms.date: 12/10/2018
ms.topic: reference
helpviewer_keywords:
- Edit Devenv switch
- Devenv, /Edit switch
- /Edit Devenv switch
ms.assetid: 02b3d6e7-a2b1-4d83-a747-aa8c2fb758b7
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: d180d5a5d723d8085537f2993aac022d74df2c08
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75595697"
---
# <a name="edit-devenvexe"></a>/Edit (devenv.exe)

指定されたファイルを Visual Studio の既存のインスタンスで開きます。

## <a name="syntax"></a>構文

```shell
devenv /Edit [File1[ FileN]...]
```

## <a name="arguments"></a>引数

- *File1*

  任意。 Visual Studio の既存のインスタンスで開くファイル。 Visual Studio のインスタンスが存在していない場合は、簡略化されたウィンドウ レイアウトで新しいインスタンスが作成され、その新しいインスタンスで *File1* が開かれます。

- *FileN*

  任意。 Visual Studio の既存インスタンスで開く 1 つ以上の追加ファイル。

## <a name="remarks"></a>Remarks

ファイルが指定されていない場合は、既存の Visual Studio インスタンスがフォーカスを受け取ります。 ファイルが指定されておらず、Visual Studio のインスタンスが存在しない場合、簡略化されたウィンドウ レイアウトでインスタンスが作成されます。

既存の Visual Studio インスタンスがモーダル状態の場合、Visual Studio がモーダル状態を終了すると、ファイルが既存のインスタンスで開かれます。 たとえば、[[オプション] ダイアログ ボックス](../../ide/reference/options-dialog-box-visual-studio.md)が開かれているときにこのような状況が発生することがあります。

Visual Studio の複数のインスタンスが開いている場合、ファイルは最後に開いたインスタンスで開きます。

## <a name="example"></a>例

最初の例では、ファイル `MyFile.cs` を Visual Studio の既存のインスタンスで開きます。 Visual Studio インスタンスが存在しない場合、新しいインスタンスでファイルが開かれます。 2 つ目の例は似ていますが、1 つのファイルだけではなく 3 つのファイルを開くという点が異なります。

```shell
devenv /edit MyFile.cs

devenv /edit MyFile1.cs MyFile2.cs MyFile3.cs
```

## <a name="see-also"></a>関連項目

- [Devenv コマンドライン スイッチ](../../ide/reference/devenv-command-line-switches.md)
