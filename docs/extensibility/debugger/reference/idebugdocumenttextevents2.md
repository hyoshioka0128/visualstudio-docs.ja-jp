---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentTextEvents2
helpviewer_keywords:
- IDebugDocumentTextEvents2 interface
ms.assetid: a10cbb6b-11a8-4056-b42a-2ecebf0e690d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 44a1736890ac78e7aaf20b4a639b1794fc63b5ac
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80731369"
---
# <a name="idebugdocumenttextevents2"></a>IDebugDocumentTextEvents2
このインターフェイスは、デバッグ エンジンによって提供されるソース ドキュメントへの変更について Visual Studio に通知するために使用されます。

## <a name="syntax"></a>構文

```
IDebugDocumentTextEvents2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デは、ソース コードへの変更をサポートするために、このインターフェイスを実装します。 このインターフェイスは、通常[、IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)インターフェイスを実装する同じオブジェクトに実装されます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [!INCLUDE[vsprvs](../../../code-quality/includes/vsprvs_md.md)]メソッドの呼び出しを通じて<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint.Advise%2A>このインターフェイスを取得します。 インターフェイス<xref:System.Runtime.InteropServices.ComTypes.IConnectionPoint>はメソッドの呼び出しから<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer.EnumConnectionPoints%2A>取得されます。 インターフェイス<xref:System.Runtime.InteropServices.ComTypes.IConnectionPointContainer>は[、IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md) [インターフェイスでクエリ インターフェイス](/cpp/atl/queryinterface)メソッドを呼び出すことによって取得されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugDocumentTextEvents2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[破壊する](../../../extensibility/debugger/reference/idebugdocumenttextevents2-ondestroy.md)|文書全体が破棄されたことを示します。|
|[onInsertText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-oninserttext.md)|テキストがドキュメントに挿入されたことをデバッグ パッケージに通知します。|
|[onRemoveText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onremovetext.md)|テキストがドキュメントから削除されたことをデバッグ パッケージに通知します。|
|[onReplaceText](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onreplacetext.md)|ドキュメント内でテキストが置き換えられたことをデバッグ パッケージに通知します。|
|[onUpdateTextAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatetextattributes.md)|ドキュメント内でテキスト属性が更新されたことをデバッグ パッケージに通知します。|
|[onUpdateDocumentAttributes](../../../extensibility/debugger/reference/idebugdocumenttextevents2-onupdatedocumentattributes.md)|ドキュメント属性が更新されたことをイベントの受信者に通知します。|

## <a name="remarks"></a>Remarks
 独自のドキュメントを提供するデバッグ エンジンのみがインターフェイスを`IDebugDocumentTextEvent2`利用します。 この例としては、スクリプトデバッグエンジンがあります。 スクリプトの解釈プロセスでは、ディスク ファイルに存在せず、DE にのみ認識される新しいソース コードを生成できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
- [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)
