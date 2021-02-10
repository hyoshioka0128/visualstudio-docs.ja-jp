---
title: IDebugProcessSecurity |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity interface
ms.assetid: 8a52ddca-bd99-49c0-9778-469dce7abd44
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7c6807ff64d8acf44551fa12fcb79199d3817373
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99933025"
---
# <a name="idebugprocesssecurity"></a>IDebugProcessSecurity
`IDebugProcessSecurity` は、プロセスへのアタッチが安全でないことをユーザーに警告するために、ポート供給業者によって実装されます。

## <a name="syntax"></a>構文

```
IDebugProcessSecurity : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugProcessSecurity` ます。

|Method|説明|
|------------|-----------------|
|[GetUserName](../../../extensibility/debugger/reference/idebugprocesssecurity-getusername.md)|ポートサプライヤーからユーザー名を取得します。|
|[QueryCanSafelyAttach](../../../extensibility/debugger/reference/idebugprocesssecurity-querycansafelyattach.md)|デバッグプロセスへのアタッチが安全でないことをユーザーに警告します。|

## <a name="remarks"></a>解説
 このインターフェイスを実装して警告を表示し、アタッチしているプロセスが安全でないと見なされた場合にユーザーがキャンセルできるようにします。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [ポート](../../../extensibility/debugger/ports.md)
- [ポート サプライヤー](../../../extensibility/debugger/port-suppliers.md)
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
