---
title: SccGetExtendedCapabilities 関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccGetExtendedCapabilities
helpviewer_keywords:
- SccGetExtendedCapabilities function
ms.assetid: 588c6a92-2147-4d8b-a357-96ca7da0a092
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f02591eac6a3f69ae5513aa9dc0abed381cd1c8a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200103"
---
# <a name="sccgetextendedcapabilities-function"></a>SccGetExtendedCapabilities 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関数は、ソース管理プラグインによってサポートされている追加の機能を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
SCCRTN SccGetExtendedCapabilities(  
   LPVOID pContext,  
   LONG lSccExCaps,  
   LPBOOL pbSupported  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 pContext  
 からソース管理プラグインのコンテキストポインター。  
  
 lSccExCaps  
 からテストする拡張機能を指定するフラグ (使用可能なフラグについては、 [機能フラグ](../extensibility/capability-flags.md) の拡張機能コードテーブルを参照してください)。  
  
 pbSupported  
 入出力指定した機能がサポートされている場合は0以外 () を返します `TRUE` 。それ以外の場合は 0 () を返し `FALSE` ます。  
  
## <a name="return-value"></a>戻り値  
 この関数のソース管理プラグインの実装では、次の値のいずれかが返されることが想定されています。  
  
|値|説明|  
|-----------|-----------------|  
|SCC_OK|機能の取得操作が正常に完了しました。|  
|SCC_E_UNKNOWNERROR<br /><br /> SCC_E_NONSPECIFICERROR|不明または特定できないエラーが発生しました。|  
  
## <a name="remarks"></a>注釈  
 このメソッドは、オンデマンドで呼び出されます。つまり、機能をテストする必要がある場合は、このメソッドを呼び出して、その機能がサポートされているかどうかを判断します。 一度に1つのフラグのみが指定されています。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグイン API 関数](../extensibility/source-control-plug-in-api-functions.md)   
 [エラーコード](../extensibility/error-codes.md)   
 [機能フラグ](../extensibility/capability-flags.md)
