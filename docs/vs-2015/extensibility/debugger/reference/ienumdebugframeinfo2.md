---
title: IEnumDebugFrameInfo2 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IEnumDebugFrameInfo2
helpviewer_keywords:
- IEnumDebugFrameInfo2
ms.assetid: 994e30ad-435a-4f9e-9272-d96d9e01099c
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6cc6a0ff332fd6feac72ce4abf38b5319e63c913
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68161013"
---
# <a name="ienumdebugframeinfo2"></a>IEnumDebugFrameInfo2
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このインターフェイスは、 [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md) 構造体を列挙します。  
  
## <a name="syntax"></a>Syntax  
  
```  
IEnumDebugFrameInfo2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装側の注意  
 デバッグエンジン (DE) は、現在の呼び出し履歴を記述する構造体の一覧を提供するために、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元に関する注意事項  
 Visual Studio は、デバッグ中のプログラムでブレークポイント、例外、または停止が発生するたびに、このインターフェイスを取得するために [Enumフレーム情報](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) を呼び出します。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表に、のメソッドを示し `IEnumDebugFrameInfo2` ます。  
  
|メソッド|説明|  
|------------|-----------------|  
|[次へ](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)|列挙シーケンス内の指定された数の [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md) 構造体を取得します。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugframeinfo2-skip.md)|列挙シーケンス内の指定された数の [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md) 構造体をスキップします。|  
|[リセット](../../../extensibility/debugger/reference/ienumdebugframeinfo2-reset.md)|列挙シーケンスを先頭にリセットします。|  
|[複製](../../../extensibility/debugger/reference/ienumdebugframeinfo2-clone.md)|現在の列挙子と同じ列挙状態を含む列挙子を作成します。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)|列挙子内の [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md) 構造体の数を取得します。|  
  
## <a name="remarks"></a>注釈  
 このインターフェイスは、デバッグ中のプログラムでブレークポイント、例外、またはユーザーによって生成される一時停止を処理する最初の手順として、Visual Studio によって取得されます。 [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md)構造体の一覧は現在の呼び出し履歴を表し、現在の関数呼び出しはリストの先頭に、最も古い関数呼び出しはリストの末尾にあります。 各は `FRAMEINFO` スタックフレームを表します。これは、式を評価し、ローカル変数を調べることができるコンテキストです。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [Enumフレーム情報](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)   
 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
