---
title: プログラムノード2::アンマーシャルデバッグジーインターフェイス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
helpviewer_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
ms.assetid: 2e4653c5-10f1-493c-9973-f31d266c5d48
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3c0f6e66b6585eafde656cd7be88d0c76bbb3f37
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720711"
---
# <a name="idebugproviderprogramnode2unmarshaldebuggeeinterface"></a>IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
プロセス境界を越えて指定されたインターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT UnmarshalDebuggeeInterface(
   REFIID riid,
   void** ppvObject
);
```

```csharp
int UnmarshalDebuggeeInterface(
   ref Guid   riid,
   out IntPtr ppvObject
);
```

## <a name="parameters"></a>パラメーター
`riid`\
[in]取得するインターフェイスの GUID。

`ppvObject`\
[アウト]目的のインターフェイスを実装するオブジェクトを返します。 [C++] これは、目的のインターフェイス型に直接キャストできます。 [C#] メソッド<xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A>を使用して、目的のインターフェイスを取得します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、[!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]デバッグ エンジンがプロセス空間で実行され、デバッグ中のプログラムが独自のプロセス領域で実行されている場合に使用されます。

## <a name="see-also"></a>関連項目
- [IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)
