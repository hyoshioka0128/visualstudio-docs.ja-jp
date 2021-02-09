---
title: 'IDebugDefaultPort2:: GetServer |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDefaultPort2::GetServer
helpviewer_keywords:
- IDebugDefaultPort2::GetServer
ms.assetid: cacb4b74-0f39-471c-af38-54b73f5b2868
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e046dbad9329ae377cef6864b7bc71b2ea6a538b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99894947"
---
# <a name="idebugdefaultport2getserver"></a>IDebugDefaultPort2::GetServer
このメソッドは、このポートがあるサーバーへのインターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetServer(
   IDebugCoreServer3** ppServer
);
```

```csharp
int GetServer(
   out IDebugCoreServer3 ppServer
);
```

## <a name="parameters"></a>パラメーター
`ppServer`\
入出力 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md) インターフェイスを実装するオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)は Visual Studio によって実装され、ポートが配置されているサーバーを表します。

## <a name="see-also"></a>関連項目
- [IDebugDefaultPort2](../../../extensibility/debugger/reference/idebugdefaultport2.md)
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
