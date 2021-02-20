---
title: コード変更を停止する | Microsoft Docs
description: Visual Studio のデバッグ セッション中にエディット コンティニュ機能を使用しているときに、コード変更の適用を停止する方法について説明します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 4aebf3b4a5a7556b2e2a3f6fdff7554539812d8f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99896567"
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