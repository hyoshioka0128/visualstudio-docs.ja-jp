---
title: を使用します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2::GetEngineInterface
helpviewer_keywords:
- IDebugQueryEngine2::GetEngineInterface
ms.assetid: ed84aa98-7ec7-48f3-97ae-821090bc3664
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 82f3214783a35e668bf3164c8659f60f863e9a43
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720668"
---
# <a name="idebugqueryengine2getengineinterface"></a>IDebugQueryEngine2::GetEngineInterface
カスタム デバッグ エンジン (DE) インターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEngineInterface( 
   IUnknown** ppUnk
);
```

```csharp
int GetEngineInterface( 
   out object ppUnk
);
```

## <a name="parameters"></a>パラメーター
`ppUnk`\
[アウト]オブジェクトを`IUnknown`返すデバッグ エンジン (DE)、および DE に関連付けられている他の有効なインターフェイス (たとえば[、IDebugEngine2 または IDebugEngineLaunch2)](../../../extensibility/debugger/reference/idebugengine2.md)を照会できます。 [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドから取得したインターフェイスを通じて呼び出すとセッション デバッグ マネージャーの処理が回避され、SDM が無効な状態に陥ったり、デバッグ中にエラーが発生したりする可能性があるため、生成されるインターフェイスは注意して使用する必要があります。

## <a name="see-also"></a>関連項目
- [IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
