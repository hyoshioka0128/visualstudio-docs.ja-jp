---
title: IActiveScriptParse32 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c39c14aa-beb7-4eca-8b8c-2181da1c2e3e
caps.latest.revision: 6
author: mikejo5000
ms.author: mikejo
ms.openlocfilehash: 568feacfe75de22a330c892a44fa4f4f6fd0e3b8
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835317"
---
# <a name="iactivescriptparse32"></a>IActiveScriptParse32
Windows スクリプトエンジンで、スクリプトに未加工のテキストコードのスクリプトを追加したり、実行時に式のテキストを評価したりできるようにするには、インターフェイスを実装し `IActiveScriptParse32` ます。 VBScript など、独立した作成環境を持たない解釈されたスクリプト言語では、 `IPersist*` スクリプトコードをスクリプトエンジンに取り込み、さまざまなオブジェクトイベントにスクリプトフラグメントをアタッチするための代替メカニズム (以外) が用意されています。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
  
|メソッド|説明|  
|------------|-----------------|  
|[IActiveScriptParse32::AddScriptlet](../../winscript/reference/iactivescriptparse32-addscriptlet.md)|スクリプトにコードレットを追加します。|  
|[IActiveScriptParse32::InitNew](../../winscript/reference/iactivescriptparse32-initnew.md)|スクリプトエンジンを初期化します。|  
|[IActiveScriptParse32::ParseScriptText](../../winscript/reference/iactivescriptparse32-parsescripttext.md)|指定されたコードレットを解析し、名前空間に宣言を追加し、必要に応じてコードを評価します。|