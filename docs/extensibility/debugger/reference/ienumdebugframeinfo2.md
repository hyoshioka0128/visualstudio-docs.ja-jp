---
title: IEnumDebugFrameInfo2 |Microsoft ドキュメント
ms.custom: ''
ms.date: 11/04/2016
ms.technology:
- vs-ide-sdk
ms.topic: conceptual
f1_keywords:
- IEnumDebugFrameInfo2
helpviewer_keywords:
- IEnumDebugFrameInfo2
ms.assetid: 994e30ad-435a-4f9e-9272-d96d9e01099c
author: gregvanl
ms.author: gregvanl
manager: douge
ms.workload:
- vssdk
ms.openlocfilehash: 858250c3c951880cf905ea6ee150f1ff61008204
ms.sourcegitcommit: 6a9d5bd75e50947659fd6c837111a6a547884e2a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2018
ms.locfileid: "31123919"
---
# <a name="ienumdebugframeinfo2"></a>IEnumDebugFrameInfo2
このインターフェイスの列挙[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体。  
  
## <a name="syntax"></a>構文  
  
```  
IEnumDebugFrameInfo2 : IUnknown  
```  
  
## <a name="notes-for-implementers"></a>実装についてのメモ  
 デバッグ エンジン (DE) では、現在の呼び出し履歴を表す構造体のリストを提供するには、このインターフェイスを実装します。  
  
## <a name="notes-for-callers"></a>呼び出し元のノート  
 Visual Studio 呼び出し[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)ブレークポイントされるたびにこのインターフェイスを取得するには、例外、または停止が発生したデバッグ中のプログラムです。  
  
## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド  
 次の表は、メソッドの`IEnumDebugFrameInfo2`します。  
  
|メソッド|説明|  
|------------|-----------------|  
|[次へ](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)|指定した数を取得[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)列挙のシーケンス内の構造体。|  
|[Skip](../../../extensibility/debugger/reference/ienumdebugframeinfo2-skip.md)|指定した数のスキップ[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)列挙のシーケンス内の構造体。|  
|[リセット](../../../extensibility/debugger/reference/ienumdebugframeinfo2-reset.md)|列挙のシーケンスを先頭にリセットします。|  
|[複製](../../../extensibility/debugger/reference/ienumdebugframeinfo2-clone.md)|現在の列挙子と同じ列挙の状態を含む列挙子を作成します。|  
|[GetCount](../../../extensibility/debugger/reference/ienumdebugframeinfo2-getcount.md)|数を取得[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体、列挙子にします。|  
  
## <a name="remarks"></a>コメント  
 Visual Studio は、ブレークポイント、例外、またはデバッグ中のプログラム上のユーザーによって生成された一時停止を処理する最初の手順として、このインターフェイスを取得します。 一連の[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体は、現在の呼び出し履歴を表すの一覧と、最も古い関数の先頭に現在の関数呼び出しで、リストの末尾に呼び出します。 各`FRAMEINFO`コンテキストの式を評価し、ローカル変数を調べるスタック フレームを表します。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg.h  
  
 Namespace: Microsoft.VisualStudio.Debugger.Interop  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>関連項目  
 [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)   
 [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)   
 [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)