---
title: プログラム2::終了 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::Terminate
helpviewer_keywords:
- IDebugProgram2::Terminate
ms.assetid: 4d3127d3-b1e9-4b28-ac22-2f2eea255f86
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 913c90e34e308ce5bb4ceecface739afc8d03f3d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722748"
---
# <a name="idebugprogram2terminate"></a>IDebugProgram2::Terminate
プログラムを終了します。

## <a name="syntax"></a>構文

```cpp
HRESULT Terminate( 
   void 
);
```

```csharp
int Terminate();
```

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 可能な場合、プログラムは終了され、プロセスからアンロードされます。それ以外の場合、デバッグ エンジン (DE) は必要なクリーンアップを実行します。

 このメソッドまたは[Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)メソッドは、通常、すべてのデバッグを停止するユーザーに応答して、IDE によって呼び出されます。 このメソッドの実装は、理想的には、プロセス内のプログラムを終了する必要があります。 これが不可能な場合、DE は、このプロセスでプログラムが実行されないようにする必要があります (必要なクリーンアップを行います)。 メソッドが`IDebugProcess2::Terminate`IDE によって呼び出された場合、`IDebugProgram2::Terminate`メソッドが呼び出された後、プロセス全体が終了します。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [Terminate](../../../extensibility/debugger/reference/idebugprocess2-terminate.md)
