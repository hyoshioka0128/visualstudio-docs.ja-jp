---
title: サーバーを作成します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCoreServer3::CreateInstanceInServer
helpviewer_keywords:
- IDebugCoreServer3::CreateInstanceInServer
ms.assetid: 76f36bae-f6ab-413c-a8a9-8808bfeba05b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2346bb76fe604265a309a51f48b734fc6f2ab8d0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80733027"
---
# <a name="idebugcoreserver3createinstanceinserver"></a>IDebugCoreServer3::CreateInstanceInServer
サーバー上にデバッグ エンジンのインスタンスを作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT CreateInstanceInServer(
   LPCWSTR  szDll,
   WORD     wLangId,
   REFCLSID clsidObject,
   REFIID   riid,
   void**   ppvObject
);
```

```csharp
int CreateInstanceInServer(
   string     szDll,
   ushort     wLangID,
   ref Guid   clsidObject,
   ref Guid   riid,
   out IntPtr ppvObject
);
```

## <a name="parameters"></a>パラメーター
`szDll`\
[in]`clsidObject`パラメータで指定された CLSID を実装する dll へのパス。 が 場合`NULL`は、COM の`CoCreateInstance`関数が呼び出されます。

`wLangId`\
[in]デバッグ エンジンのロケール。 [SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)メソッドを呼び出さない場合は、0 を指定できます。

`clsidObject`\
[in]作成するデバッグ エンジンの CLSID。

`riid`\
[in]クラス オブジェクトから取得する特定のインターフェイスのインターフェイス ID。

`ppvObject`\
[アウト]`IUnknown`インスタンス化されたオブジェクトからのインターフェイス。 このオブジェクトを目的のインターフェイスにキャストまたはマーシャリングします。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugCoreServer3](../../../extensibility/debugger/reference/idebugcoreserver3.md)
- [SetLocale](../../../extensibility/debugger/reference/idebugengine2-setlocale.md)
