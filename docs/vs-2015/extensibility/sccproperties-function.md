---
title: SccProperties 関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccProperties
helpviewer_keywords:
- SccProperties function
ms.assetid: 1bed38c9-73d2-4474-9717-f9dc26a89cbe
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f4e8452465873cb66883abd347406d17b469e90a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68199996"
---
# <a name="sccproperties-function"></a>SccProperties 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関数は、ファイルまたはプロジェクトのソース管理プロパティを表示します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
SCCRTN SccProperties (  
   LPVOID pvContext,  
   HWND   hWnd,  
   LPCSTR lpFileName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pvContext  
 からソース管理プラグインのコンテキスト構造。  
  
 hWnd  
 からソース管理プラグインが提供するすべてのダイアログボックスの親として使用できる IDE ウィンドウへのハンドル。  
  
 lpFileName  
 からファイルまたはプロジェクトの完全修飾パス名。  
  
## <a name="return-value"></a>戻り値  
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_OK|プロパティが正常に表示されました。|  
|SCC_I_RELOADFILE|バージョンコントロールシステムによってファイルのプロパティが変更されたため、IDE がこのファイルを再読み込みする必要があります。|  
|SCC_E_PROJNOTOPEN|指定されたプロジェクトは、ソース管理で開かれていません。|  
|SCC_E_NOTAUTHORIZED|このファイルまたはプロジェクトのプロパティを表示する権限がユーザーにありません。|  
|SCC_E_FILENOTCONTROLLED|指定されたファイルまたはプロジェクトは、ソース管理下にありません。|  
|SCC_E_NONSPECIFICERROR<br /><br /> SCC_E_UNKNOWNERROR|不明または一般的なエラーが発生しました。|  
  
## <a name="remarks"></a>注釈  
 ソース管理プラグインによって、独自のダイアログボックスにプロパティが表示されます。  
  
 プロパティはソース管理プラグインによって定義され、プラグインにプラグインとは異なる場合があります。 プラグインでファイルのソース管理プロパティを変更できる場合、 `SCC_I_RELOAD` このファイルまたはプロジェクトを再読み込みする必要があることを IDE に通知するために、が返されます。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
