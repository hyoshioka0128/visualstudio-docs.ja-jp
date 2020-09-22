---
title: DBG_ATTRIB_FLAGS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- DBG_ATTRIB_FLAGS
helpviewer_keywords:
- DBGPROP_ATTRIB_FLAGS enumerations
ms.assetid: 2f13e601-dadc-476e-a8ec-01c4515082e7
caps.latest.revision: 18
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 74694c903040b278ed8864b46756cac66381405a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841500"
---
# <a name="dbg_attrib_flags"></a>DBG_ATTRIB_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

[IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)または[IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)インターフェイスのさまざまな属性について説明します。 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)構造体のメンバー。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
#define DBG_ATTRIB_NONE                 0x0000000000000000,  
#define DBG_ATTRIB_ALL                  0x00000000ffffffff,  
  
// Attributes about the object itself  
  
#define DBG_ATTRIB_OBJ_IS_EXPANDABLE    0x0000000000000001,  
#define DBG_ATTRIB_OBJ_HAS_ID           0x0000000000000002,  
#define DBG_ATTRIB_OBJ_CAN_HAVE_ID      0x0000000000000004,  
  
// Attributes about the value of the object  
  
#define DBG_ATTRIB_VALUE_READONLY       0x0000000000000010,  
#define DBG_ATTRIB_VALUE_ERROR          0x0000000000000020,  
#define DBG_ATTRIB_VALUE_SIDE_EFFECT    0x0000000000000040,  
#define DBG_ATTRIB_OVERLOADED_CONTAINER 0x0000000000000080,  
#define DBG_ATTRIB_VALUE_BOOLEAN        0x0000000000000100,  
#define DBG_ATTRIB_VALUE_BOOLEAN_TRUE   0x0000000000000200,  
#define DBG_ATTRIB_VALUE_INVALID        0x0000000000000400,  
#define DBG_ATTRIB_VALUE_NAT            0x0000000000000800,  
#define DBG_ATTRIB_VALUE_AUTOEXPANDED   0x0000000000001000,  
#define DBG_ATTRIB_VALUE_TIMEOUT        0x0000000000002000,  
#define DBG_ATTRIB_VALUE_RAW_STRING     0x0000000000004000,  
#define DBG_ATTRIB_VALUE_CUSTOM_VIEWER  0x0000000000008000,  
  
// Attributes about field access types for the object  
  
#define DBG_ATTRIB_ACCESS_NONE          0x0000000000010000,  
#define DBG_ATTRIB_ACCESS_PUBLIC        0x0000000000020000,  
#define DBG_ATTRIB_ACCESS_PRIVATE       0x0000000000040000,  
#define DBG_ATTRIB_ACCESS_PROTECTED     0x0000000000080000,  
#define DBG_ATTRIB_ACCESS_FINAL         0x0000000000100000,  
#define DBG_ATTRIB_ACCESS_ALL           0x00000000001f0000,  
  
// Attributes for the storage types of the object  
  
#define DBG_ATTRIB_STORAGE_NONE         0x0000000001000000,  
#define DBG_ATTRIB_STORAGE_GLOBAL       0x0000000002000000,  
#define DBG_ATTRIB_STORAGE_STATIC       0x0000000004000000,  
#define DBG_ATTRIB_STORAGE_REGISTER     0x0000000008000000,  
#define DBG_ATTRIB_STORAGE_ALL          0x000000000f000000,  
  
// Attributes for the type modifiers on the object  
  
#define DBG_ATTRIB_TYPE_NONE            0x0000000100000000,  
#define DBG_ATTRIB_TYPE_VIRTUAL         0x0000000200000000,  
#define DBG_ATTRIB_TYPE_CONSTANT        0x0000000400000000,  
#define DBG_ATTRIB_TYPE_SYNCHRONIZED    0x0000000800000000,  
#define DBG_ATTRIB_TYPE_VOLATILE        0x0000001000000000,  
#define DBG_ATTRIB_TYPE_ALL             0x0000001f00000000,  
  
// Attributes that describe the type of object  
  
