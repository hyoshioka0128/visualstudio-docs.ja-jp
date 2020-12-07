---
title: コード スニペット ピッカー
description: コード スニペット ピッカーを使用して、既成のコード ブロックをアクティブなドキュメントに挿入する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.expansionpicker
helpviewer_keywords:
- Code Snippet Picker
- IntelliSense code snippets, Code Snippet Picker
- code snippets, Code Snippet Picker
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: bf0b1c264911c92389c6c3afe722b5061455c3da
ms.sourcegitcommit: 967c2f8c1b3f805cf42c0246389517689d971b53
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "96041019"
---
# <a name="code-snippet-picker"></a>コード スニペット ピッカー

Visual Studio コード エディターでは、**コード スニペット ピッカー** が提供されています。これを使うと、数回マウスをクリックするだけで、既成のコードのブロックをアクティブなドキュメントに挿入することができます。

**コード スニペット ピッカー** を表示する手順は、使用している言語によって異なります。

- Visual Basic: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、**[スニペットの挿入]** を選択します。

- C#: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、**[スニペットの挿入]** または **[ブロックの挿入]** をクリックします。

- C++: **コード スニペット ピッカー** は使用できません。

- F#: **コード スニペット ピッカー** は使用できません。

- JavaScript: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、**[スニペットの挿入]** または **[ブロックの挿入]** をクリックします。

- XML: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、**[スニペットの挿入]** または **[ブロックの挿入]** をクリックします。

- HTML: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、**[スニペットの挿入]** または **[ブロックの挿入]** をクリックします。

- SQL: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、**[スニペットの挿入]** をクリックします。

ほとんどの Visual Studio 開発言語では、**コード スニペット マネージャー** を使って、**コード スニペット ピッカー** が XML スニペット ファイルをスキャンするフォルダー一覧にフォルダーを追加することができます。 独自のスニペットを作成して一覧に追加することもできます。 詳細については、「[チュートリアル:コード スニペットを作成する](../../ide/walkthrough-creating-a-code-snippet.md)」をご覧ください。

## <a name="uielement-list"></a>UIElement の一覧

Item Name

**[項目一覧]** で選択した項目の名前を表示する編集可能なテキスト フィールドです。 目的の項目のインクリメンタル検索を実行するには、このフィールドで名前の入力を開始します。 **[項目一覧]** で目的の項目が選択されるまで、文字の追加を続けます。

項目一覧

挿入に使用できるコード スニペットの一覧、またはコード スニペットを含むフォルダーの一覧です。 スニペットを挿入またはフォルダーを展開するには、目的の項目を選択して Enter キーを押します。

## <a name="see-also"></a>関連項目

- [コード スニペットを使用するためのベスト プラクティス](../../ide/best-practices-for-using-code-snippets.md)
- [Visual Basic の IntelliSense コード スニペット](/dotnet/visual-basic/developing-apps/using-ide/intellisense-code-snippets)
- [コードへのブックマークの設定](../../ide/setting-bookmarks-in-code.md)
- [方法: surround-with コード スニペットを使用する](../../ide/how-to-use-surround-with-code-snippets.md)
