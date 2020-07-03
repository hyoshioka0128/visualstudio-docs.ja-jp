---
title: エラー - IA64 プロセスの混合モードのデバッグはサポートされていません | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.interop_unsupported_ia64
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 850698edc53e810bbb4dcd2bfd45e31eedcecb2a
ms.sourcegitcommit: 66f31cc4ce1236e638ab58d2f70d3646206386fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85460665"
---
# <a name="error-mixed-mode-debugging-for-ia64-processes-is-unsupported"></a>エラー :IA64 プロセスの混合モードのデバッグはサポートされていません。
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] デバッガーは、Itanium ベースのプロセスでのネイティブ コードとマネージド コードの混合のデバッグをサポートしません。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- デバッグのため、32 ビット バージョンのアプリケーションをビルドします。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)