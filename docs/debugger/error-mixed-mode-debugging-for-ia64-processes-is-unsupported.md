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
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5bc0fe09078493814d1ff12108ccdada36e8da1f
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90852629"
---
# <a name="error-mixed-mode-debugging-for-ia64-processes-is-unsupported"></a>エラー :IA64 プロセスの混合モードのデバッグはサポートされていません。
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] デバッガーは、Itanium ベースのプロセスでのネイティブ コードとマネージド コードの混合のデバッグをサポートしません。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- デバッグのため、32 ビット バージョンのアプリケーションをビルドします。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)