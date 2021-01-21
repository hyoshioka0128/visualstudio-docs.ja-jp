---
title: x64 プロセスの混合モード デバッグは Microsoft.NET Framework 4 以降を使用している場合にのみサポートされます | Microsoft Docs
ms.date: 11/04/2016
ms.topic: error-reference
f1_keywords:
- vs.debug.error.interop_unsupported_x64
dev_langs:
- CSharp
- VB
- FSharp
- C++
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- dotnet
ms.openlocfilehash: e8cfc3ac5cb606637fe5c2818750168a239a46fa
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90852616"
---
# <a name="error-mixed-mode-debugging-for-x64-processes-is-supported-only-when-using-microsoft-net-framework-4-or-greater"></a>エラー :x64 プロセスの混合モード デバッグは、Microsoft .NET Framework 4 以上を使用している場合にのみサポートされます
ネイティブ コードとマネージド コードの混合を 64 プロセスでデバッグするには、.NET Framework バージョン 4 が必要です。 .NET Framework のバージョン 4 より前のバージョンを使用した 64 ビット プロセスの混合モード デバッグはサポートされません。

### <a name="to-correct-this-error"></a>このエラーを解決するには

- 次のいずれかの操作を実行します。

  - .NET Framework をバージョン 4 にアップグレードします。

  - デバッグのため、32 ビット バージョンのアプリケーションをビルドします。

## <a name="see-also"></a>関連項目
- [Remote Debugging](../debugger/remote-debugging.md)