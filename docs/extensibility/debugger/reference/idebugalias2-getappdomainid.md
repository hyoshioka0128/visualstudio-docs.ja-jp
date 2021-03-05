---
description: アプリケーションドメインの識別子を取得します。
title: 'IDebugAlias2:: GetAppDomainId |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetAppDomainId
- IDebugAlias2::GetAppDomainId
ms.assetid: 23581aaa-5a53-4859-b264-eca49fc44bcd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6f5bd0d6a96ad41409b87433599fe693fc86c1cc
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143871"
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

## <a name="remarks"></a>解説
 アプリケーションドメイン識別子は、アプリケーションが再起動され、新しいアプリケーションドメインが作成されるたびに変更されます。

## <a name="see-also"></a>関連項目
- [IDebugAlias2](../../../extensibility/debugger/reference/idebugalias2.md)
