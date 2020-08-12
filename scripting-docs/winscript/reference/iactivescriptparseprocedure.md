---
title: IActiveScriptParseProcedure |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IActiveScriptParseProcedure interface
ms.assetid: 741a35bb-5b92-489e-ba8a-a406b42125fc
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 3567a22eac2ad270739e62e0f0fb9914bdf4a9ec
ms.sourcegitcommit: d281d2a04a5bc302650eebf369946d8f101e59dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2020
ms.locfileid: "88144572"
---
# <a name="iactivescriptparseprocedure"></a>IActiveScriptParseProcedure
Windows スクリプトエンジンで、プロシージャのソースコードテキストをスクリプトに追加することが許可されている場合は、インターフェイスが実装され `IActiveScriptParseProcedure` ます。 VBScript など、独立した作成環境を持たない解釈されたスクリプト言語で `IActiveScriptParse` は、 `IPersist` スクリプトプロシージャを名前空間に追加するための代替メカニズム (または * 以外) が用意されています。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
  
|Method|説明|
|-|-|
|[IActiveScriptParseProcedure::ParseProcedureText](../../winscript/reference/iactivescriptparseprocedure-parseproceduretext.md)|指定されたコードプロシージャを解析し、プロシージャを名前空間に追加します。|  
  
## <a name="see-also"></a>関連項目  
 [アクティブ スクリプト インターフェイス](../../winscript/reference/active-script-interfaces.md)