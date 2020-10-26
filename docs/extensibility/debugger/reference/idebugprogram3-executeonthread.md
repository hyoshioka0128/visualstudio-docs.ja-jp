---
title: 'IDebugProgram3:: ExecuteOnThread |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugProgram3::ExecuteOnThread
ms.assetid: 2f5211e3-7a3f-47bf-9595-dfc8b4895d0d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 201c08352bc5b616298349c52197529ef3f1a7d2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722663"
---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
デバッガープログラムを実行します。 スレッドは、プログラムの実行時にユーザーが表示しているスレッドについてデバッガー情報を提供するために返されます。

## <a name="syntax"></a>構文

```cpp
HRESULT ExecuteOnThread(
   [in] IDebugThread2* pThread)
```

```csharp
int ExecuteOnThread(
   IDebugThread2 pThread
);
```

## <a name="parameters"></a>パラメーター
`pThread`\
から [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md) オブジェクトです。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 デバッガーが停止した後に実行を再開するには、次の3つの方法があります。

- Execute: 前の手順をキャンセルし、次のブレークポイントまで実行します。

- ステップ: 前の手順をキャンセルし、新しい手順が完了するまで実行します。

- 続行: をもう一度実行し、古いステップをアクティブのままにします。

  に渡されるスレッド `ExecuteOnThread` は、キャンセルするステップを決定するときに役立ちます。 スレッドがわからない場合は、execute を実行すると、すべてのステップが取り消されます。 スレッドに関する知識があれば、アクティブスレッドでの手順をキャンセルするだけでよいのです。

## <a name="see-also"></a>関連項目
- [実行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)
- [IDebugProgram3](../../../extensibility/debugger/reference/idebugprogram3.md)
