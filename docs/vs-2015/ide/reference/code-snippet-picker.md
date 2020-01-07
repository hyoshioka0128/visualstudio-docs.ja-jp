---
title: コード スニペット ピッカー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vs.expansionpicker
helpviewer_keywords:
- Code Snippet Picker
- IntelliSense code snippets, Code Snippet Picker
- code snippets, Code Snippet Picker
ms.assetid: f0862d48-fbbc-4cfe-b228-24492d5c89c4
caps.latest.revision: 29
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 2918826d6923efa3db42f4f572c416b9668513a9
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72660897"
---
# <a name="code-snippet-picker"></a>コード スニペット ピッカー
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Code エディターでは、**コード スニペット ピッカー**が提供されています。これを使用すると、数回マウスをクリックするだけで、既成のコードのブロックをアクティブなドキュメントに挿入することができます。

 **コード スニペット ピッカー**を表示する手順は、使用している言語によって異なります。

- [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、 **[スニペットの挿入]** を選択します。

- [!INCLUDE[csprcs](../../includes/csprcs-md.md)]: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、 **[スニペットの挿入]** または **[ブロックの挿入]** をクリックします。

- [!INCLUDE[vcprvc](../../includes/vcprvc-md.md)]: **コード スニペット ピッカー**は使用できません。

- Visual F#: **コード スニペット ピッカー**は使用できません。

- [!INCLUDE[jsprjscript](../../includes/jsprjscript-md.md)]: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、 **[スニペットの挿入]** または **[ブロックの挿入]** をクリックします。

- XML: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、 **[スニペットの挿入]** または **[ブロックの挿入]** をクリックします。

- HTML: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、 **[スニペットの挿入]** または **[ブロックの挿入]** をクリックします。

- SQL: コード エディターで目的の場所を右クリックしてショートカット メニューを表示し、 **[スニペットの挿入]** をクリックします。

  ほとんどの Visual Studio 開発言語では、**コード スニペット マネージャー**を使用して、**コード スニペット ピッカー**が XML スニペット ファイルをスキャンする**フォルダー一覧**にフォルダーを追加することができます。 独自のスニペットを作成して一覧に追加することもできます。 詳細については、「[チュートリアル: コード スニペットを作成する](../../ide/walkthrough-creating-a-code-snippet.md)」を参照してください。

## <a name="uielement-list"></a>UIElement の一覧
 項目名**項目の一覧**で選択された項目の名前を表示する編集可能なテキストフィールドです。 目的の項目のインクリメンタル検索を実行するには、このフィールドで名前の入力を開始します。 **[項目一覧]** で目的の項目が選択されるまで、文字の追加を続けます。

 項目リスト挿入に使用できるコードスニペットの一覧、またはコードスニペットを含むフォルダーの一覧。 スニペットを挿入またはフォルダーを展開するには、目的の項目を選択して Enter キーを押します。

## <a name="see-also"></a>参照
 [コードスニペットを使用するためのベストプラクティス](../../ide/best-practices-for-using-code-snippets.md) [Visual Basic IntelliSense コードスニペット](https://msdn.microsoft.com/library/ffdde4c9-8141-4906-b09b-15181357a643)コード[にブックマークを設定](../../ide/setting-bookmarks-in-code.md)[する方法: ブロックコードスニペットを使用する](../../ide/how-to-use-surround-with-code-snippets.md)
