---
title: diagnostic 名前空間 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic
helpviewer_keywords:
- Concurrency::diagnostic namespace
ms.assetid: ad786b19-7c4c-46ee-bfb6-c4752b373a09
caps.latest.revision: 11
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d412cfa5a9b5e7e90aeac3ac6bbb530b0ef48ad0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157577"
---
# <a name="diagnostic-namespace"></a>diagnostic 名前空間
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

`diagnostics` 名前空間は、コンカレンシー ビジュアライザー マーカーを出力するための機能を提供します。  
  
## <a name="syntax"></a>構文  
  
```  
namespace diagnostic;  
```  
  
## <a name="members"></a>メンバー  
  
### <a name="classes"></a>クラス  
  
|名前|説明|  
|----------|-----------------|  
|[marker_series クラス](../profiling/marker-series-class.md)|1 つのプロバイダーによって生成されたイベントのシリアル チャネルを表します。|  
|[span クラス](../profiling/span-class.md)|アプリケーションのフェーズを定義します。|  
  
### <a name="enumerations"></a>列挙  
  
|名前|説明|  
|----------|-----------------|  
|[marker_importance 列挙型](../profiling/marker-importance-enumeration.md)|コンカレンシー ビジュアライザー マーカーの重要度レベルを表します。|  
  
## <a name="requirements"></a>必要条件  
 **ヘッダー:** cvmarkersobj.h  
  
 **名前空間:** コンカレンシー  
  
## <a name="see-also"></a>参照  
 [コンカレンシー名前空間 (コンカレンシー ビジュアライザー)](../profiling/concurrency-namespace-concurrency-visualizer.md)
