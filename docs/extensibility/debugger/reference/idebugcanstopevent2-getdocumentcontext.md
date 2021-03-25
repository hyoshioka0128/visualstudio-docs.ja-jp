---
description: このイベントの場所を記述するドキュメントコンテキストを取得します。
title: 'IDebugCanStopEvent2:: GetDocumentContext |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetDocumentContext
helpviewer_keywords:
- IDebugCanStopEvent2::GetDocumentContext
ms.assetid: 936a6c4e-30c5-4c7e-9ad5-910cc605a4b5
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 44e1f2aa918547d8b3b0b1bea1940072fe2d8f84
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105085080"
---
# <a name="idebugcanstopevent2getdocumentcontext"></a>IDebugCanStopEvent2::GetDocumentContext
このイベントの場所を記述するドキュメントコンテキストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDocumentContext ( 
   IDebugDocumentContext2** ppDocCxt
);
```

```csharp
int GetDocumentContext ( 
   out IDebugDocumentContext2 ppDocCxt
);
```

## <a name="parameters"></a>パラメーター
`ppDocCxt`\
入出力現在のコードの場所に対応するソースファイルドキュメント内の位置を表す [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md) インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 通常、ドキュメントコンテキストは、ソースファイル内の位置と考えることができます。

 コードの命令に向いているコードコンテキストを取得するには、 [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md) メソッドを呼び出します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugDocumentContext2](../../../extensibility/debugger/reference/idebugdocumentcontext2.md)
- [GetCodeContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getcodecontext.md)
