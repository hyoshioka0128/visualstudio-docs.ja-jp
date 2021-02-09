---
title: Web ページを Outlook フォルダーに関連付ける
description: Web ページを Microsoft Office Outlook フォルダーに関連付ける方法について説明します。 この例では、Outlook で HtmlView という名前のフォルダーがあるかどうかを確認します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 35fad43f78d654cfaf9e06c1f432c620da830dd4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99885574"
---
# <a name="associate-a-web-page-with-an-outlook-folder"></a>Web ページを Outlook フォルダーに関連付ける

  この例では Microsoft Office Outlook でという名前のフォルダーがあるかどうかを確認 `HtmlView` します。 フォルダーが存在しない場合、コードによってフォルダーが作成され、そのフォルダーに Web ページが割り当てられます。 フォルダーが存在する場合は、このコードによってフォルダーの内容が表示されます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_OL_HTMLFolder#1](../vsto/codesnippet/CSharp/Trin_OL_HTMLFolder/thisaddin.cs#1)]

## <a name="see-also"></a>関連項目
- [フォルダーの操作](../vsto/working-with-folders.md)
- [方法: プログラムによって名前を指定してフォルダーを取得する](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
- [方法: プログラムによってカスタムフォルダー項目を作成する](../vsto/how-to-programmatically-create-custom-folder-items.md)
