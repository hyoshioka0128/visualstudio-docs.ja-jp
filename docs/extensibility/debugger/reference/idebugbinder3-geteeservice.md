---
title: バインダー3::ゲットイーサービス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder3::GetEEService
helpviewer_keywords:
- IDebugBinder3::GetEEService method
ms.assetid: eb07aa40-8cd9-4a52-a4c7-4affd2307a01
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7c08d7df4a6b05be489f6b9ab06569c085f3b1f8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735825"
---
# <a name="idebugbinder3geteeservice"></a>IDebugBinder3::GetEEService
このメソッドは、要求されたサービスを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEEService(
   [in] GUID        vendor,
   [in] GUID        language,
   [in] GUID        iid,
   [out] IUnknown** ppService
);
```

```csharp
Int GetEEService(
   Guid       vendor,
   Guid       language,
   Guid       iid,
   out object ppService
);
```

## <a name="parameters"></a>パラメーター
`vendor`\
[in]`GUID`のベンダー (NULL 値は許容されます)。

`language`\
[in]`GUID`の言語 (NULL 値は許容されます)。

`iid`\
[in]`IID`取得するサービスの。

`ppService`\
[アウト]要求されたサービスへのインターフェイス。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 型ビ`IID`ジュアライザー サービスが使用可能かどうかを確認するには`IID_IEEVisualizerServiceProvider`[、IEEVisualizer サービス プロバイダー](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)インターフェイス ( ) を渡します。 その場合、式エバリュエーターは、型のビジュアライザーをサポートする[IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)インターフェイスを取得できます。 詳細については[、データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)を参照してください。

## <a name="see-also"></a>関連項目
- [IDebugBinder3](../../../extensibility/debugger/reference/idebugbinder3.md)
- [IEEVisualizerServiceProvider](../../../extensibility/debugger/reference/ieevisualizerserviceprovider.md)
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [データの視覚化と表示](../../../extensibility/debugger/visualizing-and-viewing-data.md)
