---
title: IDebugCoreServer3::CreateInstanceInServer |Microsoft Docs
ms.custom: ''
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.reviewer: ''
ms.suite: ''
ms.technology:
- vs-ide-sdk
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- IDebugCoreServer3::CreateInstanceInServer
helpviewer_keywords:
- IDebugCoreServer3::CreateInstanceInServer
ms.assetid: 76f36bae-f6ab-413c-a8a9-8808bfeba05b
caps.latest.revision: 10
ms.author: gregvanl
manager: ghogen
ms.openlocfilehash: efdd8078439e288e600ef3a318e4038af51c7d1b
ms.sourcegitcommit: af428c7ccd007e668ec0dd8697c88fc5d8bca1e2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/16/2018
ms.locfileid: "51749706"
---
# <a name="idebugcoreserver3createinstanceinserver"></a>IDebugCoreServer3::CreateInstanceInServer
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

サーバー上のデバッグ エンジンのインスタンスを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT CreateInstanceInServer(  
   LPCWSTR  szDll,  
   WORD     wLangId,  
   REFCLSID clsidObject,  
   REFIID   riid,  
   void**   ppvObject  
);  
```  
  
```csharp  
int CreateInstanceInServer(  
   string     szDll,   
   ushort     wLangID,   
   ref Guid   clsidObject,   
   ref Guid   riid,   
   out IntPtr ppvObject  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `szDll`  
 [in]指定された CLSID を実装する dll へのパス、`clsidObject`パラメーター。 この場合`NULL`、し、COM の`CoCreateInstance`関数が呼び出されます。  
  
 `wLangId`  
 [in]デバッグ エンジンのロケール。 場合 0 になります、 [SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)メソッドを呼び出すことはできません。  
  
 `clsidObject`  
 [in]作成するデバッグ エンジンの CLSID。  
  
 `riid`  
 [in]インターフェイス クラスのオブジェクトから取得するには、特定のインターフェイスの ID。  
  
 `ppvObject`  
 [out]`IUnknown`オブジェクトのインスタンスからのインターフェイス。 キャストまたは必要なインターフェイスには、このオブジェクトをマーシャ リングします。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、返します`S_OK`、それ以外のエラー コードを返します。  
  
## <a name="see-also"></a>関連項目  
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)   
 [SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)

