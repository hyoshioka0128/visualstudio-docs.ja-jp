---
title: '方法: プログラムによって web ページを Outlook フォルダーに関連付ける'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- folders [Office development in Visual Studio], Web pages and
- Outlook [Office development in Visual Studio], Web pages attached to folders
- Web pages [Office development in Visual Studio], Outlook folders
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: b8d44ffc46557243d2681b8f8b4a3b85d1cd9be6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85546147"
---
# <a name="how-to-programmatically-associate-a-web-page-with-an-outlook-folder"></a>方法: プログラムによって web ページを Outlook フォルダーに関連付ける
  この例では Microsoft Office Outlook でという名前のフォルダーがあるかどうかを確認 `HtmlView` します。 フォルダーが存在しない場合、コードによってフォルダーが作成され、そのフォルダーに Web ページが割り当てられます。 フォルダーが存在する場合は、このコードによってフォルダーの内容が表示されます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_OL_HTMLFolder#1](../vsto/codesnippet/CSharp/Trin_OL_HTMLFolder/thisaddin.cs#1)]

## <a name="see-also"></a>関連項目
- [フォルダーの操作](../vsto/working-with-folders.md)
- [方法: プログラムによって名前を指定してフォルダーを取得する](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [方法: プログラムによってカスタムフォルダー項目を作成する](../vsto/how-to-programmatically-create-custom-folder-items.md)
