---
title: 'IDebugProcess2:: EnumPrograms |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess2::EnumPrograms
helpviewer_keywords:
- IDebugProcess2::EnumPrograms
ms.assetid: f5b7295d-487d-464f-a4c6-d54175b07705
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 56b1c939802406394bdf09e3cfa8c76f5103d974
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80724090"
---
# <a name="idebugprocess2enumprograms"></a>IDebugProcess2::EnumPrograms
このプロセスに含まれるすべてのプログラムの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumPrograms( 
   IEnumDebugPrograms2** ppEnum
);
```

```csharp
int EnumPrograms( 
   out IEnumDebugPrograms2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力プロセス内のすべてのプログラムの一覧を含む [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugProcess2](../../../extensibility/debugger/reference/idebugprocess2.md)
- [IEnumDebugPrograms2](../../../extensibility/debugger/reference/ienumdebugprograms2.md)
