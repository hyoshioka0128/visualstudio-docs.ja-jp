---
title: SEEK_START |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SEEK_START
helpviewer_keywords:
- SEEK_START enumeration
ms.assetid: 55bd8901-626e-428b-a263-23b14417f4c6
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 45e664b153c4d643d8fbe8f1cefb207e0a76e18e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204875"
---
# <a name="seek_start"></a>SEEK_START
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

逆アセンブリストリームでシークを開始する位置を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_SEEK_START {   
   SEEK_START_BEGIN       = 0x0001,  
   SEEK_START_END         = 0x0002,  
   SEEK_START_CURRENT     = 0x0003,  
   SEEK_START_CODECONTEXT = 0x0004,  
   SEEK_START_CODELOCID   = 0x0005  
};  
typedef DWORD SEEK_START;  
```  
  
```csharp  
public enum enum_SEEK_START {   
   SEEK_START_BEGIN       = 0x0001,  
   SEEK_START_END         = 0x0002,  
   SEEK_START_CURRENT     = 0x0003,  
   SEEK_START_CODECONTEXT = 0x0004,  
   SEEK_START_CODELOCID   = 0x0005  
};  
```  
  
## <a name="members"></a>メンバー  
 SEEK_START_BEGIN  
 現在のドキュメントの先頭からシークを開始します。  
  
 SEEK_START_END  
 現在のドキュメントの末尾からシークを開始します。  
  
 SEEK_START_CURRENT  
 現在のドキュメントの現在位置からシークを開始します。  
  
 SEEK_START_CODECONTEXT  
 現在のドキュメントの指定されたコードコンテキストでシークを開始します。  
  
 SEEK_START_CODELOCID  
 指定されたコード位置識別子でシークを開始します。 コードの場所の識別子は、 [Getcurrentlocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)を呼び出すことによって取得されます。  
  
## <a name="remarks"></a>注釈  
 [Seek](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)メソッドに引数として渡されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [弁護士](../../../extensibility/debugger/reference/idebugdisassemblystream2-seek.md)   
 [GetCurrentLocation](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcurrentlocation.md)
