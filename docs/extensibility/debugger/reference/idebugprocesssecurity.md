---
title: セキュリティを強化する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessSecurity interface
ms.assetid: 8a52ddca-bd99-49c0-9778-469dce7abd44
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 36c81cda3a27cfe1ef0fecfefc9bbb790d4d5217
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723196"
---
# <a name="idebugprocesssecurity"></a>IDebugProcessSecurity
`IDebugProcessSecurity`は、プロセスへのアタッチが安全でいいということをユーザーに警告するために、ポートサプライヤーによって実装されます。

## <a name="syntax"></a>構文

```
IDebugProcessSecurity : IUnknown
```

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProcessSecurity`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[ユーザー名を取得します。](../../../extensibility/debugger/reference/idebugprocesssecurity-getusername.md)|ポートサプライヤーからユーザー名を取得します。|
|[QueryCanSafelyAttach](../../../extensibility/debugger/reference/idebugprocesssecurity-querycansafelyattach.md)|デバッグ プロセスへのアタッチが安全でいいという警告をユーザーに警告します。|

## <a name="remarks"></a>Remarks
 このインターフェイスを実装して警告を表示し、アタッチするプロセスが安全でないと見なされる場合にユーザーがキャンセルできるようにします。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [ポート](../../../extensibility/debugger/ports.md)
- [ポート サプライヤー](../../../extensibility/debugger/port-suppliers.md)
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
