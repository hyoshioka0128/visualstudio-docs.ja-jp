---
title: Watch コマンド
description: Watch コマンドと、それを使用して、指定したインスタンスのウォッチ ウィンドウを作成し、開く方法を説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.watch
helpviewer_keywords:
- Watch command
- Debug.Watch command
ms.assetid: aa02e647-d9f5-4905-a651-52a8df595795
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 631c9cf61e6da70b3c7554a1aac0cacc8eef0294
ms.sourcegitcommit: df6ba39a62eae387e29f89388be9e3ee5ceff69c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/02/2020
ms.locfileid: "96480149"
---
# <a name="watch-command"></a>Watch コマンド
指定したインスタンスの **[ウォッチ]** ウィンドウを作成し、開きます。 **[ウォッチ]** ウィンドウを使用すると、変数、式、レジスタの値の計算し、それらの値を編集し、結果を保存することができます。

## <a name="syntax"></a>構文

```cmd
Debug.Watch[index]
```

## <a name="arguments"></a>引数

`index`\
必須です。 [ウォッチ] ウィンドウのインスタンス番号。

## <a name="remarks"></a>注釈

`index` は整数でなければなりません。 有効値は 1、2、3、または 4 です。

## <a name="example"></a>例

```cmd
>Debug.Watch1
```

## <a name="see-also"></a>関連項目

- [[自動変数] ウィンドウと [ローカル] ウィンドウ](../../debugger/autos-and-locals-windows.md)
- [Visual Studio でウォッチ ウィンドウとクイック ウォッチ ウィンドウを使用して変数のウォッチ ポイントを設定する](../../debugger/watch-and-quickwatch-windows.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
