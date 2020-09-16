---
title: 方法 - コード変更を停止する | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Stop Applying Code Changes command
- code changes, stopping application of
- Edit and Continue, stopping code changes
ms.assetid: 9e72a50c-bb0a-4eaa-9ac1-d00930b68d38
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: a62fe2b99e197cfafbf48a1a5a881fce73d89788
ms.sourcegitcommit: ed4372bb6f4ae64f1fd712b2b253bf91d9ff96bf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2020
ms.locfileid: "89599852"
---
# <a name="how-to-stop-code-changes"></a>方法: コード変更を停止する
エディット コンティニュがコード変更を適用するプロセスを実行している間、その操作は中断できます。

> [!CAUTION]
> マネージド コードのコード変更を中断すると、予期しない結果が生じることがあります。 通常、マネージド コードの変更はすばやく適用されるため、マネージド コードのコード変更の中断が必要となることはほとんどありません。

### <a name="to-stop-applying-code-changes"></a>コードの変更内容の適用を停止するには

- **[デバッガー]** メニューの **[コード変更の適用を中止]** をクリックします。

  このメニュー項目は、コード変更の適用中にのみ表示されます。

  このオプションを選択すると、コードの変更内容は一切コミットされません。

## <a name="see-also"></a>関連項目
- [エディット コンティニュ](../debugger/edit-and-continue.md)
- [[エディット コンティニュ] ([オプション] ダイアログ ボックス - [デバッグ])](./edit-and-continue.md)