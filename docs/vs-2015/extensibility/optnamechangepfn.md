---
title: OPTNAMECHANGEPFN |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- OPTNAMECHANGEPFN
helpviewer_keywords:
- OPTNAMECHANGEPFN callback function
ms.assetid: 147303f3-c7f1-438a-81b7-db891ea3d076
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4969dff811b6517c0274a35884703a9dc0c693cb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194104"
---
# <a name="optnamechangepfn"></a>OPTNAMECHANGEPFN
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

これは、 [Sccsetoption](../extensibility/sccsetoption-function.md) (using オプション) の呼び出しで指定されたコールバック関数であり、 `SCC_OPT_NAMECHANGEPFN` ソース管理プラグインによって IDE に戻された名前の変更を通知するために使用されます。  
  
## <a name="signature"></a>署名  
  
```cpp#  
typedef void (*OPTNAMECHANGEPFN)(  
   LPVOID pvCallerData,  
   LPCSTR pszOldName,  
   LPCSTR pszNewName  
);  
```  
  
## <a name="parameters"></a>パラメーター  
 pvCallerData  
 から [Sccsetoption](../extensibility/sccsetoption-function.md) の前の呼び出しで指定されたユーザー値 (オプションを使用 `SCC_OPT_USERDATA` )。  
  
 pszOldName  
 からファイルの元の名前。  
  
 pszNewName  
 からファイルの名前が変更された名前。  
  
## <a name="return-value"></a>戻り値  
 [なし] :  
  
## <a name="remarks"></a>解説  
 ソース管理操作中にファイルの名前が変更された場合、ソース管理プラグインは、このコールバックによって名前の変更について IDE に通知できます。  
  
 IDE がこのコールバックをサポートしていない場合は、 [Sccsetoption](../extensibility/sccsetoption-function.md) を呼び出して指定しません。 プラグインがこのコールバックをサポートしていない場合、 `SCC_E_OPNOTSUPPORTED` `SccSetOption` IDE がコールバックを設定しようとすると、関数からが返されます。  
  
## <a name="see-also"></a>参照  
 [IDE によって実装されるコールバック関数](../extensibility/callback-functions-implemented-by-the-ide.md)   
 [SccSetOption](../extensibility/sccsetoption-function.md)
