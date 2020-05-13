---
title: Iデバッグフィールド::ゲットタイプ情報 |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728779"
---
# <a name="idebugfieldgettypeinfo"></a>IDebugField::GetTypeInfo
このメソッドは、シンボルまたは型に関する型に依存しない情報を取得します。

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
[アウト]指定された[TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)構造体の型情報を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 型に依存しない情報には、たとえば、AppDomain、モジュール、シンボルを含むクラスが含まれます。

## <a name="see-also"></a>関連項目
- [Gettype](../../../extensibility/debugger/reference/idebugfield-gettype.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
- [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)
