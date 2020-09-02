---
title: BP_FLAGS90 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- BP_FLAGS90 enumeration
ms.assetid: 3e5a06c5-fb30-4b8a-b2d5-4a0570fc80bd
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 9f7192eb7b2fa6d8bc886c0e601788ecba8eebcd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153500"
---
# <a name="bp_flags90"></a>BP_FLAGS90
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

オプションフラグの有効な値を列挙します。 ブレークポイントを設定するときに、省略可能なフラグを使用して追加情報を指定できます。 この列挙体は [BP_FLAGS](../../../extensibility/debugger/reference/bp-flags.md) 列挙体を拡張します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_BP_FLAGS90  
{  
   // VS 8.0 values  
   BP90_FLAG_NONE               = 0x0000,  
   BP90_FLAG_MAP_DOCPOSITION    = 0x0001,  
   BP90_FLAG_DONT_STOP          = 0x0002,  
  
   // Values added in VS 9.0  
   BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,  
};  
typedef DWORD BP_FLAGS90;  
```  
  
```csharp  
public enum enum_BP_FLAGS90  
{  
   // VS 8.0 values  
   BP90_FLAG_NONE                = 0x0000,  
   BP90_FLAG_MAP_DOCPOSITION     = 0x0001,  
   BP90_FLAG_DONT_STOP           = 0x0002,  
  
   // Values added in VS 9.0  
   BP90_FLAG_TRACEPOINT_CONTINUE = 0x0004,  
};  
```  
  
#### <a name="parameters"></a>パラメーター  
 BP90_FLAG_NONE  
 ブレークポイントフラグを指定しません。  
  
 BP90_FLAG_MAP_DOCPOSITION  
 デバッグエンジン (DE) がドキュメントの位置を使用してブレークポイントをマップすることを指定します。 これは、Active Server ページ (ASP) などのスクリプト指向のソースファイルに設定されているブレークポイントにのみ適用できます。  
  
 BP90_FLAG_DONT_STOP  
 ブレークポイントがデバッグエンジンによって処理される必要があることを指定しますが、最終的にはデバッグエンジンがそこで停止しないように指定します。つまり、 [IDebugBreakpointEvent2](../../../extensibility/debugger/reference/idebugbreakpointevent2.md) イベントオブジェクトを送信することはできません。 このフラグは、主にトレースポイントで使用されるように設計されています。  
  
 BP90_FLAG_TRACEPOINT_CONTINUE  
 ステップ実行状態をクリアする必要があるかどうかを判断するために、ネイティブデバッグエンジンによって使用されます。 トレースポイントがマクロを実行する場合は BP90_FLAG_DONT_STOP が設定されないため、BP90_FLAG_DONT_STOP とは異なります。  
  
## <a name="requirements"></a>要件  
 ヘッダー: Msdbg90  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
