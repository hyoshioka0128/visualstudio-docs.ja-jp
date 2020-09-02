---
title: SccGetVersion 関数 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- SccGetVersion
helpviewer_keywords:
- SccGetVersion function
ms.assetid: a6e786bf-744e-4272-9e21-0be44d23b1a1
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a4e548f1f2b82a97206cdf41174a8c1c7d61e885
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68200045"
---
# <a name="sccgetversion-function"></a>SccGetVersion 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

この関数は、ソース管理プラグインによってサポートされているソース管理プラグイン API のバージョン番号を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
LONG SccGetVersion(void);  
```  
  
#### <a name="parameters"></a>パラメーター  
 [なし] :  
  
## <a name="return-value"></a>戻り値  
 `LONG`サポートされているソース管理プラグイン API のバージョン番号を含むデータ型。  
  
|WORD|説明|  
|----------|-----------------|  
|HIWORD|メジャー バージョン|  
|LOWORD|マイナー バージョン|  
  
## <a name="remarks"></a>注釈  
 たとえば、ソース管理プラグインがソース管理プラグイン API のバージョン1.3 をサポートしている場合、この関数は0x0103 を返します。  
  
## <a name="see-also"></a>参照  
 [ソース管理プラグインの API 関数](../extensibility/source-control-plug-in-api-functions.md)
