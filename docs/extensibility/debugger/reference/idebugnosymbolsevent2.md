---
title: IDebugNoSymbolsEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugNoSymbolsEvent2 interface
ms.assetid: f6fb6388-47f6-4385-9ad5-95d62f9a7592
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0922d6e6e7d7e4ccc162652427e3f8c584580dd4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99929668"
---
# <a name="idebugnosymbolsevent2"></a>IDebugNoSymbolsEvent2
[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]起動された実行可能ファイルのシンボルが見つからなかったことをユーザーに警告するように、デバッガーの UI に通知します。

## <a name="syntax"></a>構文

```
IDebugNoSymbolsEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジンによって実装され、デバッガー UI によって使用さ [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] れます。

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
