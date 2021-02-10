---
title: IDebugWindowsComputerPort2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugWindowsComputerPort2 interface
ms.assetid: 25f327b8-0303-4268-88d1-74df630436aa
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: c90e63e8ea7b00ff7d342ef6b1a0e624779e13d4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99965604"
---
# <a name="idebugwindowscomputerport2"></a>IDebugWindowsComputerPort2
対象のコンピュータに関する情報のクエリを実行できるようにします。

## <a name="syntax"></a>構文

```
IDebugWindowsComputerPort2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、セッションデバッグマネージャーのポートオブジェクトによって実装されます。

## <a name="methods"></a>メソッド
 次の表に、のメソッドを示し `IDebugWindowsComputerPort2` ます。

|Method|説明|
|------------|-----------------|
|[GetComputerInfo](../../../extensibility/debugger/reference/idebugwindowscomputerport2-getcomputerinfo.md)|デバッガーが実行されているコンピューターに関する情報を取得します。|

## <a name="requirements"></a>要件
 ヘッダー: Msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll
