---
title: 右端で折り返す
description: コード エディターで [右端で折り返す] オプションをオンまたはオフにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/07/2018
ms.topic: how-to
helpviewer_keywords:
- word wrap
- editors, text viewing
- Code Editor, word wrap
ms.assetid: 442f33ef-9f52-4515-b55f-fb816d664645
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 20540fe7cc124c44cd1af0e031e10d5ee0b06ba1
ms.sourcegitcommit: 2cf87f79762906ccaa133a7645aa4c77a0bed7da
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96617423"
---
# <a name="how-to-manage-word-wrap-in-the-editor"></a>方法: エディターのワード ラップを管理する

**[右端で折り返す]** オプションを設定および解除できます。 このオプションを設定すると、コード エディター ウィンドウの現在の幅からはみ出した長い行の部分は次の行に表示されます。 たとえば行番号の使用を容易にするためにこのオプションをオフにすると、右にスクロールして長い行の末尾を表示できます。

> [!NOTE]
> このトピックは、Windows 上の Visual Studio に適用されます。 Visual Studio for Mac については、「[ソース エディター: 右端で折り返す](/visualstudio/mac/source-editor#word-wrap)」を参照してください。

## <a name="to-set-word-wrap-preferences"></a>ワード ラップ オプションを設定するには

1. **[ツール]** メニューの **[オプション]** を選択します。

2. **[テキスト エディター]** フォルダーで、 **[すべての言語]** サブフォルダーの **[全般]** オプションを選択して、このオプションをグローバルに設定します。

     または

     プログラミングしている言語のサブフォルダーの **[全般]** オプションを選択します。

3. **[設定]** で、 **[右端で折り返す]** オプションをオンまたはオフにします。

     **[右端で折り返す]** オプションをオンにすると、 **[右端の折り返しの記号を表示する]** オプションが有効になります。

4. 長い行が 2 行目に折り返される場合に改行インジケーターを表示するには、 **[折り返しの記号を表示する]** オプションをオンにします。 このオプションをオフにすると、インジケーターは表示されません。

    > [!NOTE]
    > 改行インジケーターはコードには追加されません。表示専用です。

## <a name="known-issues"></a>既知の問題

Notepad++、Sublime Text、Visual Studio Code での行の折り返しに慣れている場合は、Visual Studio の動作が他のエディターと異なる場合の次の問題に注意してください。

* [トリプル クリックで行全体が選択されない](https://developercommunity.visualstudio.com/content/problem/268989/triple-click-doesnt-select-whole-line-when-word-wr.html)
* [End キーを 2 回押してもカーソルが行末に移動しない](https://developercommunity.visualstudio.com/content/problem/138274/pressing-end-key-twice-should-move-cursor-to-end-o.html)

## <a name="see-also"></a>関連項目

- [コード エディターの機能](../../ide/writing-code-in-the-code-and-text-editor.md)
