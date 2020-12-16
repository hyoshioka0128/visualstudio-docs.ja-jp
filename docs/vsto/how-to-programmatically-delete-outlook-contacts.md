---
title: '方法: プログラムによって Outlook の連絡先を削除する'
description: Microsoft Outlook でプログラムを使用して連絡先を削除する方法について説明します。 この例では、1つの連絡先を削除します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- deleting contacts
- contacts [Office development in Visual Studio], deleting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: f1398a631db77704a89a06b5e66ef4cb370280e4
ms.sourcegitcommit: 4bd2b770e60965fc0843fc25318a7e1b46137875
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/15/2020
ms.locfileid: "97528296"
---
# <a name="how-to-programmatically-delete-outlook-contacts"></a>方法: プログラムによって Outlook の連絡先を削除する
  この例では、連絡先を 1 件削除します。 この例では、"Armando Pinto" という名前の連絡先が **[Contacts]** フォルダーに存在することを前提にしています。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-vb[Trin_Outlook_RL_DeleteContacts#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_RL_DeleteContacts/thisaddin.vb#1)]
 [!code-csharp[Trin_Outlook_RL_DeleteContacts#1](../vsto/codesnippet/CSharp/Trin_Outlook_RL_DeleteContacts/thisaddin.cs#1)]

## <a name="see-also"></a>関連項目
- [連絡先アイテムの操作](../vsto/working-with-contact-items.md)
- [方法: プログラムによって特定の連絡先を検索する](../vsto/how-to-programmatically-search-for-a-specific-contact.md)
- [方法: プログラムによって Outlook の連絡先にアクセスする](../vsto/how-to-programmatically-access-outlook-contacts.md)
