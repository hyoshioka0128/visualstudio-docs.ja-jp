---
title: FIELD_KIND |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- FIELD_KIND
helpviewer_keywords:
- FIELD_KIND enumeration
ms.assetid: fd522b9c-52e2-42fa-939d-343347d5c3b1
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ab972df2cf1b382498d2e57a5ae2e978c7230a34
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65692876"
---
# <a name="field_kind"></a>FIELD_KIND
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)オブジェクトに含まれるフィールドの種類を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_FIELD_KIND {   
   FIELD_KIND_NONE       = 0x00000000,  
  
   // Type of field  
   FIELD_KIND_TYPE       = 0x00000001,  
   FIELD_KIND_SYMBOL     = 0x00000002,  
  
   // Storage type of the field  
   FIELD_TYPE_PRIMITIVE  = 0x00000010,  
   FIELD_TYPE_STRUCT     = 0x00000020,  
   FIELD_TYPE_CLASS      = 0x00000040,  
   FIELD_TYPE_INTERFACE  = 0x00000080,  
   FIELD_TYPE_UNION      = 0x00000100,  
   FIELD_TYPE_ARRAY      = 0x00000200,  
   FIELD_TYPE_METHOD     = 0x00000400,  
   FIELD_TYPE_BLOCK      = 0x00000800,  
   FIELD_TYPE_POINTER    = 0x00001000,  
   FIELD_TYPE_ENUM       = 0x00002000,  
   FIELD_TYPE_LABEL      = 0x00004000,  
   FIELD_TYPE_TYPEDEF    = 0x00008000,  
   FIELD_TYPE_BITFIELD   = 0x00010000,  
   FIELD_TYPE_NAMESPACE  = 0x00020000,  
   FIELD_TYPE_MODULE     = 0x00040000,  
   FIELD_TYPE_DYNAMIC    = 0x00080000,  
   FIELD_TYPE_PROP       = 0x00100000,  
   FIELD_TYPE_INNERCLASS = 0x00200000,  
   FIELD_TYPE_REFERENCE  = 0x00400000,  
   FIELD_TYPE_EXTENDED   = 0x00800000,  
  
   // Specific information about symbols  
   FIELD_SYM_MEMBER      = 0x01000000,  
   FIELD_SYM_LOCAL       = 0x02000000,  
   FIELD_SYM_PARAM       = 0x04000000,  
   FIELD_SYM_THIS        = 0x08000000,  
   FIELD_SYM_GLOBAL      = 0x10000000,  
   FIELD_SYM_PROP_GETTER = 0x20000000,  
   FIELD_SYM_PROP_SETTER = 0x40000000,  
   FIELD_SYM_EXTENDED    = 0x80000000,  
  
   FIELD_KIND_MASK       = 0x0000000f,  
   FIELD_TYPE_MASK       = 0x00fffff0,  
   FIELD_SYM_MASK        = 0xff000000,  
  
   FIELD_KIND_ALL        = 0xffffffff  
};  
typedef DWORD FIELD_KIND;  
```  
  
```csharp  
public enum enum_FIELD_KIND {  
   FIELD_KIND_NONE       = 0x00000000,  
  
   // Type of field  
   FIELD_KIND_TYPE       = 0x00000001,  
   FIELD_KIND_SYMBOL     = 0x00000002,  
  
   // Storage type of the field  
   FIELD_TYPE_PRIMITIVE  = 0x00000010,  
   FIELD_TYPE_STRUCT     = 0x00000020,  
   FIELD_TYPE_CLASS      = 0x00000040,  
   FIELD_TYPE_INTERFACE  = 0x00000080,  
   FIELD_TYPE_UNION      = 0x00000100,  
   FIELD_TYPE_ARRAY      = 0x00000200,  
   FIELD_TYPE_METHOD     = 0x00000400,  
   FIELD_TYPE_BLOCK      = 0x00000800,  
   FIELD_TYPE_POINTER    = 0x00001000,  
   FIELD_TYPE_ENUM       = 0x00002000,  
   FIELD_TYPE_LABEL      = 0x00004000,  
   FIELD_TYPE_TYPEDEF    = 0x00008000,  
   FIELD_TYPE_BITFIELD   = 0x00010000,  
   FIELD_TYPE_NAMESPACE  = 0x00020000,  
   FIELD_TYPE_MODULE     = 0x00040000,  
   FIELD_TYPE_DYNAMIC    = 0x00080000,  
   FIELD_TYPE_PROP       = 0x00100000,  
   FIELD_TYPE_INNERCLASS = 0x00200000,  
   FIELD_TYPE_REFERENCE  = 0x00400000,  
   FIELD_TYPE_EXTENDED   = 0x00800000,  
  
