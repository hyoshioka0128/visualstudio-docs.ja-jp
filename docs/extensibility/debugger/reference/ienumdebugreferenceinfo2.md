---
title: を参照してください。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugReferenceInfo2
helpviewer_keywords:
- IEnumDebugReferenceInfo2
ms.assetid: 7ed01441-686f-4032-8268-a4c750f19f85
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6132235a7e4789c7d9efe5bae9d7fd531112dab4
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80715279"
---
# <a name="ienumdebugreferenceinfo2"></a>IEnumDebugReferenceInfo2
このインターフェイスは[、DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体を列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugReferenceInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、メモリ内のオブジェクトへの参照のサポートの一部として、このインターフェイスを実装します。 このインターフェイスは、参照がサポートされている場合にのみ実装する必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスを取得するために[列挙子](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IEnumDebugReferenceInfo2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-next.md)|列挙体シーケンス内の指定した数の[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体を取得します。|
|[スキップ](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-skip.md)|列挙体シーケンス内の指定した数の[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体をスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-getcount.md)|列挙子の[DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体の数を取得します。|

## <a name="remarks"></a>Remarks
 参照は基本的に型とアドレスですが、プロパティは名前、型、およびアドレスです。 参照は、参照されるオブジェクトがメモリ内に存在する限り保持されます。 詳細については[、IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
