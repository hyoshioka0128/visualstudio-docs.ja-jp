---
title: '方法: Outlook でフォーム領域が表示されないようにする'
description: Outlook が特定のアイテムのフォーム領域を表示しない Microsoft Office ようにする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- form regions [Office development in Visual Studio], canceling display
- canceling form region display
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f6e6b00e8e26d261aac18dd48af1d912bd6ffad1
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899544"
---
# <a name="how-to-prevent-outlook-from-displaying-a-form-region"></a>方法: Outlook でフォーム領域が表示されないようにする
  Outlook Microsoft Office 特定のアイテムのフォーム領域を表示しないようにする必要がある場合があります。 たとえば、連絡先アイテムに勤務先住所が含まれていない場合、マップ内のビジネスの場所を表示するフォーム領域が表示されないようにすることができます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="to-prevent-outlook-from-displaying-a-form-region"></a>Outlook でフォーム領域が表示されないようにするには

1. 変更するフォーム領域のコードファイルを開きます。

2. **フォーム領域ファクトリ** コード領域を展開します。

3. `FormRegionInitializing`クラスのプロパティを true に設定するコードをイベントハンドラーに追加 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> <xref:Microsoft.Office.Tools.Outlook.FormRegionInitializingEventArgs> します。 

   この例では、連絡先アイテムに住所が含まれていない場合、 <xref:System.ComponentModel.CancelEventArgs.Cancel%2A> プロパティは **true** に設定され、フォーム領域は表示されません。

## <a name="example"></a>例
 [!code-csharp[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/CSharp/Trin_Outlook_FR_Separate_O12/MapIt.cs#1)]
 [!code-vb[Trin_Outlook_FR_Separate#1](../vsto/codesnippet/VisualBasic/Trin_Outlook_FR_Separate_O12/MapIt.vb#1)]

## <a name="see-also"></a>関連項目
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [方法: フォーム領域を Outlook アドインプロジェクトに追加する](../vsto/how-to-add-a-form-region-to-an-outlook-add-in-project.md)
- [チュートリアル: Outlook フォーム領域のデザイン](../vsto/walkthrough-designing-an-outlook-form-region.md)
- [チュートリアル: Outlook でデザインされたフォーム領域をインポートする](../vsto/walkthrough-importing-a-form-region-that-is-designed-in-outlook.md)
