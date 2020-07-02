---
title: '方法: アドインのユーザーインターフェイスエラーを表示する'
ms.date: 02/02/2017
ms.topic: how-to
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- add-ins [Office development in Visual Studio], user interface errors
- errors [Office development in Visual Studio], user interface errors
- user interfaces [Office development in Visual Studio], errors
- application-level add-ins [Office development in Visual Studio], user interface errors
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 49985589c021192454bf0dd58929c9ef5646aec9
ms.sourcegitcommit: b885f26e015d03eafe7c885040644a52bb071fae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/30/2020
ms.locfileid: "85545783"
---
# <a name="how-to-show-add-in-user-interface-errors"></a>方法: アドインのユーザーインターフェイスエラーを表示する
  既定では、VSTO アドインが Microsoft Office ユーザーインターフェイス (UI) を操作しようとして失敗した場合、エラーメッセージは表示されません。 しかし、UI に関連するエラー メッセージを表示するように Microsoft Office アプリケーションを構成できます。 これらのメッセージを使用すると、カスタムリボンが表示されない理由や、リボンが表示されるのにコントロールが表示されない理由を判断するのに役立ちます。

 [!INCLUDE[appliesto_ribbon](../vsto/includes/appliesto-ribbon-md.md)]

## <a name="to-show-vsto-add-in-user-interface-errors"></a>VSTO アドインのユーザー インターフェイス エラーを表示するには

1. アプリケーションを起動します。

2. **[ファイル]** タブをクリックします。

3. **[オプション]** をクリックします。

4. [カテゴリ] ウィンドウで **[詳細]** をクリックします。

5. 詳細ウィンドウで、 **[VSTO アドイン ユーザー インターフェイスのエラーを表示する]** を選び、 **[OK]** をクリックします。

    > [!NOTE]
    > Outlook の場合、詳細ウィンドウの **[開発]** セクションに **[VSTO アドイン ユーザー インターフェイスのエラーを表示する]** チェック ボックスがあります。 その他のアプリケーションの場合、このチェック ボックスは、詳細ウィンドウの **[全般]** セクションにあります。

## <a name="see-also"></a>関連項目
- [Office UI のカスタマイズ](../vsto/office-ui-customization.md)
- [Outlook フォーム領域の作成](../vsto/creating-outlook-form-regions.md)
- [リボンの概要](../vsto/ribbon-overview.md)
- [操作ウィンドウの概要](../vsto/actions-pane-overview.md)
