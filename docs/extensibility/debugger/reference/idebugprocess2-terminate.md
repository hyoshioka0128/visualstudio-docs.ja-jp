---
description: プロセスを終了します。
title: 'IDebugProcess2:: Terminate |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::Terminate
helpviewer_keywords:
- IDebugProcess2::Terminate
ms.assetid: 5e6bf373-0fe9-4321-b04a-473a65f664d9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9e26a4486e9c97638d20f9c634b66183824c2b39
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105081647"
---
# <a name="idebugprocess2terminate"></a>IDebugProcess2::Terminate
プロセスを終了します。

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
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 プロセスが終了すると、そのプロセス内のすべてのプログラムが終了します。これ以上コードを実行することはできません。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
