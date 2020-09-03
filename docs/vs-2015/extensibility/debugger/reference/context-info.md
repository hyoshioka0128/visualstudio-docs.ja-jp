---
title: CONTEXT_INFO |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- CONTEXT_INFO
helpviewer_keywords:
- CONTEXT_INFO structure
ms.assetid: 6b513f4e-e7b0-4969-adf0-2205ccc1e09b
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f4e8c1b438cd2fa2721e81f055695e5836c26d12
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68179944"
---
# <a name="context_info"></a>CONTEXT_INFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

この構造体は、メモリコンテキストまたはコードコンテキストを記述します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _tagCONTEXT_INFO {   
   CONTEXT_INFO_FIELDS dwFields;  
   BSTR                bstrModuleUrl;  
   BSTR                bstrFunction;  
   TEXT_POSITION       posFunctionOffset;  
   BSTR                bstrAddress;  
   BSTR                bstrAddressOffset;  
   BSTR                bstrAddressAbsolute;  
} CONTEXT_INFO;  
```  
  
```csharp  
public struct CONTEXT_INFO {  
   public uint          dwFields;  
   public string        bstrModuleUrl;  
   public string        bstrFunction;  
   public TEXT_POSITION posFunctionOffset;  
   public string        bstrAddress;  
   public string        bstrAddressOffset;  
   public string        bstrAddressAbsolute;  
};  
```  
  
## <a name="members"></a>メンバー  
 dwFields  
 入力するフィールドを指定する、 [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md) 列挙型のフラグの組み合わせ<strong>。</strong>  
  
 bstrModuleUrl  
 コンテキストが配置されているモジュールの名前。  
  
 bstrFunction  
 コンテキストが配置されている関数の名前。  
  
 posFunctionOffset  
 コードコンテキストに関連付けられている関数の行と列のオフセットを識別する [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md) 構造体。  
  
 bstrAddress  
 指定したコンテキストが配置されているコード内のアドレス。  
  
 bstrAddressOffset  
 指定したコンテキストが配置されているコード内のアドレスのオフセット。  
  
 bstrAddressAbsolute  
 指定したコンテキストが配置されているメモリ内の絶対アドレス。  
  
## <a name="remarks"></a>注釈  
 この構造体は、 [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md) メソッドの呼び出しから返されます。  
  
 この構造体の一般的な用途は、 **メモリ** デバッグウィンドウをサポートすることです。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [GetInfo](../../../extensibility/debugger/reference/idebugmemorycontext2-getinfo.md)   
 [CONTEXT_INFO_FIELDS](../../../extensibility/debugger/reference/context-info-fields.md)   
 [TEXT_POSITION](../../../extensibility/debugger/reference/text-position.md)
