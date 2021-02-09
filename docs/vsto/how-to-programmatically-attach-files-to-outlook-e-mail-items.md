---
title: '方法: プログラムによって Outlook の電子メールアイテムにファイルを添付する'
description: Outlook アイテム Microsoft Office にファイルを添付する方法について説明します。 この例では、新しいメールアイテムにファイルを添付し、それを Armando Pinto に送信します。
ms.custom: SEO-VS-2020
titleSuffix: ''
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 972203b5306d3fa7c94461b235c204051871c33c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99892087"
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
