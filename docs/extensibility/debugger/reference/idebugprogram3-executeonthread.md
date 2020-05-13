---
title: Iデバッグプログラム3::スレッドを実行する |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722663"
---
# <a name="idebugprogram3executeonthread"></a>IDebugProgram3::ExecuteOnThread
デバッガ プログラムを実行します。 プログラムの実行時に、ユーザーが表示しているスレッドに関する情報をデバッガーに提供するために、スレッドが返されます。

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
[in]オブジェクト[。](../../../extensibility/debugger/reference/idebugthread2.md)

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 デバッガーが停止した後に実行を再開する方法は 3 つあります。

- 実行: 前のステップをキャンセルし、次のブレークポイントまで実行します。

- ステップ: 古いステップをキャンセルし、新しいステップが完了するまで実行します。

- 続行: 再度実行し、古いステップをアクティブのままにします。

  渡される`ExecuteOnThread`スレッドは、どのステップをキャンセルするかを決定する際に役立ちます。 スレッドがわからない場合は、実行するとすべてのステップがキャンセルされます。 スレッドの知識がある場合、アクティブなスレッドのステップをキャンセルするだけで済みます。

## <a name="see-also"></a>関連項目
- [実行](../../../extensibility/debugger/reference/idebugprogram2-execute.md)
- [IDebugProgram3](../../../extensibility/debugger/reference/idebugprogram3.md)
