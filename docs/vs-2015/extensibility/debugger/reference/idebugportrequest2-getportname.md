---
title: 'IDebugPortRequest2:: GetPortName |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPortRequest2::GetPortName
helpviewer_keywords:
- IDebugPortRequest2::GetPortName
ms.assetid: 53e2a3a4-bb34-4a02-a983-6bd84ea70587
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: afed0bb700f41f7c39551f1a9bc7779f36b0ae57
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188367"
---
# <a name="idebugportrequest2getportname"></a>IDebugPortRequest2::GetPortName
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ポートの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetPortName(   
   BSTR* pbstrPortName  
);  
```  
  
```csharp  
int GetPortName(   
   out string pbstrPortName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pbstrPortName`  
 入出力ポートの名前を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)インターフェイスは、通常、ポートへの接続を取得するために、デバッグパッケージ (クライアント) からポートサプライヤー (サーバー) に渡されます。 デバッグパッケージとポートサプライヤーは、どちらもポートの選択肢を認識しています。 単純な文字列でポートを記述できる場合、メソッドには `IDebugPortRequest2::GetPortName` 接続に必要な情報が含まれています。 それ以外の場合、クライアントは追加のインターフェイスを提供できます。これは、を使用してサーバーで取得でき `IDebugPortRequest2::QueryInterface` ます。  
  
## <a name="see-also"></a>参照  
 [IDebugPortRequest2](../../../extensibility/debugger/reference/idebugportrequest2.md)
