---
title: marker_series クラス | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2016
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- cvmarkersobj/Concurrency::diagnostic::marker_series
helpviewer_keywords:
- Concurrency::diagnostic::marker_series class
ms.assetid: b8445ed0-c512-4f92-b6b4-3d05c044f939
author: mikejo5000
ms.author: mikejo
manager: douge
ms.workload:
- multiple
ms.openlocfilehash: e638d9316b46a8600fe2e88ca5e4a6611fa1ec4d
ms.sourcegitcommit: ce154aee5b403d5c1c41da42302b896ad3cf8d82
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2018
ms.locfileid: "34843836"
---
# <a name="markerseries-class"></a>marker_series クラス
1 つのプロバイダーによって生成されたイベントのシリアル チャネルを表します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
class marker_series;  
```  
  
## <a name="members"></a>メンバー  
  
### <a name="public-constructors"></a>パブリック コンストラクター  
  
|name|説明|  
|----------|-----------------|  
|[marker_series::marker_series コンストラクター](../profiling/marker-series-marker-series-constructor.md)|`marker_series` クラスの新しいインスタンスを初期化します。|  
|[marker_series::~marker_series デストラクター](../profiling/marker-series-tilde-marker-series-destructor.md)|marker_series オブジェクトを破棄し、割り当てられているすべてのリソースを解放します。|  
  
### <a name="public-methods"></a>パブリック メソッド  
  
|name|説明|  
|----------|-----------------|  
|[marker_series::is_enabled メソッド](../profiling/marker-series-is-enabled-method.md)|任意のセッションでプロバイダーが有効にされているかどうかを調べます。|  
|[marker_series::write_alert メソッド](../profiling/marker-series-write-alert-method.md)|同時実行ビジュアライザーのトレース ファイルにアラートを書き込みます。|  
|[marker_series::write_flag メソッド](../profiling/marker-series-write-flag-method.md)|同時実行ビジュアライザーのトレース ファイルにフラグを書き込みます。|  
|[marker_series::write_message メソッド](../profiling/marker-series-write-message-method.md)|同時実行ビジュアライザーのトレース ファイルにメッセージを書き込みます。|  
  
## <a name="inheritance-hierarchy"></a>継承階層  
 `marker_series`  
  
## <a name="requirements"></a>必要条件  
 **ヘッダー:** *cvmarkersobj.h*  
  
 **名前空間:** Concurrency::diagnostic  
  
## <a name="see-also"></a>関連項目  
 [diagnostic 名前空間](../profiling/diagnostic-namespace.md)