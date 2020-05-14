---
title: IDebugEngine3::ロードシンボル |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngine3::LoadSymbols
helpviewer_keywords:
- IDebugEngine3::LoadSymbols
ms.assetid: c846a440-1d91-4d48-b8f1-82e902ae152b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7963d39601a0d3a90ca2daa7632902d7aa506de8
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730805"
---
# <a name="idebugengine3loadsymbols"></a>IDebugEngine3::LoadSymbols
このデバッグ エンジンによってデバッグされるすべてのモジュールのシンボルを (必要に応じて) 読み込みます。

## <a name="syntax"></a>構文

```cpp
HRESULT LoadSymbols();
```

```csharp
int LoadSymbols();
```

## <a name="parameters"></a>パラメーター
 [なし] :

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このデバッグ エンジンによって参照されるすべてのモジュールのデバッグ シンボルを読み込みます。 シンボルは、まだ読み込まれていない場合にのみロードされます。 シンボルは[、SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)の呼び出しによって設定されたパスで検索されます。

## <a name="see-also"></a>関連項目
- [SetSymbolPath](../../../extensibility/debugger/reference/idebugengine3-setsymbolpath.md)
- [IDebugEngine3](../../../extensibility/debugger/reference/idebugengine3.md)
