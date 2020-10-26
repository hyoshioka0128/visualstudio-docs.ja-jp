---
title: 'IDebugProgram2:: WriteDump |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProgram2::WriteDump
helpviewer_keywords:
- IDebugProgram2::WriteDump
ms.assetid: 375afb8c-882d-44db-bfa7-e2c9eb555122
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 491515d2778c6ad16287739bfc88d8134903d2bb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205797"
---
# <a name="idebugprogram2writedump"></a>IDebugProgram2::WriteDump
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ダンプをファイルに書き込みます。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT WriteDump(   
   DUMPTYPE  DumpType,  
   LPCOLESTR pszDumpUrl  
);  
```  
  
```csharp  
int WriteDump(   
   enum_DUMPTYPE  DumpType,  
   string         pszDumpUrl  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `DumpType`  
 からダンプの種類 (short、long など) を指定する [dumptype](../../../extensibility/debugger/reference/dumptype.md) 列挙の値です。  
  
 `pszDumpUrl`  
 からダンプの書き込み先の URL。 通常、これはの形式です `file://c:\path\filename.ext` が、任意の有効な URL にすることができます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 通常、プログラムダンプには、現在のスタックフレーム、スタック自体、プログラムで実行されているスレッドの一覧、およびプログラムが所有するメモリが含まれます。  
  
## <a name="see-also"></a>参照  
 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
