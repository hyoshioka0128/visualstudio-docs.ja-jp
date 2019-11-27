---
title: APPBREAKFLAGS 列挙型 |Microsoft Docs
ms.custom: ''
ms.date: 01/18/2017
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- APPBREAKFLAGS
apilocation:
- scrobj.dll
helpviewer_keywords:
- APPBREAKFLAGS constants
ms.assetid: ea8ed80f-2ddb-4800-bb3b-52b76ba6c7a0
caps.latest.revision: 9
author: mikejo5000
ms.author: mikejo
manager: ghogen
ms.openlocfilehash: de6efbc20843fcaa73965334c18cf0e5c2a0abab
ms.sourcegitcommit: 184e2ff0ff514fb980724fa4b51e0cda753d4c6e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72572661"
---
# <a name="appbreakflags-enumeration"></a>APPBREAKFLAGS 列挙型
アプリケーションおよびスレッドの現在のデバッグ状態を示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
enum enum_APPBREAKFLAGS{APPBREAKFLAG_DEBUGGER_BLOCK= 0x00000001,APPBREAKFLAG_DEBUGGER_HALT= 0x00000002,APPBREAKFLAG_STEP= 0x00010000,APPBREAKFLAG_NESTED= 0x00020000,APPBREAKFLAG_STEPTYPE_SOURCE= 0x00000000,APPBREAKFLAG_STEPTYPE_BYTECODE= 0x00100000,APPBREAKFLAG_STEPTYPE_MACHINE= 0x00200000,APPBREAKFLAG_STEPTYPE_MASK= 0x00F00000,APPBREAKFLAG_IN_BREAKPOINT= 0x80000000};  
```  
  
## <a name="members"></a>メンバー  
  
|メンバー|値|説明|  
|------------|-----------|-----------------|  
|APPBREAKFLAG_DEBUGGER_BLOCK|0x00000001|言語エンジンは、BREAKREASON_DEBUGGER_BLOCK を持つすべてのスレッドですぐに中断する必要があります。|  
|APPBREAKFLAG_DEBUGGER_HALT|0x00000002|言語エンジンは、BREAKREASON_DEBUGGER_HALT ですぐに中断する必要があります。|  
|APPBREAKFLAG_STEP|0x00010000|言語エンジンは、BREAKREASON_STEP を使用して、ステップ実行スレッドですぐに中断する必要があります。|  
|APPBREAKFLAG_NESTED|0x00020000|アプリケーションは、ブレークポイントで入れ子になって実行されています。|  
|APPBREAKFLAG_STEPTYPE_SOURCE|0x00000000|デバッガーは、ソースレベルでステップ実行しています。|  
|APPBREAKFLAG_STEPTYPE_BYTECODE|0x00100000|デバッガーは、バイトコードレベルでステップ実行しています。|  
|APPBREAKFLAG_STEPTYPE_MACHINE|0x00200000|デバッガーはコンピューターレベルでステップ実行しています。|  
|APPBREAKFLAG_STEPTYPE_MASK|0x00F00000|ステップの種類をファクタリングするマスク。|  
|APPBREAKFLAG_IN_BREAKPOINT|0x80000000|ブレークポイントが進行中です。|  
  
## <a name="remarks"></a>コメント  
 フラグによっては、次の機会に言語エンジンを中断するように指定し、他のフラグはデバッガーのステップ実行モードを指定します。  
  
## <a name="see-also"></a>参照  
 [アクティブスクリプトデバッガーの定数、列挙型、および構造体](../../winscript/reference/active-script-debugger-constants-enumerations-and-structures.md)   
 [BREAKREASON 列挙型](../../winscript/reference/breakreason-enumeration.md)