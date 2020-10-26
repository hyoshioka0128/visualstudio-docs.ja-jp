---
title: GETNAME_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- GETNAME_TYPE
helpviewer_keywords:
- GETNAME_TYPE enumeration
ms.assetid: 2f9f1679-e9e8-4c9c-ac90-aa07bfe69914
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 648f84b106dab7aa6e38cc3e45e59162a216a875
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68160139"
---
# <a name="getname_type"></a>GETNAME_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

取得するファイルの名前の種類を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_GETNAME_TYPE {   
   GN_NAME         = 0,  
   GN_FILENAME     = 1,  
   GN_BASENAME     = 2,  
   GN_MONIKERNAME  = 3,  
   GN_URL          = 4,  
   GN_TITLE        = 5,  
   GN_STARTPAGEURL = 6  
};  
typedef DWORD GETNAME_TYPE;  
```  
  
```csharp  
public enum enum_GETNAME_TYPE {   
   GN_NAME         = 0,  
   GN_FILENAME     = 1,  
   GN_BASENAME     = 2,  
   GN_MONIKERNAME  = 3,  
   GN_URL          = 4,  
   GN_TITLE        = 5,  
   GN_STARTPAGEURL = 6  
};  
```  
  
## <a name="members"></a>メンバー  
 GN_NAME  
 ドキュメントまたはコンテキストのフレンドリ名を指定します。  
  
 GN_FILENAME  
 ドキュメントまたはコンテキストの完全パスを指定します。  
  
 GN_BASENAME  
 ドキュメントまたはコンテキストの完全パスではなく、基本ファイル名を指定します。  
  
 GN_MONIKERNAME  
 モニカーの形式で、ドキュメントまたはコンテキストの一意な名前を指定します。  
  
 GN_URL  
 ドキュメントまたはコンテキストの URL 名を指定します。  
  
 GN_TITLE  
 ドキュメントのタイトルを指定します (存在する場合)。  
  
 GN_STARTPAGEURL  
 プロセスの開始ページの URL を取得します。  
  
## <a name="remarks"></a>注釈  
 これらの値は、返される名前の種類を指定するために、 [getname](../../../extensibility/debugger/reference/idebugdocument2-getname.md)、 [Getname](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)、および [getname](../../../extensibility/debugger/reference/idebugprocess2-getname.md) メソッドにパラメーターとして渡されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [GetName](../../../extensibility/debugger/reference/idebugdocument2-getname.md)   
 [GetName](../../../extensibility/debugger/reference/idebugdocumentcontext2-getname.md)   
 [GetName](../../../extensibility/debugger/reference/idebugprocess2-getname.md)
