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
ms.openlocfilehash: 16d432b6c150b53fdd059a48cc683d240bd1a50a
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835304"
---
# <a name="iactivescriptparseprocedure32"></a>IActiveScriptParseProcedure32
Windows スクリプトエンジンで、プロシージャのソースコードテキストをスクリプトに追加することが許可されている場合は、インターフェイスが実装され `IActiveScriptParseProcedure32` ます。 VBScript など、独立した作成環境を持たない解釈されたスクリプト言語で `IActiveScriptParse32` は、 `IPersist` スクリプトプロシージャを名前空間に追加するための代替メカニズム (または * 以外) が用意されています。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
  
|||  
|-|-|  
|メソッド|説明|  
|[IActiveScriptParseProcedure32::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure32-parseproceduretext.md)|指定されたコードプロシージャを解析し、プロシージャを名前空間に追加します。|  
  
## <a name="see-also"></a>関連項目  
 [アクティブ スクリプト インターフェイス](../../winscript/reference/active-script-interfaces.md)