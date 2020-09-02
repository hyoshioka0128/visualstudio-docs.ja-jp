---
title: METADATA_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- METADATA_TYPE
helpviewer_keywords:
- METADATA_TYPE structure
ms.assetid: 2d8b78f6-0aef-4d79-809a-cff9b2c24659
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 1be7cb6071a0307a56285b8929e52e038c263fdc
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62546825"
---
# <a name="metadata_type"></a>METADATA_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

この構造体は、メタデータから取得されたフィールド型に関する情報を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
typedef struct _tagTYPE_METADATA {  
   ULONG32  ulAppDomainID;  
   GUID     guidModule;  
   _mdToken tokClass;  
} METADATA_TYPE;  
```  
  
```csharp  
public struct METADATA_TYPE {  
   public uint ulAppDomainID;  
   public Guid guidModule;  
   public int  tokClass;  
};  
```  
  
#### <a name="parameters"></a>パラメーター  
 ulAppDomainID  
 シンボルの取得元のアプリケーションの ID。 これは、アプリケーションのインスタンスを一意に識別するために使用されます。  
  
 guidModule  
 このフィールドを含むモジュールの GUID。  
  
 tokClass  
 この型のメタデータトークン ID。  
  
 [C++] `_mdToken` は、 `typedef` 32 ビットのです `int` 。  
  
## <a name="remarks"></a>注釈  
 この構造体は、構造体のフィールドがに設定されている場合に、 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md) 構造体の共用体の一部として表示され `dwKind` `TYPE_INFO` `TYPE_KIND_METADATA` ます ( [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md) 列挙型の値)。  
  
 `tokClass`値は、型を一意に識別するメタデータトークンです。 メタデータトークン ID の上位ビットを解釈する方法の詳細については、 `CorTokenType` SDK の corhdr .h ファイルの列挙体を参照してください [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 。  
  
## <a name="requirements"></a>要件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [TYPE_INFO](../../../extensibility/debugger/reference/type-info.md)   
 [dwTYPE_KIND](../../../extensibility/debugger/reference/dwtype-kind.md)
