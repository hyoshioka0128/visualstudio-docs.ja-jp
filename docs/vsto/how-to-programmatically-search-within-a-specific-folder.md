---
title: '方法: プログラムによって特定のフォルダー内を検索する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Outlook folders [Office development in Visual Studio], searching
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 8f5e0f098edcffce07eb2c3f243b994d1a53cdf9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85547018"
---
# <a name="how-to-programmatically-search-within-a-specific-folder"></a>方法: プログラムによって特定のフォルダー内を検索する
  このコード例では、メソッドとメソッドを使用して、 `Find` `FindNext` **受信トレイ**にある電子メールメッセージの件名フィールド内のテキストを検索します。 このメソッドでは、文字列フィルターを使用して、文字 T をテキストの開始文字として確認し `Subject` ます。

 [!INCLUDE[appliesto_olkallapp](../vsto/includes/appliesto-olkallapp-md.md)]

## <a name="example"></a>例
 [!code-csharp[Trin_OL_SearchFolder#1](../vsto/codesnippet/CSharp/Trin_OL_SearchFolder/thisaddin.cs#1)]

## <a name="see-also"></a>関連項目
- [フォルダーの操作](../vsto/working-with-folders.md)
- [Outlook オブジェクトモデルの概要](../vsto/outlook-object-model-overview.md)
- [方法: プログラムによって名前を指定してフォルダーを取得する](../vsto/how-to-programmatically-retrieve-a-folder-by-name.md)
