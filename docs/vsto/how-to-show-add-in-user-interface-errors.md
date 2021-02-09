---
title: '方法: アドインのユーザーインターフェイスエラーを表示する'
description: Visual Studio を使用して、Microsoft Office アプリケーションでのアドインユーザーインターフェイスエラーをプログラムによって表示する方法について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 29e07e49d901b44b534d9d274e5535be663e97ef
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99927679"
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
