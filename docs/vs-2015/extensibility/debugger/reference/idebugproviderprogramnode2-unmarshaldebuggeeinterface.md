---
title: 'IDebugProviderProgramNode2:: UnmarshalDebuggeeInterface |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
helpviewer_keywords:
- IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
ms.assetid: 2e4653c5-10f1-493c-9973-f31d266c5d48
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3007d13ec3eae46511e4775497d0aad5b6325b2b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68146259"
---
# <a name="idebugproviderprogramnode2unmarshaldebuggeeinterface"></a>IDebugProviderProgramNode2::UnmarshalDebuggeeInterface
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

プロセスの境界を越えて、指定されたインターフェイスを取得します。  
  
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
  
#### <a name="parameters"></a>パラメーター  
 `riid`  
 から取得するインターフェイスの GUID。  
  
 `ppvObject`  
 入出力目的のインターフェイスを実装しているオブジェクトを返します。 [C++] これは、目的のインターフェイス型に直接キャストできます。 [C#] メソッドを使用し <xref:System.Runtime.InteropServices.Marshal.GetObjectForIUnknown%2A> て、目的のインターフェイスを取得します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、デバッグエンジンがプロセス空間で実行されて [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] おり、デバッグ中のプログラムが独自のプロセス空間で実行されている場合に使用されます。  
  
## <a name="see-also"></a>参照  
 [IDebugProviderProgramNode2](../../../extensibility/debugger/reference/idebugproviderprogramnode2.md)
