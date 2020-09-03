---
title: FIELD_MODIFIERS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- FIELD_MODIFIERS
helpviewer_keywords:
- FIELD_MODIFIERS enumeration
ms.assetid: 1e44681c-1f03-41a9-9c04-b79f231b0822
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bd25a3cb5b2d074e989b47f33513e05538868759
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68203049"
---
# <a name="field_modifiers"></a>FIELD_MODIFIERS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

フィールド型の修飾子を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_FIELD_MODIFIERS {   
   FIELD_MOD_NONE             = 0x00000000,  
  
   // Modifier of the field  
   FIELD_MOD_ACCESS_NONE      = 0x00000001,  
   FIELD_MOD_ACCESS_PUBLIC    = 0x00000002,  
   FIELD_MOD_ACCESS_PROTECTED = 0x00000004,  
   FIELD_MOD_ACCESS_PRIVATE   = 0x00000008,  
  
   // Storage modifier of the field  
   FIELD_MOD_NOMODIFIERS      = 0x00000010,  
   FIELD_MOD_STATIC           = 0x00000020,  
   FIELD_MOD_CONSTANT         = 0x00000040,  
   FIELD_MOD_TRANSIENT        = 0x00000080,  
   FIELD_MOD_VOLATILE         = 0x00000100,  
   FIELD_MOD_ABSTRACT         = 0x00000200,  
   FIELD_MOD_NATIVE           = 0x00000400,  
   FIELD_MOD_SYNCHRONIZED     = 0x00000800,  
   FIELD_MOD_VIRTUAL          = 0x00001000,  
   FIELD_MOD_INTERFACE        = 0x00002000,  
   FIELD_MOD_FINAL            = 0x00004000,  
   FIELD_MOD_SENTINEL         = 0x00008000,  
   FIELD_MOD_INNERCLASS       = 0x00010000,  
   FIELD_TYPE_OPTIONAL        = 0x00020000,  
   FIELD_MOD_BYREF            = 0x00040000,  
   FIELD_MOD_HIDDEN           = 0x00080000,  
   FIELD_MOD_MARSHALASOBJECT  = 0x00100000,  
   FIELD_MOD_SPECIAL_NAME     = 0x00200000,  
   FIELD_MOD_HIDEBYSIG        = 0x00400000,  
  
   FIELD_MOD_WRITEONLY        = 0x80000000,  
   FIELD_MOD_ACCESS_MASK      = 0x000000ff,  
   FIELD_MOD_MASK             = 0xffffff00,  
   FIELD_MOD_ALL              = 0x7fffffff  
};  
typedef DWORD FIELD_MODIFIERS;  
```  
  
```csharp  
public enum enum_FIELD_MODIFIERS {  
   FIELD_MOD_NONE             = 0x00000000,  
  
   // Modifier of the field  
   FIELD_MOD_ACCESS_NONE      = 0x00000001,  
   FIELD_MOD_ACCESS_PUBLIC    = 0x00000002,  
   FIELD_MOD_ACCESS_PROTECTED = 0x00000004,  
   FIELD_MOD_ACCESS_PRIVATE   = 0x00000008,  
  
   // Storage modifier of the field  
   FIELD_MOD_NOMODIFIERS      = 0x00000010,  
   FIELD_MOD_STATIC           = 0x00000020,  
   FIELD_MOD_CONSTANT         = 0x00000040,  
   FIELD_MOD_TRANSIENT        = 0x00000080,  
   FIELD_MOD_VOLATILE         = 0x00000100,  
   FIELD_MOD_ABSTRACT         = 0x00000200,  
   FIELD_MOD_NATIVE           = 0x00000400,  
   FIELD_MOD_SYNCHRONIZED     = 0x00000800,  
   FIELD_MOD_VIRTUAL          = 0x00001000,  
   FIELD_MOD_INTERFACE        = 0x00002000,  
   FIELD_MOD_FINAL            = 0x00004000,  
   FIELD_MOD_SENTINEL         = 0x00008000,  
   FIELD_MOD_INNERCLASS       = 0x00010000,  
   FIELD_TYPE_OPTIONAL        = 0x00020000,  
   FIELD_MOD_BYREF            = 0x00040000,  
   FIELD_MOD_HIDDEN           = 0x00080000,  
   FIELD_MOD_MARSHALASOBJECT  = 0x00100000,  
   FIELD_MOD_SPECIAL_NAME     = 0x00200000,  
   FIELD_MOD_HIDEBYSIG        = 0x00400000,  
  
