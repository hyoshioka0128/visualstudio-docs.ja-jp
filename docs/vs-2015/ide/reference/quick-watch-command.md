---
title: QuickWatch コマンド | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- debug.quickwatch
helpviewer_keywords:
- Quick Watch command
- Debug.Quickwatch command
ms.assetid: 9670ac3a-8f2f-4874-974d-cb87d3b0cde1
caps.latest.revision: 18
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: da9ba9572e121a9eba74cd8d624789032f1bb4a1
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MTE95
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665669"
---
# <a name="quick-watch-command"></a>QuickWatch コマンド
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

選択または指定したテキストが [[クイック ウォッチ] ダイアログ ボックス](https://msdn.microsoft.com/library/ffaee1dd-e5ce-4ef2-9401-d28329398867)の [式] フィールドに表示されます。 このダイアログ ボックスを利用し、デバッガーが認識する変数または式の現在値やレジスタのコンテンツの現在値を計算できます。 さらに、非定数の変数の値やレジストリのコンテンツの値を変更できます。

## <a name="syntax"></a>構文

```
Debug.QuickWatchq [text]
```

## <a name="arguments"></a>引数
 `text` 省略可能。 **[クイック ウォッチ]** ダイアログ ボックスに追加するテキスト。

## <a name="remarks"></a>解説
 `text` を省略した場合、カーソルで現在選択されているテキストや単語がウォッチ ウィンドウに追加されます。

## <a name="example"></a>例

```
>Debug.QuickWatch
```

## <a name="see-also"></a>関連項目
 [方法: [クイックウォッチ] ダイアログボックスを使用](https://msdn.microsoft.com/library/ffaee1dd-e5ce-4ef2-9401-d28329398867)[する visual studio コマンド](../../ide/reference/visual-studio-commands.md)の[コマンドウィンドウ](../../ide/reference/command-window.md)[検索/コマンドボックス](../../ide/find-command-box.md) [visual studio コマンドのエイリアス](../../ide/reference/visual-studio-command-aliases.md)
