---
title: Windows スクリプト ホスト | Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- Windows Script Host, implementing hosts
ms.assetid: 9d5f6471-b318-40f3-be01-d9cd0b1cdd47
caps.latest.revision: 7
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: 51053dec1f8362aa9eef80e4867d2f92a06454cb
ms.sourcegitcommit: 9a9c61ca115c22d33bb902153eb0853789c7be4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85835330"
---
# <a name="windows-script-hosts"></a>Windows スクリプト ホスト
Microsoft Windows スクリプト ホストを実装する場合、スクリプト エンジンは、ホストが以下を実行する限り、基本スレッドのコンテキスト内でのみ [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) インターフェイスを呼び出すと想定して問題ありません。  
  
- 基本スレッド (一般にメッセージ ループを含むスレッド) を選択する。  
  
- 基本スレッドでスクリプト エンジンをインスタンス化する。  
  
- [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) と [IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) の場合のように、基本スレッドからのみスクリプト エンジン メソッドを呼び出す (ただし、特別に許可されている場合を除く)。  
  
- 基本スレッドからのみ、スクリプト エンジンのディスパッチ オブジェクトを呼び出す。  
  
- ウィンドウ ハンドルが提供されている場合は、基本スレッドでメッセージ ループが実行されるようにする。  
  
- ホストのオブジェクト モデルのオブジェクトのみが基本スレッドにイベントを提供するようにする。  
  
  すべてのシングル スレッド ホストはこれらの規則に自動的に従うことになります。 上記の制限モデルには、ホストが別のスレッドから [IActiveScript::InterruptScriptThread](../winscript/reference/iactivescript-interruptscriptthread.md) を呼び出してスタック スクリプトを中止するか、[IActiveScript::Clone](../winscript/reference/iactivescript-clone.md) を使用して新しいスレッドでスクリプトを複製できるように意図的に柔軟性を持たせています。  
  
## <a name="remarks"></a>Remarks  
 これらの制限のいずれも、フリー スレッドの [IActiveScriptSite](../winscript/reference/iactivescriptsite.md) インターフェイスやフリー スレッドのオブジェクト モデルを実装することを選択したホストには適用されません。 このようなホストは、任意のスレッドから [IActiveScript](../winscript/reference/iactivescript.md) インターフェイスを制限なく使用できます。  
  
## <a name="see-also"></a>関連項目  
 [Windows スクリプト インターフェイス](../winscript/windows-script-interfaces.md)