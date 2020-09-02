---
title: プログラムによって連絡先の電子メールアドレスを検索する
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- e-mail [Office development in Visual Studio], searching
- contacts [Office development in Visual Studio], searching
- searching contacts
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a4a9d52ae16b77b40461a314c6008f8cdd741bcd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85537645"
---
# <a name="how-to-programmatically-search-for-an-email-address-in-contacts"></a>方法: プログラムによって連絡先の電子メールアドレスを検索する
  この例では、連絡先フォルダーから、電子メール アドレスに **example.com** というドメイン名が含まれている連絡先を検索します。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_OL_SearchEmail#1](../vsto/codesnippet/CSharp/Trin_OL_SearchEmail/thisaddin.cs#1)]

## <a name="compile-the-code"></a>コードのコンパイル
 この例で必要な要素は次のとおりです。

- 電子メール アドレスに **example.com** というドメイン名が含まれており (たとえば、 `somebody@example.com`)、姓と名が設定されている連絡先。

## <a name="see-also"></a>関連項目
- [連絡先アイテムの操作](../vsto/working-with-contact-items.md)
- [方法: プログラムによって電子メールを送信する](../vsto/how-to-programmatically-send-e-mail-programmatically.md)
- [方法: プログラムによって Outlook の連絡先にアクセスする](../vsto/how-to-programmatically-access-outlook-contacts.md)
- [方法: プログラムによって Outlook の連絡先にエントリを追加する](../vsto/how-to-programmatically-add-an-entry-to-outlook-contacts.md)