#define DBG_ATTRIB_DATA                 0x0000010000000000,  
#define DBG_ATTRIB_METHOD               0x0000020000000000,  
#define DBG_ATTRIB_PROPERTY             0x0000040000000000,  
#define DBG_ATTRIB_CLASS                0x0000080000000000,  
#define DBG_ATTRIB_BASECLASS            0x0000100000000000,  
#define DBG_ATTRIB_INTERFACE            0x0000200000000000,  
#define DBG_ATTRIB_INNERCLASS           0x0000400000000000,  
#define DBG_ATTRIB_MOSTDERIVED          0x0000800000000000,  
#define DBG_ATTRIB_CHILD_ALL            0x0000ff0000000000,  
  
// Miscellaneous attributes  
  
#define DBG_ATTRIB_MULTI_CUSTOM_VIEWERS 0x0001000000000000  
  
typedef UINT64 DBG_ATTRIB_FLAGS;  
```  
  
```csharp  
public const int DBG_ATTRIB_NONE                 = 0x0000000000000000,  
public const int DBG_ATTRIB_ALL                  = 0x00000000ffffffff,  
  
// Attributes about the object itself  
  
public const int DBG_ATTRIB_OBJ_IS_EXPANDABLE    = 0x0000000000000001,  
public const int DBG_ATTRIB_OBJ_HAS_ID           = 0x0000000000000002,  
public const int DBG_ATTRIB_OBJ_CAN_HAVE_ID      = 0x0000000000000004,  
  
// Attributes about the value of the object  
  
public const int DBG_ATTRIB_VALUE_READONLY       = 0x0000000000000010,  
public const int DBG_ATTRIB_VALUE_ERROR          = 0x0000000000000020,  
public const int DBG_ATTRIB_VALUE_SIDE_EFFECT    = 0x0000000000000040,  
public const int DBG_ATTRIB_OVERLOADED_CONTAINER = 0x0000000000000080,  
public const int DBG_ATTRIB_VALUE_BOOLEAN        = 0x0000000000000100,  
public const int DBG_ATTRIB_VALUE_BOOLEAN_TRUE   = 0x0000000000000200,  
public const int DBG_ATTRIB_VALUE_INVALID        = 0x0000000000000400,  
public const int DBG_ATTRIB_VALUE_NAT            = 0x0000000000000800,  
public const int DBG_ATTRIB_VALUE_AUTOEXPANDED   = 0x0000000000001000,  
public const int DBG_ATTRIB_VALUE_TIMEOUT        = 0x0000000000002000,  
public const int DBG_ATTRIB_VALUE_RAW_STRING     = 0x0000000000004000,  
public const int DBG_ATTRIB_VALUE_CUSTOM_VIEWER  = 0x0000000000008000,  
  
// Attributes about field access types for the object  
  
public const int DBG_ATTRIB_ACCESS_NONE          = 0x0000000000010000,  
public const int DBG_ATTRIB_ACCESS_PUBLIC        = 0x0000000000020000,  
public const int DBG_ATTRIB_ACCESS_PRIVATE       = 0x0000000000040000,  
public const int DBG_ATTRIB_ACCESS_PROTECTED     = 0x0000000000080000,  
public const int DBG_ATTRIB_ACCESS_FINAL         = 0x0000000000100000,  
public const int DBG_ATTRIB_ACCESS_ALL           = 0x00000000001f0000,  
  
// Attributes for the storage types of the object  
  
public const int DBG_ATTRIB_STORAGE_NONE         = 0x0000000001000000,  
public const int DBG_ATTRIB_STORAGE_GLOBAL       = 0x0000000002000000,  
public const int DBG_ATTRIB_STORAGE_STATIC       = 0x0000000004000000,  
public const int DBG_ATTRIB_STORAGE_REGISTER     = 0x0000000008000000,  
public const int DBG_ATTRIB_STORAGE_ALL          = 0x000000000f000000,  
  
// Attributes for the type modifiers on the object  
  
public const int DBG_ATTRIB_TYPE_NONE            = 0x0000000100000000,  
public const int DBG_ATTRIB_TYPE_VIRTUAL         = 0x0000000200000000,  
public const int DBG_ATTRIB_TYPE_CONSTANT        = 0x0000000400000000,  
public const int DBG_ATTRIB_TYPE_SYNCHRONIZED    = 0x0000000800000000,  
public const int DBG_ATTRIB_TYPE_VOLATILE        = 0x0000001000000000,  
public const int DBG_ATTRIB_TYPE_ALL             = 0x0000001f00000000,  
  
