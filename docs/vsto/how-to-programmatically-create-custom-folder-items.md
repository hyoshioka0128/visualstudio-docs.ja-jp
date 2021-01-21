---
title: '方法: プログラムによってカスタムフォルダー項目を作成する'
description: Visual Studio を使用して、Microsoft Outlook でカスタムフォルダー項目をプログラムで作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], creating
- Outlook folders [Office development in Visual Studio], custom
author: John-Hart
ms.author: johnhart
ms.workload:
- office
ms.openlocfilehash: f149758665e5d7a7cdf7f4edd5d926e1de632dca
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97527788"
---
# <a name="how-to-programmatically-create-custom-folder-items"></a>方法: プログラムによってカスタムフォルダー項目を作成する
  この例では Microsoft Office Outlook で新しいフォルダーを作成します。 ログオンしたユーザーの名前は、フォルダー名として使用されます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_OL_CustFolderItem#1](../vsto/codesnippet/CSharp/Trin_OL_CustFolderItem/thisaddin.cs#1)]

## <a name="see-also"></a>関連項目
- [フォルダーの操作](../vsto/working-with-folders.md)
- [方法: プログラムによって Outlook の連絡先にエントリを追加する](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
- [方法: プログラムによって予定を作成する](../vsto/how-to-programmatically-create-appointments.md)
