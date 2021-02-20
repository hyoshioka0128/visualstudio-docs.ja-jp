---
title: IA64 プロセスの混合モードのデバッグはサポートされていません | Microsoft Docs
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 22fa1b7f332d6a9f6481c513a3c2024a3551c7a5
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99871586"
---
# <a name="error-mixed-mode-debugging-for-ia64-processes-is-unsupported"></a>エラー :IA64 プロセスの混合モードのデバッグはサポートされていません。
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] デバッガーは、Itanium ベースのプロセスでのネイティブ コードとマネージド コードの混合のデバッグをサポートしません。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- デバッグのため、32 ビット バージョンのアプリケーションをビルドします。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)