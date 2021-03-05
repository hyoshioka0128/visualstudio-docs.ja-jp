---
description: 起動された実行可能ファイルのシンボルを見つけることができなかったことをユーザーに警告するように、Visual Studio デバッガー UI に通知します。
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
ms.openlocfilehash: 859c9c1d07a5f4660f2d13dcffac4f19659a2bc2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102149822"
---
# <a name="idebugnosymbolsevent2"></a>IDebugNoSymbolsEvent2
[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]起動された実行可能ファイルのシンボルが見つからなかったことをユーザーに警告するように、デバッガーの UI に通知します。

## <a name="syntax"></a>構文

```
IDebugNoSymbolsEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジンによって実装され、デバッガー UI によって使用さ [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] れます。

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
