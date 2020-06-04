---
title: エラー :IA64 プロセスの混合モードのデバッグはサポートされていません | Microsoft Docs
ms.date: 11/04/2016
ms.topic: troubleshooting
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
ms.openlocfilehash: 0bddbb1572bd0258eae2052eb34dfa3d0d67a134
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72737627"
---
# <a name="error-mixed-mode-debugging-for-ia64-processes-is-unsupported"></a>エラー :IA64 プロセスの混合モードのデバッグはサポートされていません。
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] デバッガーは、Itanium ベースのプロセスでのネイティブ コードとマネージド コードの混合のデバッグをサポートしません。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- デバッグのため、32 ビット バージョンのアプリケーションをビルドします。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)