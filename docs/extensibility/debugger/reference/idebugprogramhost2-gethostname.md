---
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
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5f1bd63d6b53359cf3b86f5e3849cb18bd8367f7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80722233"
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

## <a name="remarks"></a>注釈
 このメソッドの一般的な実装では、 `dwType` パラメーターは無視され、ホストコンピューターのフレンドリ名が返されます。 もう1つの実装として、 `dwType` [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md) メソッドへの呼び出しにパラメーターを渡して、名前を取得することもできます。

## <a name="see-also"></a>関連項目
- [IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)
- [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
