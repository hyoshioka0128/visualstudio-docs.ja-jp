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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 53b4d69be1ea24f5c240b6247539f499c9fb00fb
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084013"
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

## <a name="see-also"></a>こちらもご覧ください
- [IDebugProgramHost2](../../../extensibility/debugger/reference/idebugprogramhost2.md)
- [GetHostName](../../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)
