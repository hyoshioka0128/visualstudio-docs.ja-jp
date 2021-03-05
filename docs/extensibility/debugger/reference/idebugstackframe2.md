---
description: このインターフェイスは、特定のスレッドのコールスタック内の1つのスタックフレームを表します。
title: IDebugStackFrame2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame2
helpviewer_keywords:
- IDebugStackFrame2 interface
ms.assetid: bd212a6a-dcc6-4756-a77a-e8dfda38b104
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b5ec53e89afb43187c641058620df53c4a61d6cc
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102145912"
---
# <a name="idebugstackframe2"></a>IDebugStackFrame2
このインターフェイスは、特定のスレッドのコールスタック内の1つのスタックフレームを表します。

## <a name="syntax"></a>構文

```
IDebugStackFrame2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、このインターフェイスを実装してスタックフレームを表します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IEnumDebugFrameInfo2](../../../extensibility/debugger/reference/ienumdebugframeinfo2.md)インターフェイスを取得するには、 [enumフレーム情報](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)を呼び出します。 インターフェイスを含む[フレーム情報](../../../extensibility/debugger/reference/frameinfo.md)構造体を取得するには、 [[次へ](../../../extensibility/debugger/reference/ienumdebugframeinfo2-next.md)] を呼び出し `IDebugStackFrame2` ます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugStackFrame2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetCodeContext](../../../extensibility/debugger/reference/idebugstackframe2-getcodecontext.md)|このスタックフレームのコードコンテキストを取得します。|
|[GetDocumentContext](../../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)|このスタックフレームのドキュメントコンテキストを取得します。|
|[GetName](../../../extensibility/debugger/reference/idebugstackframe2-getname.md)|スタックフレームの名前を取得します。|
|[GetInfo](../../../extensibility/debugger/reference/idebugstackframe2-getinfo.md)|スタックフレームの説明を取得します。|
|[GetPhysicalStackRange](../../../extensibility/debugger/reference/idebugstackframe2-getphysicalstackrange.md)|スタックフレームに関連付けられている物理アドレスの範囲のコンピューターに依存する表現を取得します。|
|[GetExpressionContext](../../../extensibility/debugger/reference/idebugstackframe2-getexpressioncontext.md)|スタックフレームとスレッドの現在のコンテキスト内で式の評価を実行するための評価コンテキストを取得します。|
|[GetLanguageInfo](../../../extensibility/debugger/reference/idebugstackframe2-getlanguageinfo.md)|スタックフレームに関連付けられている言語を取得します。|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugstackframe2-getdebugproperty.md)|スタックフレームに関連付けられたプロパティの説明を取得します。|
|[EnumProperties](../../../extensibility/debugger/reference/idebugstackframe2-enumproperties.md)|スタックフレームのプロパティの列挙子を作成します。|
|[GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)|スタックフレームに関連付けられているスレッドを取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、デバッグ中のプログラムがブレークポイントで停止された場合にのみ取得されます (ユーザー設定のブレークポイントまたは例外によって発生します)。 このインターフェイスから式のコンテキストを取得して、式を評価したり、レジスタの一覧を返したり、呼び出し履歴を取得して検査したりすることができます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
