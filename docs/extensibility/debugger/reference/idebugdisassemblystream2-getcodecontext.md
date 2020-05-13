---
title: IDebugdisアセンブリストリーム2::取得コードコンテキスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::GetCodeContext
helpviewer_keywords:
- IDebugDisassemblyStream2::GetCodeContext
ms.assetid: a6d0ae82-7617-4915-9713-369abe3e2e53
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a6b3864528ee90c22a1e7122eeaf1969f613cc8e
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732287"
---
# <a name="idebugdisassemblystream2getcodecontext"></a>IDebugDisassemblyStream2::GetCodeContext
指定したコードの場所識別子に対応するコード コンテキスト オブジェクトを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCodeContext( 
   UINT64               uCodeLocationId,
   IDebugCodeContext2** ppCodeContext
);
```

```csharp
int GetCodeContext( 
   ulong                  uCodeLocationId,
   out IDebugCodeContext2 ppCodeContext
);
```

## <a name="parameters"></a>パラメーター
`uCodeLocationId`\
[in]コードの場所の識別子を指定します。 コードの場所識別子の説明については[、GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)メソッドの解説セクションを参照してください。

`ppCodeContext`\
[アウト]関連付けられたコード コンテキストを表す[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 コードの場所の識別子は[、GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)メソッドの呼び出しから返され[、DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)構造体に表示できます。

 コード コンテキストをコードの場所識別子に変換するには、[メソッド](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)を呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)
- [GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)
- [DisassemblyData](../../../extensibility/debugger/reference/disassemblydata.md)
