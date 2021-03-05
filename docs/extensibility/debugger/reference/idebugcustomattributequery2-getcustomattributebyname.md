---
description: カスタム属性の名前を指定して、カスタム属性のバイトを取得します。
title: 'IDebugCustomAttributeQuery2:: GetCustomAttributeByName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
helpviewer_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
ms.assetid: 7428dfeb-8929-41b2-9b99-cb343a86c02d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8c65abff050af7b7c34161cbca2594431cb119b5
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150082"
---
# <a name="idebugcustomattributequery2getcustomattributebyname"></a>IDebugCustomAttributeQuery2::GetCustomAttributeByName
カスタム属性の名前を指定して、カスタム属性のバイトを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCustomAttributeByName( 
   LPCOLESTR pszCustomAttributeName,
   BYTE*     ppBlob,
   DWORD*    pdwLen
);
```

```csharp
int GetCustomAttributeByName(
   [In] string        pszCustomAttributeName,
   [In, Out] byte[]   ppBlob,
   [In, Out] ref uint pdwLen
);
```

## <a name="parameters"></a>パラメーター
`pszCustomAttributeName`\
から検索するカスタム属性の名前を格納している文字列。

`ppBlob`\
[入力、出力]カスタム属性のバイトを格納する配列。

`pdwLen`\
[入力、出力]配列に返す最大バイト数を指定し、 `ppBlob` 実際に配列に書き込まれたバイト数を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、S_OK を返すか、カスタム属性が存在しない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 パラメーターを `ppBlob` null 値に設定すると、使用可能な属性の数を返すことができます。 次に、配列を割り当て、その配列をパラメーターに対して渡し `ppBlob` ます。

 属性バイトは、カスタム属性の生データを表します。

 `ppBlob` `pdwLen` パラメーターとパラメーターが null 値に設定されている場合、このメソッドを使用して、カスタム属性が単に存在するかどうかを判断できます。 ただし、より簡単な方法として、 [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md) メソッドを呼び出すこともできます。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)
