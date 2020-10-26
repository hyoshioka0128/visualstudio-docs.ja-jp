---
title: 'IDebugField:: GetTypeInfo |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::GetTypeInfo
helpviewer_keywords:
- IDebugField::GetTypeInfo method
ms.assetid: bb5acfa3-04c3-4088-be84-9ff8926cd16f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: faa3464f0396999f36604aa88c429235d4849688
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80728779"
---
# <a name="idebugfieldgettypeinfo"></a>IDebugField::GetTypeInfo
このメソッドは、記号または型に関する型に依存しない情報を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetTypeInfo( 
   TYPE_INFO* pTypeInfo
);
```

```csharp
int GetTypeInfo(
   TYPE_INFO[] pTypeInfo
);
```

## <a name="parameters"></a>パラメーター
`pTypeInfo`\
入出力指定された [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 構造体の型情報を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 型に依存しない情報には、たとえば、AppDomain、モジュール、およびシンボルを含むクラスが含まれます。

## <a name="see-also"></a>関連項目
- [GetType](../../../extensibility/debugger/reference/idebugfield-gettype.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
