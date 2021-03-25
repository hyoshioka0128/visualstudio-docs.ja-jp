---
description: プロセスの境界を越えて、指定されたインターフェイスを取得します。
title: 'IDebugProviderProgramNode2:: UnmarshalDebuggeeInterface |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
helpviewer_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
ms.assetid: 2e4653c5-10f1-493c-9973-f31d266c5d48
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 42b51d93f9c0cec3a2ee74b2dfc0f4621c608c07
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083688"
---
# <a name="idebugproviderprogramnode2unmarshaldebuggeeinterface"></a>IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
プロセスの境界を越えて、指定されたインターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT UnmarshalDebuggeeInterface(
   REFIID riid,
   void** ppvObject
);
```

```csharp
int UnmarshalDebuggeeInterface(
   ref Guid   riid,
   out IntPtr ppvObject
);
```

## <a name="parameters"></a>パラメーター
`riid`\
から取得するインターフェイスの GUID。

`ppvObject`\
入出力目的のインターフェイスを実装しているオブジェクトを返します。 [C++] これは、目的のインターフェイス型に直接キャストできます。 [C#] メソッドを使用し <xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> て、目的のインターフェイスを取得します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、デバッグエンジンがプロセス空間で実行されて [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)] おり、デバッグ中のプログラムが独自のプロセス空間で実行されている場合に使用されます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)
