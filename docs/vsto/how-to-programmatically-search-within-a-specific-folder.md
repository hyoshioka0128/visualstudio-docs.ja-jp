---
title: '方法: プログラムによって特定のフォルダー内を検索する'
description: Visual Studio を使用して、特定の Microsoft Outlook フォルダー内でプログラムによって検索する方法について説明します。
ms.custom: SEO-VS-2020
titleSuffix: ''
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], searching
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: a9c7861698e678ca6d8332e3940c3ae49ff423f3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99877877"
---
# <a name="how-to-programmatically-search-within-a-specific-folder"></a>方法: プログラムによって特定のフォルダー内を検索する
  このコード例では、メソッドとメソッドを使用して、 `Find` `FindNext` **受信トレイ** にある電子メールメッセージの件名フィールド内のテキストを検索します。 このメソッドでは、文字列フィルターを使用して、文字 T をテキストの開始文字として確認し `Subject` ます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_OL_SearchFolder#1](../vsto/codesnippet/CSharp/Trin_OL_SearchFolder/thisaddin.cs#1)]

## <a name="see-also"></a>関連項目
- [フォルダーの操作](../vsto/working-with-folders.md)
- [Outlook オブジェクトモデルの概要](../vsto/outlook-object-model-overview.md)
- [方法: プログラムによって名前を指定してフォルダーを取得する](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
