---
description: ブレークポイント要求のドキュメントチェックサムを表します。
title: IDebugBreakpointChecksumRequest2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBreakpointChecksumRequest2 interface
ms.assetid: 9cfdbca5-052c-48e9-8411-e2e9e4065d00
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 78361429e371bf19ee1fea27c090af80c2b79b73
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105078085"
---
# <a name="idebugbreakpointchecksumrequest2"></a>IDebugBreakpointChecksumRequest2
ブレークポイント要求のドキュメントチェックサムを表します。

## <a name="syntax"></a>Syntax

```
IDebugBreakpointChecksumRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグパッケージによって実装さ [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] れ、デバッグエンジンによって使用されます。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugBreakpointChecksumRequest2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetChecksum](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2-getchecksum.md)|使用するチェックサムアルゴリズムの一意の識別子を指定して、ブレークポイント要求のドキュメントチェックサムを取得します。|
|[IsChecksumEnabled](../../../extensibility/debugger/reference/idebugbreakpointchecksumrequest2-ischecksumenabled.md)|このドキュメントに対してチェックサムを有効にするかどうかを決定します。|

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