   FIELD_MOD_WRITEONLY        = 0x80000000,  
   FIELD_MOD_ACCESS_MASK      = 0x000000ff,  
   FIELD_MOD_MASK             = 0xffffff00,  
   FIELD_MOD_ALL              = 0x7fffffff  
};  
```  
  
## <a name="members"></a>メンバー  
 FIELD_MOD_ACCESS_TYPE  
 フィールドにアクセスできないことを示します。  
  
 FIELD_MOD_ACCESS_PUBLIC  
 フィールドにパブリックアクセスがあることを示します。  
  
 FIELD_MOD_ACCESS_PROTECTED  
 フィールドに保護されたアクセス権があることを示します。  
  
 FIELD_MOD_ACCESS_PRIVATE  
 フィールドにプライベートアクセスがあることを示します。  
  
 FIELD_MOD_NOMODIFIERS  
 フィールドに修飾子がないことを示します。  
  
 FIELD_MOD_STATIC  
 フィールドが静的であることを示します。  
  
 FIELD_MOD_CONSTANT  
 フィールドが定数であることを示します。  
  
 FIELD_MOD_TRANSIENT  
 フィールドが一時的なものであることを示します。  
  
 FIELD_MOD_VOLATILE  
 フィールドが volatile であることを示します。  
  
 FIELD_MOD_ABSTRACT  
 フィールドが抽象であることを示します。  
  
 FIELD_MOD_NATIVE  
 フィールドがネイティブであることを示します。  
  
 FIELD_MOD_SYNCHRONIZED  
 フィールドが同期されていることを示します。  
  
 FIELD_MOD_VIRTUAL  
 フィールドが仮想であることを示します。  
  
 FIELD_MOD_INTERFACE  
 フィールドがインターフェイスであることを示します。  
  
 FIELD_MOD_FINAL  
 フィールドが final であることを示します。  
  
 FIELD_MOD_SENTINEL  
 フィールドが sentinel であることを示します。  
  
 FIELD_MOD_INNERCLASS  
 フィールドが内部クラスであることを示します。  
  
 FIELD_TYPE_OPTIONAL  
 フィールドが省略可能であることを示します。  
  
 FIELD_MOD_BYREF  
 フィールドが参照引数であることを示します。 これは、メソッドの引数に特に使用されます。  
  
 FIELD_MOD_HIDDEN  
 フィールドを別のコンテキストで非表示または表示する必要があることを示します。たとえば、 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] static ローカルです。  
  
 FIELD_MOD_MARSHALASOBJECT  
 フィールドがインターフェイスを持つオブジェクトを表すことを示し `IUnknown` ます。  
  
 FIELD_MOD_SPECIAL_NAME  
 フィールドがコンストラクター (のみ) などの特別な名前を持つことを示し `.ctor` [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] ます。  
  
 FIELD_MOD_HIDEBYSIG  
 フィールドにキーワードが適用されていることを示し `Overloads` [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] ます (のみ)。  
  
 FIELD_MOD_WRITEONLY  
 フィールドが書き込み専用であることを示します。 この値はには含まれていません `FIELD_MOD_ALL` 。このような書き込み専用フィールドを使用するのは関数の評価だけであるためです。 ユーザーは、フィールドを明示的に要求する必要があり `FIELD_MOD_WRITEONLY` ます。  
  
 FIELD_MOD_ACCESS_MASK  
 フィールドアクセスのマスクを示します。  
  
 FIELD_MOD_MASK  
 フィールド修飾子のマスクを示します。  
  
## <a name="remarks"></a>注釈  
 `dwModifiers` [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)構造体のメンバーに使用されます。  
  
 これらの値は、特定のフィールドをフィルター処理するために、 [enumfields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md) メソッドにも渡されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [FIELD_INFO](../../../extensibility/debugger/reference/field-info.md)   
 [EnumFields](../../../extensibility/debugger/reference/idebugcontainerfield-enumfields.md)
