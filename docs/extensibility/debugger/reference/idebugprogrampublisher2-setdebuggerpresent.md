---
title: プログラムプログラムパブリッシャー2:::デバッガの存在マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::SetDebuggerPresent
helpviewer_keywords:
- IDebugProgramPublisher2::SetDebuggerPresent
ms.assetid: c88c3ff4-3632-4199-b5de-83c6d21bcf75
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b551c644346b66d907fa4f75b11b24c8b9538e27
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80721603"
---
# <a name="idebugprogrampublisher2setdebuggerpresent"></a>IDebugProgramPublisher2::SetDebuggerPresent
デバッガーが存在し、実行中であることをプログラムの発行元に通知します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetDebuggerPresent(
   BOOL fDebuggerPresent
);
```

```csharp
int SetDebuggerPresent(
   int fDebuggerPresent
);
```

## <a name="parameters"></a>パラメーター
`fDebuggerPresent`\
[in]デバッガーが存在する`TRUE`場合はゼロ以外 ( )`FALSE`、 存在しない場合は 0 ( ) を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 デバッガーの有無は[、GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)メソッドから返されるデータに反映されます。 `SetDebuggerPresent`

## <a name="see-also"></a>関連項目
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [GetProviderProcessData](../../../extensibility/debugger/reference/idebugprogramprovider2-getproviderprocessdata.md)
