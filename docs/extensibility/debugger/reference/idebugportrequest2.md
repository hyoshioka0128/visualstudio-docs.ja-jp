---
title: をクリックして、ポートリクエスト 2 を実行する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPortRequest2
helpviewer_keywords:
- IDebugPortRequest2 interface
ms.assetid: 556e610d-7c4b-44a8-965a-76a9d02b601a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 163718fda344ba5f3f44ef630b4eba3e5613dc61
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80724788"
---
# <a name="idebugportrequest2"></a>IDebugPortRequest2
このインターフェイスはポートを記述します。 この説明は、ポートサプライヤーにポートを追加するために使用されます。

## <a name="syntax"></a>構文

```
IDebugPortRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 Visual Studio は通常、ポートサプライヤーからデバッグ ポートを取得するプロセスでこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは、デバッグ ポートを作成するために[AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)に渡されます。 [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)の呼び出しは、最初の場所でポートを作成するために使用される要求を表す、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugPortRequest2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetPortName](../../../extensibility/debugger/reference/idebugportrequest2-getportname.md)|作成するポートの名前を取得します。|

## <a name="remarks"></a>Remarks
 通常、デバッグ エンジンはポート サプライヤーと対話せず、このインターフェイスには使用しません。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [AddPort](../../../extensibility/debugger/reference/idebugportsupplier2-addport.md)
- [GetPortRequest](../../../extensibility/debugger/reference/idebugport2-getportrequest.md)
