---
description: このプログラムのホストプロセスのタイトル、フレンドリ名、またはファイル名を取得します。
title: 'IDebugProgramHost2:: GetHostName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramHost2::GetHostName
helpviewer_keywords:
- IDebugProgramHost2::GetHostName
ms.assetid: 48bbb089-e59a-471a-9965-24b42a8dabf3
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4574bee7fb5a7f3ed125a73361de6fc9c3bcbfc2
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102149523"
---
# <a name="idebugprogramhost2gethostname"></a>IDebugProgramHost2::GetHostName
このプログラムのホストプロセスのタイトル、フレンドリ名、またはファイル名を取得します。

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
から [GETHOSTNAME_TYPE](../../../extensibility/debugger/reference/gethostname-type.md) 列挙体の値。

`pbstrHostName`\
入出力要求されたホストプロセスの名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドの一般的な実装では、 `dwType` パラメーターは無視され、ホストコンピューターのフレンドリ名が返されます。 もう1つの実装として、 `dwType` [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md) メソッドへの呼び出しにパラメーターを渡して、名前を取得することもできます。

## <a name="see-also"></a>関連項目
- [IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)
- [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