   // Specific information about symbols  
   FIELD_SYM_MEMBER      = 0x01000000,  
   FIELD_SYM_LOCAL       = 0x02000000,  
   FIELD_SYM_PARAM       = 0x04000000,  
   FIELD_SYM_THIS        = 0x08000000,  
   FIELD_SYM_GLOBAL      = 0x10000000,  
   FIELD_SYM_PROP_GETTER = 0x20000000,  
   FIELD_SYM_PROP_SETTER = 0x40000000,  
   FIELD_SYM_EXTENDED    = 0x80000000,  
  
   FIELD_KIND_MASK       = 0x0000000f,  
   FIELD_TYPE_MASK       = 0x00fffff0,  
   FIELD_SYM_MASK        = 0xff000000,  
  
   FIELD_KIND_ALL        = 0xffffffff  
};  
```  
  
## <a name="members"></a>メンバー  
 FIELD_KIND_TYPE  
 フィールドが型のみであることを示します。  
  
 FIELD_KIND_SYMBOL  
 フィールドが、型、名前、およびその他の情報を含むシンボルであることを示します。  
  
 FIELD_TYPE_PRIMITIVE  
 フィールドがプリミティブデータ型であることを示します。  
  
 FIELD_TYPE_STRUCT  
 フィールドが構造体であることを示します。  
  
 FIELD_TYPE_CLASS  
 フィールドがクラスであることを示します。  
  
 FIELD_TYPE_INTERFACE  
 フィールドがインターフェイスであることを示します。  
  
 FIELD_TYPE_UNION  
 フィールドが共用体であることを示します。  
  
 FIELD_TYPE_ARRAY  
 フィールドが配列であることを示します。  
  
 FIELD_TYPE_METHOD  
 フィールドがメソッドであることを示します。  
  
 FIELD_TYPE_BLOCK  
 フィールドがブロックであることを示します。  
  
 FIELD_TYPE_POINTER  
 フィールドがポインターであることを示します。  
  
 FIELD_TYPE_ENUM  
 フィールドが列挙データ型であることを示します。  
  
 FIELD_TYPE_LABEL  
 フィールドがラベルであることを示します。  
  
 FIELD_TYPE_TYPEDEF  
 フィールドが typedef であることを示します。  
  
 FIELD_TYPE_BITFIELD  
 フィールドがビットフィールドであることを示します。  
  
 FIELD_TYPE_NAMESPACE  
 フィールドが名前空間であることを示します。  
  
 FIELD_TYPE_MODULE  
 フィールドがモジュールであることを示します。  
  
 FIELD_TYPE_DYNAMIC  
 フィールドが動的であることを示します。  
  
 FIELD_TYPE_PROP  
 フィールドがプロパティであることを示します。  
  
 FIELD_TYPE_INNERCLASS  
 フィールドが内部クラスであることを示します。  
  
 FIELD_TYPE_REFERENCE  
 フィールドが参照であることを示します。  
  
 FIELD_TYPE_EXTENDED  
 将来使用するために予約されています。  
  
 FIELD_SYM_MEMBER  
 フィールドがメンバーであることを示します。  
  
 FIELD_SYM_LOCAL  
 フィールドがローカルであることを示します。  
  
 FIELD_SYM_PARAMETER  
 フィールドがパラメーターであることを示します。  
  
 FIELD_SYM_THIS  
 フィールドが "this" ポインターであることを示します。  
  
 FIELD_SYM_GLOBAL  
 フィールドがグローバルであることを示します。  
  
 FIELD_SYM_PROP_GETTER  
 フィールドがプロパティを取得することを示します。  
  
 FIELD_SYM_PROP_SETTER  
 フィールドがプロパティを設定することを示します。  
  
 FIELD_SYM_EXTENDED  
 将来使用するために予約されています。  
  
 FIELD_KIND_MASK  
 フィールドの種類のマスクを示します。  
  
 FIELD_TYPE_MASK  
 フィールドの種類のマスクを示します。  
  
 FIELD_SYM_MASK  
 シンボル情報のマスクを示します。  
  
## <a name="remarks"></a>解説  
 [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md)メソッドの呼び出しから返されます。  
  
 フィールドの種類に応じて、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)インターフェイスで[QueryInterface](https://msdn.microsoft.com/library/62fce95e-aafa-4187-b50b-e6611b74c3b3)を呼び出して、より具体的な形式のインターフェイスを作成できます。 たとえば、 [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md) がを返す場合は、 `FIELD_TYPE_METHOD` `QueryInterface` I でを呼び出して `DebugField` [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) インターフェイスを取得できます。  
  
## <a name="requirements"></a>必要条件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [FIELD_MODIFIERS](../../../extensibility/debugger/reference/field-modifiers.md)   
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
