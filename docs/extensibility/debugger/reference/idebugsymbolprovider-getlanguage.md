---
description: このメソッドは、デバッグアドレスでコードをコンパイルするために使用された言語を取得します。
title: 'IDebugSymbolProvider:: GetLanguage |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolProvider::GetLanguage
helpviewer_keywords:
- IDebugSymbolProvider::GetLanguage method
ms.assetid: e4142183-3d8b-418f-907f-4ee4c753d8ce
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 86387e86261a91b77793e9a31ae4b415983e2c5c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168557"
---
# <a name="idebugsymbolprovidergetlanguage"></a>IDebugSymbolProvider::GetLanguage
このメソッドは、デバッグアドレスでコードをコンパイルするために使用された言語を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetLanguage( 
   IDebugAddress* pAddress,
   GUID*          pguidLanguage,
   GUID*          pguidLanguageVendor
);
```

```csharp
int GetLanguage(
   IDebugAddress pAddress,
   out Guid      pguidLanguage,
   out Guid      pguidLanguageVendor
);
```

## <a name="parameters"></a>パラメーター
`pAddress`\
から [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md) インターフェイスによって表されるアドレスオブジェクト。

`pguidLanguage`\
入出力 `GUID` 言語を指定するを返します。

`pguidLanguageVendor`\
入出力 `GUID` 言語のベンダーを指定するを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 デバッグエンジンは、このメソッドを呼び出して、正しい式エバリュエーターを選択するために必要な情報を取得します。

## <a name="see-also"></a>関連項目
- [IDebugSymbolProvider](../../../extensibility/debugger/reference/idebugsymbolprovider.md)
- [IDebugAddress](../../../extensibility/debugger/reference/idebugaddress.md)
