---
title: BP_LOCATION_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BP_LOCATION_TYPE
helpviewer_keywords:
- BP_LOCATION_TYPE structure
ms.assetid: 0248430a-3b61-4809-87a9-e9b6bb7d1130
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fb8074317e52b43806a61d6486c53d7409333e2c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153401"
---
# <a name="bp_location_type"></a>BP_LOCATION_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイント要求のブレークポイントの場所の種類を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_BP_LOCATION_TYPE {   
   BPLT_NONE               = 0x00000000,  
   BPLT_FILE_LINE          = 0x00010000,  
   BPLT_FUNC_OFFSET        = 0x00020000,  
   BPLT_CONTEXT            = 0x00030000,  
   BPLT_STRING             = 0x00040000,  
   BPLT_ADDRESS            = 0x00050000,  
   BPLT_RESOLUTION         = 0x00060000,  
   BPLT_CODE_FILE_LINE     = BPT_CODE | BPLT_FILE_LINE,  
   BPLT_CODE_FUNC_OFFSET   = BPT_CODE | BPLT_FUNC_OFFSET,  
   BPLT_CODE_CONTEXT       = BPT_CODE | BPLT_CONTEXT,  
   BPLT_CODE_STRING        = BPT_CODE | BPLT_STRING,  
   BPLT_CODE_ADDRESS       = BPT_CODE | BPLT_ADDRESS ,  
   BPLT_DATA_STRING        = BPT_DATA | BPLT_STRING,  
   BPLT_TYPE_MASK          = 0x0000FFFF,  
   BPLT_LOCATION_TYPE_MASK = 0xFFFF0000  
};  
typedef DWORD BP_LOCATION_TYPE;  
```  
  
```csharp  
public enum enum_BP_LOCATION_TYPE {   
   BPLT_NONE               = 0x00000000,  
   BPLT_FILE_LINE          = 0x00010000,  
   BPLT_FUNC_OFFSET        = 0x00020000,  
   BPLT_CONTEXT            = 0x00030000,  
   BPLT_STRING             = 0x00040000,  
   BPLT_ADDRESS            = 0x00050000,  
   BPLT_RESOLUTION         = 0x00060000,  
   BPLT_CODE_FILE_LINE     = BPT_CODE | BPLT_FILE_LINE,  
   BPLT_CODE_FUNC_OFFSET   = BPT_CODE | BPLT_FUNC_OFFSET,  
   BPLT_CODE_CONTEXT       = BPT_CODE | BPLT_CONTEXT,  
   BPLT_CODE_STRING        = BPT_CODE | BPLT_STRING,  
   BPLT_CODE_ADDRESS       = BPT_CODE | BPLT_ADDRESS ,  
   BPLT_DATA_STRING        = BPT_DATA | BPLT_STRING,  
   BPLT_TYPE_MASK          = 0x0000FFFF,  
   BPLT_LOCATION_TYPE_MASK = 0xFFFF0000  
};  
```  
  
## <a name="members"></a>メンバー  
 BPLT_NONE  
 ブレークポイントの位置を指定しません。  
  
 BPLT_FILE_LINE  
 ブレークポイントの場所の種類をファイル行として指定します。  
  
 BPLT_FUNC_OFFSET  
 ブレークポイントの場所の種類を関数オフセットとして指定します。  
  
 BPLT_CONTEXT  
 ブレークポイントの場所の種類をコンテキストとして指定します。  
  
 BPLT_STRING  
 ブレークポイントの場所の種類を文字列として指定します。  
  
 BPLT_ADDRESS  
 ブレークポイントの場所の種類をアドレスとして指定します。  
  
 BPLT_RESOLUTION  
 ブレークポイントの場所の種類を解決として指定します。  
  
 BPLT_CODE_FILE_LINE  
 ソースコードの行として、ブレークポイントの場所の種類を指定します。  
  
 BPLT_CODE_FUNC_OFFSET  
 ブレークポイントの場所の種類をコード関数オフセットとして指定します。  
  
 BPLT_CODE_CONTEXT  
 ブレークポイントの場所の種類をコードコンテキストとして指定します。  
  
 BPLT_CODE_STRING  
 ブレークポイントの場所の種類をコード文字列として指定します。  
  
 BPLT_CODE_ADDRESS  
 ブレークポイントの場所の種類をコードアドレスとして指定します。  
  
 BPLT_DATA_STRING  
 ブレークポイントの場所の種類をデータ文字列として指定します。  
  
 BPLT_TYPE_MASK  
 値からブレークポイントの種類を抽出できるように、ビットマスクを指定します。  
  
 BPLT_LOCATION_TYPE_MASK  
 ブレークポイントの位置の種類を値から抽出できるように、ビットマスクを指定します。  
  
## <a name="remarks"></a>注釈  
 [GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)メソッドにパラメーターとして渡されます。  
  
 ブレークポイントの位置の種類は、ブレークポイントの種類と場所の種類で構成されます。 つまり、ブレークポイントの場所の種類は、ブレークポイントの種類 (など `BPT_CODE` ) または場所の種類 (たとえば、) にすぎません `BPLT_FILE_LINE` 。 現在サポートされているすべてのブレークポイントの場所の型の定義済み定数は、この列挙に含まれてい `BPLT_CODE_FILE_LINE` ます (から `BPLT_DATA_STRING` )。  
  
 `BPT_CODE` および `BPT_DATA` は [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md) 列挙型のメンバーです。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)   
 [BP_TYPE](../../../extensibility/debugger/reference/bp-type.md)
