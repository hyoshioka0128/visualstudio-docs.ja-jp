---
title: '方法: プログラムによってカスタムフォルダー項目を作成する'
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
ms.openlocfilehash: 034131f19c141f81922c843be0eb49e640dee858
ms.sourcegitcommit: f4b49f1fc50ffcb39c6b87e2716b4dc7085c7fb5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2020
ms.locfileid: "93399212"
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
