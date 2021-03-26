---
description: カスタム属性を列挙します。
title: IEnumDebugCustomAttributes |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumCustomAttributes
helpviewer_keywords:
- IEnumDebugCustomAttributes interface
ms.assetid: 11aa768d-1852-44d6-9de3-17f9bafaded2
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8decd8d244ad4b55d2bba7381e247535faad9b22
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081075"
---
# <a name="ienumdebugcustomattributes"></a>IEnumDebugCustomAttributes
カスタム属性を列挙します。

## <a name="syntax"></a>Syntax

```
IEnumCustomAttributes : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボルプロバイダーは、( [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md) インターフェイスを通じて) カスタム属性をサポートするために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
- [Enumcustomattributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md) は、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IEnumDebugCustomAttributes` ます。

|メソッド|説明|
|------------|-----------------|
|[次へ](../../../extensibility/debugger/reference/ienumdebugcustomattributes-next.md)|列挙シーケンス内の指定された数のカスタム属性を取得します。|
|[Skip](../../../extensibility/debugger/reference/ienumdebugcustomattributes-skip.md)|列挙シーケンス内の指定された数のカスタム属性をスキップします。|
|[リセット](../../../extensibility/debugger/reference/ienumdebugcustomattributes-reset.md)|列挙シーケンスを先頭にリセットします。|
|[複製](../../../extensibility/debugger/reference/ienumdebugcustomattributes-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|
|[GetCount](../../../extensibility/debugger/reference/ienumdebugcustomattributes-getcount.md)|列挙子内のカスタム属性の数を取得します。|

## <a name="requirements"></a>要件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [EnumCustomAttributes](../../../extensibility/debugger/reference/idebugcustomattributequery2-enumcustomattributes.md)
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
