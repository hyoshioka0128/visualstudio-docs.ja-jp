---
title: 警告 :スクリプト デバッグが無効 | Microsoft Docs
description: "\"スクリプト デバッグが無効\" は、Internet Explorer でスクリプトのデバッグを有効にすることなく、スクリプトをデバッグした場合に発生します。 これを有効にする手順を確認します。"
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.scriptdisabled
dev_langs:
- CSharp
- VB
- FSharp
- C++
ms.assetid: 323d2b1d-52a4-42f7-b4ad-96b4b0c23b8d
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 7cc2e03a4efcf9a88675fd3c80f374ff78ba35bb
ms.sourcegitcommit: 957da60a881469d9001df1f4ba3ef01388109c86
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/13/2021
ms.locfileid: "98149561"
---
# <a name="warning-script-debugging-disabled"></a>警告 :スクリプト デバッグが無効
Internet Explorer では、スクリプトのデバッグは現在無効になっています。

 この警告は、Internet Explorer でスクリプトのデバッグを有効にしないままスクリプトをデバッグした場合に発生します。 セキュリティ上の理由から、Internet Explorer ではスクリプトのデバッグは既定で無効になっています。

### <a name="to-enable-script-debugging-in-internet-explorer"></a>Internet Explorer でスクリプトのデバッグを有効にするには

1. Internet Explorer で、 **[ツール]** メニューの **[インターネット オプション]** を選択します。

2. **[インターネット オプション]** ダイアログ ボックスで、 **[詳細設定]** タブをクリックします。

3. **[詳細設定]** タブの **[設定]** で **[参照]** カテゴリを表示します。

4. **[スクリプトのデバッグを使用しない (Internet Explorer)]** チェック ボックスをオフにします。

5. **[OK]** をクリックします。

6. Internet Explorer を終了して再起動します。

     新しい設定が反映されます。

## <a name="see-also"></a>関連項目
- [方法: ](attach-to-running-processes-with-the-visual-studio-debugger.md)スクリプトにアタッチする