---
title: Iデバッグクラスフィールド::Doesインターフェイス存在 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::DoesInterfaceExist
helpviewer_keywords:
- IDebugClassField::DoesInterfaceExist method
ms.assetid: cc0c8642-1a76-4fda-a309-7018a34883c9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ba732b698f7372772142fda73e71d9e22aa443a6
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734498"
---
# <a name="idebugclassfielddoesinterfaceexist"></a>IDebugClassField::DoesInterfaceExist
特定のインターフェイスがクラスで定義されているかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT DoesInterfaceExist( 
   LPCOLESTR pszInterfaceName
);
```

```csharp
int DoesInterfaceExist(
   [In] string pszInterfaceName
);
```

## <a name="parameters"></a>パラメーター
`pszInterfaceName`\
[in]検索するインターフェイス名を含む文字列。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OKを返し、インターフェイスが存在しない場合はS_FALSEを返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、すべてのインターフェイスの列挙体を取得し、一致するインターフェイスの一覧を検索します。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
