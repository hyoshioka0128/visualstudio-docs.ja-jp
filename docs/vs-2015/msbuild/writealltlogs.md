---
title: WriteAllTLogs |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
api_name:
- WriteAllTLogs
api_location:
- filetracker.dll
api_type:
- COM
helpviewer_keywords:
- WriteAllTLogs
ms.assetid: 1fa3e10b-263c-4960-a9ad-485c02a7a872
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 371357249bb9674a636859c995ad076eb41c2a08
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68192589"
---
# <a name="writealltlogs"></a>WriteAllTLogs
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

すべてのスレッドとコンテキストの追跡ログを書き込みます。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT WINAPI WriteAllTLogs(LPCTSTR intermediateDirectory, LPCTSTR tlogRootName);  
```  
  
#### <a name="parameters"></a>パラメーター  
 [入力] `intermediateDirectory`  
 追跡ログを格納するディレクトリ。  
  
 [入力] `tlogRootName`  
 ログ ファイル名のルート名。  
  
## <a name="return-value"></a>戻り値  
 [HRESULT] (<!-- TODO: review code entity reference <xref:assetId:///HRESULT?qualifyHint=False&amp;autoUpgrade=True>  -->) [成功] (<!-- TODO: review code entity reference <xref:assetId:///SUCCEEDED?qualifyHint=False&amp;autoUpgrade=True>  -->) 追跡コンテキストが作成された場合は、ビットセット。  
  
## <a name="requirements"></a>要件  
 **ヘッダー:** FileTracker.h  
  
## <a name="see-also"></a>参照  
 [WriteContextTLogs](../msbuild/writecontexttlogs.md)
