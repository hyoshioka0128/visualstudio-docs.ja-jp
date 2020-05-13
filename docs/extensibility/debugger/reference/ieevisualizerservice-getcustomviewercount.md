---
title: サービス::カスタムビューアーカウント |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEEVisualizerService::GetCustomViewerCount
helpviewer_keywords:
- IEEVisualizerService::GetCustomViewerCount method
ms.assetid: f7b095c2-e538-4352-8cad-d4c6d4f6bdbc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 90f040c4ca0736a0312829d196d0991788357edc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718041"
---
# <a name="ieevisualizerservicegetcustomviewercount"></a>IEEVisualizerService::GetCustomViewerCount
このメソッドは、このサービスから利用できるビジュアライザーの数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCustomViewerCount(
   ULONG* pcelt
);
```

```csharp
int GetCustomViewerCount(
   out uint pcelt
);
```

## <a name="parameters"></a>パラメーター
`pcelt`\
[アウト]使用可能なビジュアライザーの型の数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
- [型](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)ビジュアライザーのサポートで、このメソッドに要求を渡します。

## <a name="see-also"></a>関連項目
- [IEEVisualizerService](../../../extensibility/debugger/reference/ieevisualizerservice.md)
- [GetCustomViewerCount](../../../extensibility/debugger/reference/idebugproperty3-getcustomviewercount.md)
