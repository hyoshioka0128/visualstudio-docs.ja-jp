---
title: ホスト名を取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2::GetHostName
helpviewer_keywords:
- IDebugProgramHost2::GetHostName
ms.assetid: 48bbb089-e59a-471a-9965-24b42a8dabf3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5f1bd63d6b53359cf3b86f5e3849cb18bd8367f7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80722233"
---
# <a name="idebugprogramhost2gethostname"></a>IDebugProgramHost2::GetHostName
このプログラムのホスト プロセスのタイトル、フレンドリ名、またはファイル名を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetHostName( 
   DWORD dwType,
   BSTR* pbstrHostName
);
```

```csharp
int GetHostName( 
   uint dwType,
   out string pbstrHostName
);
```

## <a name="parameters"></a>パラメーター
`dwType`\
[in][GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md)列挙体の値。

`pbstrHostName`\
[アウト]ホスト プロセスの要求された名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドの一般的な実装では、`dwType`パラメーターは無視され、ホスト コンピューターのフレンドリ名が返されます。 もう 1 つの実装は`dwType`[、GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)メソッドの呼び出しにパラメーターを渡して名前を取得することです。

## <a name="see-also"></a>関連項目
- [IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)
- [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
