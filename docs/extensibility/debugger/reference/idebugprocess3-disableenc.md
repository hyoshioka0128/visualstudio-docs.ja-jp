---
title: Iデバッグプロセス3::D可能なENC |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProcess3::DisableENC
helpviewer_keywords:
- IDebugProcess3::DisableENC
ms.assetid: cffdbdac-4d76-4aeb-aa55-5d0410db99f1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5b39bb448501bacd5ab458b7e61bb1a5044bc8a3
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723736"
---
# <a name="idebugprocess3disableenc"></a>IDebugProcess3::DisableENC
このメソッドは、このプロセス (およびこのプロセスに含まれるすべてのプログラム) でエディット コンティニュを明示的に無効にします。 カスタム ポートサプライヤーは常に`E_NOTIMPL`を返す必要があります。

## <a name="syntax"></a>構文

```cpp
HRESULT DisableENC(
   EncUnavailableReason reason
);
```

```csharp
   EncUnavailableReason reason
);
```

## <a name="parameters"></a>パラメーター
`reason`\
[in][列挙体](../../../extensibility/debugger/reference/encunavailablereason.md)の値。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

> [!NOTE]
> カスタム ポートサプライヤーは常に`E_NOTIMPL`を返す必要があります。

## <a name="remarks"></a>Remarks
 エディット コンティニュが無効になっているプロセスは、プロセスを再起動することによってのみ再度有効にできます。

## <a name="see-also"></a>関連項目
- [IDebugProcess3](../../../extensibility/debugger/reference/idebugprocess3.md)
- [EncUnavailableReason](../../../extensibility/debugger/reference/encunavailablereason.md)
