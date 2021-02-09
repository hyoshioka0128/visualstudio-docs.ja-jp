---
title: '方法: プログラムによって Outlook の連絡先にアクセスする'
description: プログラムによって Outlook の連絡先にアクセスする方法について説明します。 この例では、指定された検索文字列が姓に含まれているすべての連絡先を検索します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- contacts [Office development in Visual Studio], searching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 7b82595aa3a09076b91211ba4ab45145b02ebcd9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99903736"
---
# <a name="how-to-programmatically-access-outlook-contacts"></a>方法: プログラムによって Outlook の連絡先にアクセスする
  この例では、指定された検索文字列が姓に含まれているすべての連絡先を検索します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_OL_AccessContacts#1](../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs#1)]
 [!code-csharp[Trin_OL_AccessContacts#1](../vsto/codesnippet/CSharp/Trin_OL_AccessContacts.trin_ol_accesscontacts/thisaddin.cs#1)]
 [!code-vb[Trin_OL_AccessContacts#1](../vsto/codesnippet/VisualBasic/Trin_OL_AccessContacts/thisaddin.vb#1)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- **連絡先** フォルダーに姓が含まれている **連絡先 (たとえば**、tzipi Butnaru)。

## <a name="see-also"></a>関連項目
- [連絡先アイテムの操作](../vsto/working-with-contact-items.md)
- [方法: プログラムによって Outlook の連絡先にエントリを追加する](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
- [方法: プログラムによって特定の連絡先を検索する](../vsto/how-to-programmatically-search-for-a-specific-contact.md)
- [方法: プログラムによって連絡先の電子メールアドレスを検索する](../vsto/how-to-programmatically-search-for-an-e-mail-address-in-contacts.md)
- [方法: プログラムによって Outlook の連絡先を削除する](../vsto/how-to-programmatically-delete-outlook-contacts.md)
