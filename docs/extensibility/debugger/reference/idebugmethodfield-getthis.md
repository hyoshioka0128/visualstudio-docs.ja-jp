---
title: フィールドを取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMethodField::GetThis
helpviewer_keywords:
- IDebugMethodField::GetThis method
ms.assetid: cc235bea-e909-4d8c-ab54-936736c803fc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b29252d1586d039084ec1d21f1fc4967aea68baf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727167"
---
# <a name="idebugmethodfieldgetthis"></a>IDebugMethodField::GetThis
メソッドを`this`含`Me`む[!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)]オブジェクトの ( で ) ポインターを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetThis( 
   IDebugClassField** ppClass
);
```

```csharp
int GetThis(
   out IDebugClassField ppClass
);
```

## <a name="parameters"></a>パラメーター
`ppClass`\
[アウト]"this"[ポインターを表](../../../extensibility/debugger/reference/idebugclassfield.md)すオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 オブジェクト指向言語では、通常、クラスの現在のインスタンス化への暗黙のポインタがあります。 これは C#/C++ および`this``Me`として知られています[!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)]。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
