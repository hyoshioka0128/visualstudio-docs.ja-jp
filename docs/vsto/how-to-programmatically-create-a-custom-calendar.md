---
title: '方法: プログラムによってカスタムカレンダーを作成する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom calendars [Office development in Visual Studio]
- calendars [Office development in Visual Studio], custom
- appointments [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: aab9e14c7fa4b4c70b2e61eca382af2ce787148c
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85546056"
---
# <a name="how-to-programmatically-create-a-custom-calendar"></a>方法: プログラムによってカスタムカレンダーを作成する
  次の例では、"、" という名前の新しい予定表フォルダーを作成**し、新しい**予定アイテムを作成して予定表フォルダーに追加します。 次に、このコードによって Calendar フォルダーが表示されます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_OL_CustomCalendar#1](../vsto/codesnippet/CSharp/Trin_OL_CustomCalendar/thisaddin.cs#1)]

## <a name="see-also"></a>関連項目
- [予定表アイテムの操作](../vsto/working-with-calendar-items.md)
- [方法: プログラムによって予定を作成する](../vsto/how-to-programmatically-create-appointments.md)
- [方法: プログラムによって会議出席依頼を作成する](../vsto/how-to-programmatically-create-a-meeting-request.md)
