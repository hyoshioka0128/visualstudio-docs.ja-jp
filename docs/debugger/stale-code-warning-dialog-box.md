---
title: '[古いコードの警告] ダイアログ ボックス | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.debug.ENC.stalecode
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- Stale Code Warning dialog box
- code, stale code warning
- warnings, Stale Code Warning dialog box
- Edit and Continue, stale code
ms.assetid: 594b894c-e652-4e13-a980-9909473d5712
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: dba38e5b5d9f7a2be710cad58d6f2297dd03a412
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72729541"
---
# <a name="stale-code-warning-dialog-box"></a>[古いコードの警告] ダイアログ ボックス

このダイアログ ボックスは、**エディット コンティニュ**ではすぐに適用されない、ネイティブ コードへの変更を行った場合に表示されます。 結果として、現在のスタック フレーム内の一部のネイティブ コードが最新でない (陳腐化している) 場合があります。 詳細については、「[エディット コンティニュ (Visual C++)](edit-and-continue-visual-cpp.md)」を参照してください。

**[次回からこのダイアログ ボックスを表示しない]**

このチェック ボックスをオンにすると、以後エディット コンティニュは、このダイアログ ボックスを表示せずにコード変更を適用します。 この警告がまた表示されるようにするには、 **[オプション]** ダイアログ ボックスで、 **[デバッグ]** フォルダーを開き、 **[エディット コンティニュ]** ページをクリックし、 **[古いコードの警告を表示する]** をオンにします。

## <a name="see-also"></a>関連項目

- [サポートされているコード変更 (C++)](supported-code-changes-cpp.md)
- [[エディット コンティニュ] ([オプション] ダイアログ ボックス - [デバッグ])](edit-and-continue.md)