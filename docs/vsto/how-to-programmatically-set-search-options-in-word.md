---
title: '方法: プログラムによって Word の検索オプションを設定する'
description: Visual Studio を使用して、Microsoft Word での選択項目の検索オプションをプログラムで設定する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- settings, Word search options
- documents [Office development in Visual Studio], search options
- Word, searching options
- searching, Word options
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 605f782bf6dc3bb56b52bdcd896d1c6419cf5f51
ms.sourcegitcommit: 4b40aac584991cc2eb2186c3e4f4a7fcd522f607
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/21/2021
ms.locfileid: "107825031"
---
# <a name="how-to-programmatically-set-search-options-in-word"></a>方法: プログラムによって Word の検索オプションを設定する
  Microsoft Office Word 文書で選択する検索オプションを設定するには、次の2つの方法があります。

- オブジェクトの個々のプロパティを設定 <xref:Microsoft.Office.Interop.Word.Find> します。

- <xref:Microsoft.Office.Interop.Word.Find.Execute%2A>オブジェクトのメソッドの引数を使用 <xref:Microsoft.Office.Interop.Word.Find> します。

  [!INCLUDE[appliesto_wdalldocapp](../vsto/includes/appliesto-wdalldocapp-md.md)]

## <a name="use-properties-of-a-find-object"></a>Find オブジェクトのプロパティを使用する
 次のコードは、オブジェクトのプロパティを設定して <xref:Microsoft.Office.Interop.Word.Find> 、現在の選択範囲内のテキストを検索します。 検索の検索、折り返し、テキスト検索などの検索条件がオブジェクトのプロパティであることに注意して <xref:Microsoft.Office.Interop.Word.Find> ください。

 C# コードを記述する場合、オブジェクトの各プロパティを設定すること <xref:Microsoft.Office.Interop.Word.Find> は、メソッドでパラメーターとして同じプロパティを指定する必要があるため、役に立ちません <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> 。 したがって、この例には Visual Basic コードのみが含まれています。

### <a name="to-set-search-options-using-a-find-object"></a>検索オブジェクトを使用して検索オプションを設定するには

1. オブジェクトのプロパティを設定し <xref:Microsoft.Office.Interop.Word.Find> て、[ **検索** する文字列] テキストの選択範囲を前方に検索します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet76":::

## <a name="use-execute-method-arguments"></a>Execute メソッドの引数を使用する
 次のコードでは、オブジェクトのメソッドを使用して <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> <xref:Microsoft.Office.Interop.Word.Find> 、現在の選択範囲内のテキストを検索します。 検索対象の検索、折り返し、テキスト検索などの検索条件は、メソッドのパラメーターとして渡されることに注意して <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> ください。

### <a name="to-set-search-options-using-execute-method-arguments"></a>Execute メソッドの引数を使用して検索オプションを設定するには

1. 検索条件をメソッドのパラメーターとして渡して、検索 <xref:Microsoft.Office.Interop.Word.Find.Execute%2A> するテキストの選択範囲を前方に検索します。

     :::code language="vb" source="../vsto/codesnippet/VisualBasic/Trin_VstcoreWordAutomationVB/ThisDocument.vb" id="Snippet77":::
     :::code language="csharp" source="../vsto/codesnippet/CSharp/Trin_VstcoreWordAutomationCS/ThisDocument.cs" id="Snippet77":::

## <a name="see-also"></a>関連項目
- [方法: プログラムによって文書内のテキストを検索および置換する](../vsto/how-to-programmatically-search-for-and-replace-text-in-documents.md)
- [方法: ドキュメント内の見つかった項目をプログラムによってループする](../vsto/how-to-programmatically-loop-through-found-items-in-documents.md)
- [方法: プログラムによって検索後に選択を復元する](../vsto/how-to-programmatically-restore-selections-after-searches.md)
