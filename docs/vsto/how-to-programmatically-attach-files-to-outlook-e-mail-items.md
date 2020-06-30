---
title: '方法: プログラムによって Outlook の電子メールアイテムにファイルを添付する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook [Office development in Visual Studio], attachments
- e-mail [Office development in Visual Studio], attachments
- mail items [Office development in Visual Studio], attachments
- attachments [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: a6cde83fa59f45cbc45e56738f09ccf3099f5c02
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546134"
---
# <a name="how-to-programmatically-attach-files-to-outlook-email-items"></a>方法: プログラムによって Outlook の電子メールアイテムにファイルを添付する
  この例では、新しいメールアイテムにファイルを添付し、それを Armando Pinto に送信します。 この例では、Armando Pinto という名前のユーザーが受信者として存在することを前提としています。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_Outlook_RL_AttachFiles#1](../vsto/codesnippet/CSharp/Trin_Outlook_RL_AttachFiles/thisaddin.cs#1)]
 [!code-vb[Trin_Outlook_RL_AttachFiles#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_RL_AttachFiles/thisaddin.vb#1)]

## <a name="see-also"></a>関連項目
- [メールアイテムの操作](../vsto/working-with-mail-items.md)
- [方法: プログラムによって電子メールを送信する](../vsto/how-to-programmatically-send-e-mail-programmatically.md)
- [方法: プログラムによって Outlook の電子メールアイテムから添付ファイルを保存する](../vsto/how-to-programmatically-save-attachments-from-outlook-e-mail-items.md)
- [方法: プログラムによって電子メールアイテムを作成する](../vsto/how-to-programmatically-create-an-e-mail-item.md)
