---
title: AddMessage | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 102a0404-a00c-4566-93f3-01bc8df63280
caps.latest.revision: 8
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: f01d4e80c3740ae27b5df8badbc74989c2da2c60
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68156514"
---
# <a name="addmessage"></a>AddMessage
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

グラフィックス診断の *HUD* (ヘッドアップ ディスプレイ) にカスタム メッセージを追加します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void AddMessage(  
  wchar_t const * szMessage  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `szMessage`  
 HUD に追加するメッセージ。  
  
## <a name="remarks"></a>Remarks  
 グラフィックス診断の HUD は、グラフィック診断で実行されているアプリケーションの左上隅に表示されます。 これには、アプリケーションとグラフィックス情報キャプチャのランタイム情報、およびこの関数の呼び出しによって追加されたメッセージが表示されます。  
  
 HUD にメッセージを追加するには、アクティブにグラフィックス情報をキャプチャする必要はありません。メッセージは、`VsgDbg` クラスのインスタンスを使用して追加できますが、[Init](../debugger/init.md) メンバー関数は最初に呼び出されません。 メッセージは HUD に表示されるだけで、グラフィックのログ ファイルには記録されません。
