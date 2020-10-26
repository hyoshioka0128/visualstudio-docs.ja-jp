---
title: UnInit | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
ms.assetid: 4cd4fc0b-974a-4e61-9ea8-0aaa1a0c52ea
caps.latest.revision: 7
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0bec86a7f872057b7a0d652df6346e3a1ef2ff8a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68197930"
---
# <a name="uninit"></a>UnInit
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

グラフィックス ログ ファイルを終了して閉じ、アプリケーションがアクティブにグラフィックス情報を記録したときに使用されたリソースを解放します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
void UnInit();  
```  
  
## <a name="remarks"></a>Remarks  
 `UnInit` は、`VsgDbg` クラスのインスタンスが破棄されるときに自動的に呼び出されます。 `VsgDbg` のインスタンスがグラフィックス情報をアクティブに記録しなかった場合、この操作による影響はありません。  
  
 `UnInit` が `VsgDbg` クラスのインスタンスで呼び出された後、新しいグラフィックス ログ ファイルは `Init` を呼び出して作成でき、`UnInit` を呼び出して終了できます。 この操作を何度でも繰り返して、同じ `VsgDbg` インスタンスを使用して複数の独立したグラフィックス ログ ファイルを作成することができます。  
  
## <a name="see-also"></a>参照  
 [Init](../debugger/init.md)
