---
title: 'IDebugMethodField:: GetThis |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80727167"
---
# <a name="idebugmethodfieldgetthis"></a>IDebugMethodField::GetThis
`this` `Me` メソッドを格納しているオブジェクトの (の) ポインターを取得し [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] ます。

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
入出力"This" ポインターを表す [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 オブジェクト指向言語では、通常、クラスの現在のインスタンス化への暗黙的なポインターが存在します。 これは、「 `this` 」のように、C# の/c + + ととして知られてい `Me` [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] ます。

## <a name="see-also"></a>関連項目
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
