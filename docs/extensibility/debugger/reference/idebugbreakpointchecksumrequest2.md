---
description: ブレークポイント要求のドキュメントチェックサムを表します。
title: IDebugBreakpointChecksumRequest2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugBreakpointChecksumRequest2 interface
ms.assetid: 9cfdbca5-052c-48e9-8411-e2e9e4065d00
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6bb0bdd70d2d4d1d56e341bc8f21ef1127433219
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102173711"
---
# <a name="idebugbreakpointchecksumrequest2"></a>IDebugBreakpointChecksumRequest2
ブレークポイント要求のドキュメントチェックサムを表します。

## <a name="syntax"></a>構文

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

## <a name="requirements"></a>必要条件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
