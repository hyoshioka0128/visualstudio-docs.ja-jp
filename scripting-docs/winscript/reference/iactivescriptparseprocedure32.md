---
title: IActiveScriptParseProcedure32 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 387a856b-f5dc-4371-8620-bd574e046c2c
caps.latest.revision: 5
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 71a22f422ff04e56a7aaa7a715641d190ade47bf
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144390"
---
# <a name="iactivescriptparseprocedure32"></a>IActiveScriptParseProcedure32
Windows スクリプトエンジンで、プロシージャのソースコードテキストをスクリプトに追加することが許可されている場合は、インターフェイスが実装され `IActiveScriptParseProcedure32` ます。 VBScript など、独立した作成環境を持たない解釈されたスクリプト言語で `IActiveScriptParse32` は、 `IPersist` スクリプトプロシージャを名前空間に追加するための代替メカニズム (または * 以外) が用意されています。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
  
|Method|説明|
|-|-|
|[IActiveScriptParseProcedure32::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure32-parseproceduretext.md)|指定されたコードプロシージャを解析し、プロシージャを名前空間に追加します。|  
  
## <a name="see-also"></a>関連項目  
 [アクティブ スクリプト インターフェイス](../../winscript/reference/active-script-interfaces.md)