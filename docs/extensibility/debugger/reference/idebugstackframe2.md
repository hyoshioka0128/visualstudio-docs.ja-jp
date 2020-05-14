---
title: をクリックしてスタックフレーム 2 を実行する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2
helpviewer_keywords:
- IDebugStackFrame2 interface
ms.assetid: bd212a6a-dcc6-4756-a77a-e8dfda38b104
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 37acb9f2984c36130de494108ef4b76a59cc74e7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719517"
---
# <a name="idebugstackframe2"></a>IDebugStackFrame2
このインターフェイスは、特定のスレッドの呼び出し履歴の単一のスタック フレームを表します。

## <a name="syntax"></a>構文

```
IDebugStackFrame2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、スタック フレームを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [インターフェイス](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)を取得するには[、列挙型フレーム情報を](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)呼び出します。 [Next](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)を呼び出して、インターフェイスを含`IDebugStackFrame2`む[FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)構造体を取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugStackFrame2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|このスタック フレームのコード コンテキストを取得します。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|このスタック フレームのドキュメント コンテキストを取得します。|
|[GetName](../../../extensibility/debugger/reference/idebugstackframe2-getname.md)|スタック フレームの名前を取得します。|
|[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)|スタック フレームの説明を取得します。|
|[GetPhysicalStackRange](../../../extensibility/debugger/reference/idebugstackframe2-getphysicalstackrange.md)|スタック フレームに関連付けられた物理アドレスの範囲のコンピューターに依存する表現を取得します。|
|[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)|スタック フレームとスレッドの現在のコンテキスト内で式の評価を行うための評価コンテキストを取得します。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugstackframe2-getlanguageinfo.md)|スタック フレームに関連付けられている言語を取得します。|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)|スタック フレームに関連付けられているプロパティの説明を取得します。|
|[EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)|スタック フレーム プロパティの列挙子を作成します。|
|[GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)|スタック フレームに関連付けられているスレッドを取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、デバッグ中のプログラムがブレークポイント (ユーザー設定のブレークポイントまたは例外によって発生) で停止した場合にのみ取得されます。 このインターフェイスから式コンテキストを取得して式を評価したり、レジスタのリストを返したり、呼び出し履歴を取得して調べたりすることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
