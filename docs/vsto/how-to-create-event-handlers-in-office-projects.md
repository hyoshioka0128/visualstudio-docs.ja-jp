---
title: '方法: Office プロジェクトでイベントハンドラーを作成する'
description: Visual Basic と C# でコントロールの既定のイベントハンドラーを作成するいくつかの方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Visual Basic [Office development in Visual Studio], event handlers
- event handlers [Office development in Visual Studio]
- Visual C# [Office development in Visual Studio], event handlers
- events [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: b2aed6102b6aed5938ecfab826363e62dcfac48a
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99889422"
---
# <a name="how-to-create-event-handlers-in-office-projects"></a>方法: Office プロジェクトでイベントハンドラーを作成する
  Visual Basic と C# でイベントハンドラーを作成するには、いくつかの方法があります。 デザインビューでコントロールの既定のイベントハンドラーを作成するには、コントロールをダブルクリックするか、[ **プロパティ** ] ウィンドウの [イベント] ペインを使用して、コントロール上の任意のイベントのハンドラーを作成します。 ただし、コードビューでは、デザインビューに切り替えてイベントハンドラーを作成する必要がない場合があります。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

 [!INCLUDE[note_settings_general](../sharepoint/includes/note-settings-general-md.md)]

### <a name="to-create-an-event-handler-in-visual-basic"></a>Visual Basic でイベントハンドラーを作成するには

1. コードエディターの上部にある [ **クラス名** ] ドロップダウンリストから、イベントハンドラーを作成するオブジェクトを選択します。

    > [!NOTE]
    > またはのイベントハンドラーを作成する場合は `ThisDocument` `ThisWorkbook` 、[**クラス名**] ボックスの一覧で **(ThisDocument Events)** または **(ThisWorkbook events)** を選択する必要があります。

2. コードエディターの上部にある [ **メソッド名** ] ボックスの一覧で、イベントを選択します。

     Visual Studio によってイベントハンドラーが作成され、挿入ポイントが新しく作成されたイベントハンドラーに移動します。 イベントハンドラーが既に存在する場合、挿入ポイントは既存のイベントハンドラーに移動します。

### <a name="to-create-an-event-handler-in-c"></a>C でイベントハンドラーを作成するには\#

1. 修飾されたイベント名の後にスペースを入力し、後にスペースを入力せずに、クラスの **Startup** イベントにイベントデリゲートを作成し **+=** ます。 次に例を示します。

     `this.<object name>.<event name> +=`

2. コード行の末尾で、TAB キーを2回押します。

     Visual Studio は自動的にコード行を補完し、イベントハンドラーを作成して、新しく作成されたイベントハンドラーに挿入ポイントを移動します。

## <a name="see-also"></a>関連項目
- [Office ソリューションでコードを記述する](../vsto/writing-code-in-office-solutions.md)
- [チュートリアル: NamedRange コントロールのイベントに対するプログラミング](../vsto/walkthrough-programming-against-events-of-a-namedrange-control.md)
- [Office ソリューションのビルド](../vsto/building-office-solutions.md)
