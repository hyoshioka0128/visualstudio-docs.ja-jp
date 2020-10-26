---
title: UNMANAGED_ADDRESS_PHYSICAL |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- UNMANAGED_ADDRESS_PHYSICAL
helpviewer_keywords:
- UNMANAGED_ADDRESS_PHYSICAL structure
ms.assetid: fed09686-caa6-4efc-851e-a0432019e9d0
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8f8eccadbb2ae29f684c8c760ab34dae59c79ac7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204765"
---
# <a name="unmanaged_address_physical"></a>UNMANAGED_ADDRESS_PHYSICAL
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

この構造体は、物理アドレスを表します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
typedef struct _tagUNMANAGED_ADDRESS_PHYSICAL {  
   ULONGLONG offset;  
} UNMANAGED_ADDRESS_PHYSICAL;  
```  
  
```csharp  
public struct UNMANAGED_ADDRESS_PHYSICAL {  
   public ulong offset;  
}  
```  
  
## <a name="terms"></a>用語  
 offset  
 物理アドレス空間への64ビットオフセット。  
  
## <a name="remarks"></a>注釈  
 この構造体は、構造体のフィールドがに設定されている場合に、 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 構造体の和集合の一部になり `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_UNMANAGED_PHYSICAL` ます ( [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙型の値)。  
  
## <a name="requirements"></a>要件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)
