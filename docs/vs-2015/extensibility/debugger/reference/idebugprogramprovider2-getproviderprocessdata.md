---
title: 'IDebugProgramProvider2:: GetProviderProcessData |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgramProvider2::GetProviderProcessData
helpviewer_keywords:
- IDebugProgramProvider2::GetProviderProcessData
ms.assetid: 90cf7b7f-53d2-487e-b793-94501a6e24dd
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a50faf4531a098dde544adcffe535ed26e9c5cd8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68148514"
---
# <a name="idebugprogramprovider2getproviderprocessdata"></a>IDebugProgramProvider2::GetProviderProcessData
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定されたプロセスから実行中のプログラムの一覧を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT GetProviderProcessData(  
   PROVIDER_FLAGS         Flags,  
   IDebugDefaultPort2*    pPort,  
   AD_PROCESS_ID          processId,  
   CONST_GUID_ARRAY       EngineFilter,  
   PROVIDER_PROCESS_DATA* pProcess  
);  
```  
  
```csharp  
int GetProviderProcessData(  
   enum_PROVIDER_FLAGS     Flags,  
   IDebugDefaultPort2      pPort,  
   AD_PROCESS_ID           ProcessId,  
   CONST_GUID_ARRAY        EngineFilter,  
   PROVIDER_PROCESS_DATA[] pProcess  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `Flags`  
 から [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md) 列挙型のフラグの組み合わせ。 この呼び出しでは、次のフラグが一般的に使用されます。  
  
|フラグ|説明|  
|----------|-----------------|  
|`PFLAG_REMOTE_PORT`|リモートコンピューターで呼び出し元が実行されています。|  
|`PFLAG_DEBUGGEE`|呼び出し元は現在デバッグ中です (各ノードに対してマーシャリングに関する追加情報が返されます)。|  
|`PFLAG_ATTACHED_TO_DEBUGGEE`|呼び出し元はにアタッチされましたが、デバッガーによって起動されませんでした。|  
|`PFLAG_GET_PROGRAM_NODES`|呼び出し元が、返されるプログラムノードの一覧を要求しています。|  
  
 `pPort`  
 から呼び出しプロセスが実行されているポート。  
  
 `processId`  
 から対象のプログラムを含むプロセスの ID を保持する [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md) 構造体。  
  
 `EngineFilter`  
 からこのプロセスをデバッグするために割り当てられたデバッグエンジンの Guid の配列 (これらは、指定されたエンジンがサポートしているものに基づいて実際に返されるプログラムをフィルター処理するために使用されます。エンジンが指定されていない場合は、すべてのプログラムが返されます)。  
  
 `pProcess`  
 入出力要求された情報を格納する [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md) 構造体。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 通常、このメソッドはプロセスによって呼び出され、そのプロセスで実行されているプログラムの一覧を取得します。 返される情報は、 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトの一覧です。  
  
## <a name="see-also"></a>参照  
 [IDebugProgramProvider2](../../../extensibility/debugger/reference/idebugprogramprovider2.md)   
 [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)   
 [AD_PROCESS_ID](../../../extensibility/debugger/reference/ad-process-id.md)   
 [CONST_GUID_ARRAY](../../../extensibility/debugger/reference/const-guid-array.md)   
 [PROVIDER_FLAGS](../../../extensibility/debugger/reference/provider-flags.md)   
 [PROVIDER_PROCESS_DATA](../../../extensibility/debugger/reference/provider-process-data.md)   
 [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
