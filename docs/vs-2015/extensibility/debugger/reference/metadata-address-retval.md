---
title: METADATA_ADDRESS_RETVAL |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- METADATA_ADDRESS_RETVAL
helpviewer_keywords:
- METADATA_ADDRESS_RETVAL structure
ms.assetid: 5b0ec0fb-84b3-4ce7-8e24-becf3d881d7d
caps.latest.revision: 7
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6f685bcfad5cf576215aa50aa26540ba207de2e0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62546864"
---
# <a name="metadata_address_retval"></a>METADATA_ADDRESS_RETVAL
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

この構造体は、メソッドまたは関数からの戻り値を表します。  
  
## <a name="syntax"></a>Syntax  
  
```cpp  
typedef struct _tagMETADATA_ADDRESS_RETVAL {  
   _mdToken tokMethod;  
   DWORD    dwCorType;  
   DWORD    dwSigSize;  
   BYTE     rgSig[10];  
} METADATA_ADDRESS_RETVAL;  
```  
  
```csharp  
public struct METADATA_ADDRESS_RETVAL {  
   public int    tokMethod;  
   public uint   dwCorType;  
   public uint   dwSigSize;  
   public byte[] rgSig;  
}  
```  
  
## <a name="terms"></a>用語  
 tokMethod  
 この戻り値の対象となるメソッドの ID。  
  
 dwCorType  
 戻り値の基本型。 これは、 `CorElementType` [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] SDK corhdr .h ファイルで定義されている列挙体の値です。  
  
 dwSigSize  
 戻り値のシグネチャのサイズ (に格納されている `rgSig` )。  
  
 rgSig  
 戻り値の署名を形成するバイト配列。  
  
## <a name="remarks"></a>注釈  
 この構造体は、構造体のフィールドがに設定されている場合に、 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md) 構造体の和集合の一部になり `dwKind` `DEBUG_ADDRESS_UNION` `ADDRESS_KIND_RETVAL` ます ( [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md) 列挙型の値)。  
  
## <a name="requirements"></a>要件  
 ヘッダー: sh. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [構造体と共用体](../../../extensibility/debugger/reference/structures-and-unions.md)   
 [DEBUG_ADDRESS_UNION](../../../extensibility/debugger/reference/debug-address-union.md)   
 [ADDRESS_KIND](../../../extensibility/debugger/reference/address-kind.md)
