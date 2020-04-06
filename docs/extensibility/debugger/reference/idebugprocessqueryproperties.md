---
title: クエリプロパティ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProcessQueryProperties
ms.assetid: ce29a248-81a0-42c0-99a7-1606e8c548ec
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 08abf401b4e8f0e7a33d882e8178d77e6f248318
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723277"
---
# <a name="idebugprocessqueryproperties"></a>IDebugProcessQueryProperties
このインターフェイスは[、IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)の実装によって実装される拡張機能インターフェイスです。 この機能により、実装者はデバッグプロセス環境に関する情報を取得できます。

## <a name="syntax"></a>構文

```
IDebugProcessQueryProperties: IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ プロセスの実行環境に関する情報を取得するには、このインターフェイスを実装します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugProcessQueryProperties`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[QueryProperty](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperty.md)|プロパティ値を照会します。|
|[QueryProperties](../../../extensibility/debugger/reference/idebugprocessqueryproperties-queryproperties.md)|プロパティ値のクエリ。|

## <a name="remarks"></a>Remarks
 このインターフェイスはめったに実装されません。

## <a name="requirements"></a>必要条件
 ヘッダー: ポートプリフ.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
