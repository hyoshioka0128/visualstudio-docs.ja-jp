---
title: Iデバッグプログラム2::プロパティを取得する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::GetDebugProperty
helpviewer_keywords:
- IDebugProgram2::GetDebugProperty
ms.assetid: d194224e-f0e6-46ab-85d4-9e2639e28946
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 33bc10aadf25eb95414cc5fd334c572b2f270429
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722894"
---
# <a name="idebugprogram2getdebugproperty"></a>IDebugProgram2::GetDebugProperty
プログラムのプロパティを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDebugProperty( 
   IDebugProperty2** ppProperty
);
```

```csharp
int GetDebugProperty( 
   out IDebugProperty2 ppProperty
);
```

## <a name="parameters"></a>パラメーター
`ppProperty`\
[アウト]プログラムのプロパティを表す[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドによって返されるプロパティは、プログラムに固有です。 プログラムが複数のプロパティを返す必要がある場合、このメソッドによって返される[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)オブジェクトは追加のプロパティのコンテナーであり[、EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)メソッドを呼び出すと、すべてのプロパティのリストが返されます。

 プログラムは、インターフェイスを通じて記述できる追加のプロパティの数と型を`IDebugProperty2`公開できます。 IDE は、汎用プロパティ ブラウザーのユーザー インターフェイスを通じて、追加のプログラム プロパティを表示する場合があります。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [EnumChildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)
