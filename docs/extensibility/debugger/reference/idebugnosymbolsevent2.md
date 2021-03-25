---
description: 起動された実行可能ファイルのシンボルを見つけることができなかったことをユーザーに警告するように、Visual Studio デバッガー UI に通知します。
title: IDebugNoSymbolsEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugNoSymbolsEvent2 interface
ms.assetid: f6fb6388-47f6-4385-9ad5-95d62f9a7592
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7a060436575d51710fcef9c444ac843aa56195d0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058405"
---
# <a name="idebugnosymbolsevent2"></a>IDebugNoSymbolsEvent2
[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]起動された実行可能ファイルのシンボルが見つからなかったことをユーザーに警告するように、デバッガーの UI に通知します。

## <a name="syntax"></a>Syntax

```
IDebugNoSymbolsEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジンによって実装され、デバッガー UI によって使用さ [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] れます。

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
