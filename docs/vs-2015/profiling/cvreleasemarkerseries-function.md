---
title: CvReleaseMarkerSeries 関数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- cvmarkers/CvReleaseMarkerSeries
helpviewer_keywords:
- CvReleaseMarkerSeries method
ms.assetid: 3b4711ee-e534-411d-9128-f69cd7932a48
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6bfa9952a834110ef0fea36568ea210b637547aa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68177751"
---
# <a name="cvreleasemarkerseries-function"></a>CvReleaseMarkerSeries 関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

マーカー系列をリリースします。 リリース後はマーカー系列オブジェクトを使用しないでください。使用すると、アプリケーションがクラッシュすることがあります。 マーカー系列のリリースに失敗すると、メモリ漏れが発生します。  
  
## <a name="syntax"></a>構文  
  
```  
HRESULT CvReleaseMarkerSeries(  
   _In_reads_bytes_(16) PCV_MARKERSERIES pMarkerSeries  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pMarkerSeries`  
 プロバイダー オブジェクト変数のアドレス。 アドレスには NULL を指定できません。変数には値を含めることができます。  
  
## <a name="return-value"></a>戻り値  
 マーカー系列がリリースされると S_OK を、エラーが発生した場合はエラー コードを返します。 SUCCEEDED/FAILED マクロを使用し、エラーの状態を確認します。  
  
## <a name="requirements"></a>必要条件  
 **ヘッダー:** cvmarkers.h  
  
## <a name="see-also"></a>参照  
 [C++ ライブラリリファレンス](../profiling/cpp-library-reference.md)