// Attributes that describe the type of object  
  
public const int DBG_ATTRIB_DATA                 = 0x0000010000000000,  
public const int DBG_ATTRIB_METHOD               = 0x0000020000000000,  
public const int DBG_ATTRIB_PROPERTY             = 0x0000040000000000,  
public const int DBG_ATTRIB_CLASS                = 0x0000080000000000,  
public const int DBG_ATTRIB_BASECLASS            = 0x0000100000000000,  
public const int DBG_ATTRIB_INTERFACE            = 0x0000200000000000,  
public const int DBG_ATTRIB_INNERCLASS           = 0x0000400000000000,  
public const int DBG_ATTRIB_MOSTDERIVED          = 0x0000800000000000,  
public const int DBG_ATTRIB_CHILD_ALL            = 0x0000ff0000000000,  
  
// Miscellaneous attributes  
  
public const int DBG_ATTRIB_MULTI_CUSTOM_VIEWERS = 0x0001000000000000  
```  
  
## <a name="members"></a>メンバー  
 DBG_ATTRIB_NONE  
 属性がないことを示します。  
  
 DBG_ATTRIB_ALL  
 すべての属性を示します。  
  
 DBG_ATTRIB_OBJ_IS_EXPANDABLE  
 参照またはプロパティが子を持つことを示します。  
  
 DBG_ATTRIB_OBJ_HAS_ID  
 このオブジェクトの ID が作成されたことを示します。  
  
 DBG_ATTRIB_OBJ_CAN_HAVE_ID  
 このオブジェクトの ID を作成できることを示します。  
  
 DBG_ATTRIB_VALUE_READONLY  
 値が読み取り専用であることを示します。  
  
 DBG_ATTRIB_VALUE_ERROR  
 値がエラーであることを示します。  
  
 DBG_ATTRIB_VALUE_SIDE_EFFECT  
 評価に副作用があったことを示します。  
  
 DBG_ATTRIB_OVERLOADED_CONTAINER  
 このプロパティが実際にはオーバーロードのコンテナーであることを示します。  
  
 DBG_ATTRIB_VALUE_BOOLEAN  
 の値がブール値であることを示し `DEBUG_PROPERTY_INFO::bstrValue` ます。  
  
 DBG_ATTRIB_VALUE_BOOLEAN_TRUE  
 の値がブール値であり、であることを示し `DEBUG_PROPERTY_INFO::bstrValue` `TRUE` ます。  
  
 DBG_ATTRIB_VALUE_INVALID  
 `DEBUG_PROPERTY_INFO::bstrValue` 内の値が無効であることを示します。  
  
 DBG_ATTRIB_VALUE_NAT  
 の値 `DEBUG_PROPERTY_INFO::bstrValue` が "*not a*" (NAT) であることを示します。 NAT は、遅延予測例外を示す Intel 64 ビットプロセッサのレジスタフラグを記述します。  
  
 DBG_ATTRIB_VALUE_AUTOEXPANDED  
 の値が `DEBUG_PROPERTY_INFO::bstrValue` 自動展開されている可能性があることを示します。  
  
 DBG_ATTRIB_VALUE_TIMEOUT  
 評価がタイムアウトしたことを示します。  
  
 DBG_ATTRIB_VALUE_RAW_STRING  
 の値を生の `DEBUG_PROPERTY_INFO::bstrValue` 文字列で表すことができることを示します。  
  
 DBG_ATTRIB_VALUE_CUSTOM_VIEWER  
 このプロパティに少なくとも1つのカスタムビューアーが関連付けられていることを示します。  
  
 DBG_ATTRIB_ACCESS_NONE  
 、、または型のアクセスを持たないオブジェクトを示し `public` `private` `protected` ます。  
  
 DBG_ATTRIB_ACCESS_PUBLIC  
 パブリック アクセスを持つオブジェクトであることを示します。  
  
 DBG_ATTRIB_ACCESS_PRIVATE  
 プライベート アクセスを持つオブジェクトであることを示します。  
  
 DBG_ATTRIB_ACCESS_PROTECTED  
 保護されたアクセスを持つオブジェクトであることを示します。  
  
 DBG_ATTRIB_ACCESS_FINAL  
 最終的なアクセスを持つオブジェクトであることを示します。  
  
 DBG_ATTRIB_ACCESS_ALL  
 アクセス属性を抽出するマスク `DBG_ATTRIB_FLAGS` 。  
  
 DBG_ATTRIB_STORAGE_NONE  
 ストレージの種類が指定されていないことを示します。  
  
 DBG_ATTRIB_STORAGE_GLOBAL  
 グローバル ストレージであることを示します。  
  
 DBG_ATTRIB_STORAGE_STATIC  
 静的ストレージであることを示します。  
  
 DBG_ATTRIB_STORAGE_REGISTER  
 レジスタ内のストレージを示します。  
  
 DBG_ATTRIB_STORAGE_ALL  
 ストレージ属性の抽出元となるマスク `DBG_ATTRIB_FLAGS` 。  
  
 DBG_ATTRIB_TYPE_NONE  
 型修飾子がないことを示します。  
  
 DBG_ATTRIB_TYPE_VIRTUAL  
 オブジェクトの型が virtual であることを示します。  
  
 DBG_ATTRIB_TYPE_CONSTANT  
 オブジェクトの型が定数であることを示します。  
  
 DBG_ATTRIB_TYPE_SYNCHRONIZED  
 オブジェクトの型が同期されていることを示します。  
  
 DBG_ATTRIB_TYPE_VOLATILE  
 オブジェクトの型が volatile であることを示します。  
  
 DBG_ATTRIB_TYPE_ALL  
 型属性を抽出するマスク `DBG_ATTRIB_FLAGS` 。  
  
 DBG_ATTRIB_DATA  
 このオブジェクトがデータフィールドであることを示します。  
  
 DBG_ATTRIB_METHOD  
 このオブジェクトがメソッドであることを示します。  
  
 DBG_ATTRIB_PROPERTY  
 このオブジェクトがプロパティであることを示します。  
  
 DBG_ATTRIB_CLASS  
 このオブジェクトがクラスであることを示します。  
  
 DBG_ATTRIB_BASECLASS  
 このオブジェクトが基底クラスであることを示します。  
  
 DBG_ATTRIB_INTERFACE  
 このオブジェクトがインターフェイスであることを示します。  
  
 DBG_ATTRIB_INNERCLASS  
 このオブジェクトが内部クラスであることを示します。  
  
 DBG_ATTRIB_MOSTDERIVED  
 このオブジェクトが '*最派生*' であることを示します。 "*最派生*" という用語は、その参照の型ではなく、オブジェクトの実際の型を意味します。  
  
 DBG_ATTRIB_CHILD_ALL  
 を通じてのマスクを示し `DBG_ATTRIB_DATA` `DBG_ATTRIB_MOSTDERIVED` ます。  
  
 DBG_ATTRIB_MULTI_CUSTOM_VIEWERS  
 オブジェクトに複数のカスタムビューアーが関連付けられていることを示します。  
  
## <a name="remarks"></a>注釈  
  
> [!NOTE]
> この列挙体の値は、実際には C# のアセンブリで定義されていません。 代わりに、定義をソースファイルにコピーする必要があります。  
  
 これらのフラグは、オブジェクトの子をフィルター処理するためにも使用されます。たとえば、 [enumchildren](../../../extensibility/debugger/reference/idebugproperty2-enumchildren.md)に引数として渡される場合です。 値は、ビットごとのを使用して組み合わせることができ `OR` ます。  
  
 `DBG_ATTRIB_VALUE_CUSTOM_VIEWER`フラグは、 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)インターフェイスから[IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)インターフェイスを取得し、 [GetCustomViewerList](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewerlist.md)を呼び出してカスタムビューアーの一覧を取得することを示しています。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)   
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)   
 [IDebugReference2](../../../extensibility/debugger/reference/idebugreference2.md)   
 [DEBUG_PROPERTY_INFO](../../../extensibility/debugger/reference/debug-property-info.md)
