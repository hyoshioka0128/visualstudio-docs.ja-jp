---
description: アプリケーションドメインの識別子を取得します。
title: 'IDebugAlias2:: GetAppDomainId |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetAppDomainId
- IDebugAlias2::GetAppDomainId
ms.assetid: 23581aaa-5a53-4859-b264-eca49fc44bcd
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ee1caec6968f9a67a15a31c8064b7795a37a6829
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105059107"
---
# <a name="idebugalias2getappdomainid"></a>IDebugAlias2::GetAppDomainId
アプリケーションドメインの識別子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAppDomainId (
   ULONG32* pappDomainId
);
```

```csharp
int GetAppDomainId (
   out uint pappDomainId
);
```

## <a name="parameters"></a>パラメーター
`pappDomainId`\
入出力アプリケーションドメイン識別子を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 アプリケーションドメイン識別子は、アプリケーションが再起動され、新しいアプリケーションドメインが作成されるたびに変更されます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)
