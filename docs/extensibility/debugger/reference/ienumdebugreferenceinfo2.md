---
title: IEnumDebugReferenceInfo2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugReferenceInfo2
helpviewer_keywords:
- IEnumDebugReferenceInfo2
ms.assetid: 7ed01441-686f-4032-8268-a4c750f19f85
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 14b5bdc8a8be5734da765f0396fb96830042969f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99842226"
---
# <a name="ienumdebugreferenceinfo2"></a>IEnumDebugReferenceInfo2
このインターフェイスは [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体を列挙します。

## <a name="syntax"></a>構文

```
IEnumDebugReferenceInfo2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、メモリ内のオブジェクトへの参照のサポートの一部として、このインターフェイスを実装します。 このインターフェイスは、参照がサポートされている場合にのみ実装する必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスを取得するには、Visual Studio が [Enumchildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md) を呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IEnumDebugReferenceInfo2` ます。

|Method|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-next.md)|列挙シーケンス内の指定された数の [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体を取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-skip.md)|列挙シーケンス内の指定された数の [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体をスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2-getcount.md)|列挙子内の [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md) 構造体の数を取得します。|

## <a name="remarks"></a>解説
 参照は基本的には型とアドレスであり、プロパティは名前、型、およびアドレスです。 参照は、参照されるオブジェクトがメモリ内に存在する限り保持されます。 詳細については、「 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) 」を参照してください。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)
- [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)
