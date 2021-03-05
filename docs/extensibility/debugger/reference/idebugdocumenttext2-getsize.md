---
description: ドキュメント内のこの位置にあるテキストのサイズを取得します。
title: 'IDebugDocumentText2:: GetSize |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDocumentText2::GetSize
helpviewer_keywords:
- IDebugDocumentText2::GetSize
ms.assetid: bf515a8f-dcee-4004-8f81-543d547ceaae
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 91dd1b2a510589ab048bd1bd290b0ab4aabe571b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167309"
---
# <a name="idebugdocumenttext2getsize"></a>IDebugDocumentText2::GetSize
ドキュメント内のこの位置にあるテキストのサイズを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSize( 
   ULONG* pcNumLines,
   ULONG* pcNumChars
);
```

```csharp
int GetSize( 
   ref uint pcNumLines,
   ref uint pcNumChars
);
```

## <a name="parameters"></a>パラメーター
`pcNumLines`\
入出力テキストの行数を返します。

`pcNumChars`\
入出力テキストの文字数を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説

 [C++ のみ]特定の値が必要ない場合は、パラメーターに NULL を渡します。

 [C# のみ]両方のパラメーターを指定する必要があります。

## <a name="see-also"></a>関連項目
- [IDebugDocumentText2](../../../extensibility/debugger/reference/idebugdocumenttext2.md)
