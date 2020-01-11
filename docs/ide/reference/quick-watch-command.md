---
title: QuickWatch コマンド
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- debug.quickwatch
helpviewer_keywords:
- Quick Watch command
- Debug.Quickwatch command
ms.assetid: 9670ac3a-8f2f-4874-974d-cb87d3b0cde1
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8f6382a79884bf8c3891a3a191b594bf183efb62
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75565631"
---
# <a name="quick-watch-command"></a>QuickWatch コマンド
選択または指定したテキストが [[クイック ウォッチ]](../../debugger/watch-and-quickwatch-windows.md) ウィンドウの [式] フィールドに表示されます。 このダイアログ ボックスを利用し、デバッガーが認識する変数または式の現在値やレジスタのコンテンツの現在値を計算できます。 さらに、非定数の変数の値やレジストリのコンテンツの値を変更できます。

## <a name="syntax"></a>構文

```cmd
Debug.QuickWatchq [text]
```

## <a name="arguments"></a>引数

`text`\
任意。 **[クイック ウォッチ]** ダイアログ ボックスに追加するテキスト。

## <a name="remarks"></a>Remarks

`text` を省略した場合、カーソルで現在選択されているテキストや単語がウォッチ ウィンドウに追加されます。

## <a name="example"></a>例

```cmd
>Debug.QuickWatch
```

## <a name="see-also"></a>関連項目

- [Visual Studio でウォッチ ウィンドウとクイック ウォッチ ウィンドウを使用して変数のウォッチ ポイントを設定する](../../debugger/watch-and-quickwatch-windows.md)
- [Visual Studio のコマンド](../../ide/reference/visual-studio-commands.md)
- [コマンド ウィンドウ](../../ide/reference/command-window.md)
- [検索コマンド ボックス](../../ide/find-command-box.md)
- [Visual Studio Command Aliases](../../ide/reference/visual-studio-command-aliases.md)
