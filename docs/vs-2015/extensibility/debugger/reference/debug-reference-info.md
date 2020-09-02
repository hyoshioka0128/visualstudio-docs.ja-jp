---
title: DEBUG_REFERENCE_INFO |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- DEBUG_REFERENCE_INFO
helpviewer_keywords:
- DEBUG_REFERENCE_INFO structure
ms.assetid: 24b83d00-d756-42a1-8083-730f998761dc
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 675373ae1728bbca2cc7a89fdaa8014e6286d8b4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68159321"
---
# <a name="debug_reference_info"></a>DEBUG_REFERENCE_INFO
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

参照を記述します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct tagDEBUG_REFERENCE_INFO {   
   DEBUGREF_INFO_FLAGS dwFields;  
   BSTR                bstrName;  
   BSTR                bstrType;  
   BSTR                bstrValue;  
   DBG_ATTRIB_FLAGS    dwAttrib;  
   REFERENCE_TYPE.     dwRefType;  
   IDebugReference2*   m_pReference;  
} DEBUG_REFERENCE_INFO;  
```  
  
```csharp  
public struct DEBUG_REFERENCE_INFO {   
   public uint             dwFields;  
   public string           bstrName;  
   public string           bstrType;  
   public string           bstrValue;  
   public ulong            dwAttrib;  
   public uint.            dwRefType;  
   public IDebugReference2 m_pReference;  
};  
```  
  
## <a name="members"></a>メンバー  
 dwFields  
 入力するフィールドを指定する、 [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md) 列挙のフラグの組み合わせ。  
  
 bstrName  
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)オブジェクトのユーザー指定の名前。  
  
 bstrType  
 書式設定された文字列としての参照型。  
  
 bstrValue  
 書式設定された文字列としての参照値  
  
 dwAttrib  
 デバッグプロパティの属性のフラグを指定する、 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md) 列挙型のフラグの組み合わせ。  
  
 dwRefType  
 参照型が strong か weak かを指定する [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md) 列挙の値です。  
  
 m_pReference  
 参照情報を指定する [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md) オブジェクトです。  
  
## <a name="remarks"></a>注釈  
 この構造体は、入力される [Getreferenceinfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md) メソッドの呼び出しに渡されます。 この構造体は、 [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md) インターフェイスからのリストの一部としても返されます。このインターフェイスは、 [enumchildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md) メソッドの呼び出しから返されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)   
 [DEBUGREF_INFO_FLAGS](../../../extensibility/debugger/reference/debugref-info-flags.md)   
 [DBG_ATTRIB_FLAGS](../../../extensibility/debugger/reference/dbg-attrib-flags.md)   
 [REFERENCE_TYPE](../../../extensibility/debugger/reference/reference-type.md)   
 [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)   
 [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)   
 [IEnumDebugReferenceInfo2](../../../extensibility/debugger/reference/ienumdebugreferenceinfo2.md)
