---
title: クエリ2:::カスタム属性の名前 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
helpviewer_keywords:
- IDebugCustomAttributeQuery2::GetCustomAttributeByName
ms.assetid: 7428dfeb-8929-41b2-9b99-cb343a86c02d
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 47471f2743e705b06fb9a1bda6752b24a7836d1b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732565"
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
[in]検索するカスタム属性の名前を含む文字列。

`ppBlob`\
[イン、アウト]カスタム属性バイトで埋め込まれる配列。

`pdwLen`\
[イン、アウト]配列に返す最大バイト数を`ppBlob`指定し、実際に配列に書き込まれたバイト数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OKを返すか、カスタム属性が存在しない場合はS_FALSEを返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 パラメーターを`ppBlob`null 値に設定して、使用可能な属性バイト数を返します。 次に、配列を割り当て、その`ppBlob`配列をパラメータに渡します。

 属性バイトは、カスタム属性の生データを表します。

 パラメーターと`ppBlob``pdwLen`パラメーターが null 値に設定されている場合、このメソッドを使用して、カスタム属性が単に存在するかどうかを判断できます。 しかし、より簡単な方法は、[メソッド](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)を呼び出す方法です。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IsCustomAttributeDefined](../../../extensibility/debugger/reference/idebugcustomattributequery2-iscustomattributedefined.md)
