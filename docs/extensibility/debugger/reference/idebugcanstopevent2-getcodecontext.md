---
description: このイベントの場所を記述するコードコンテキストを取得します。
title: 'IDebugCanStopEvent2:: GetCodeContext |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCanStopEvent2::GetCodeContext
helpviewer_keywords:
- IDebugCanStopEvent2::GetCodeContext
ms.assetid: eecf08b6-f9b7-4358-941b-3a448a92ac62
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 29863a16d59528e86f7c5a3449e7c321b2dcaf9d
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102173538"
---
# <a name="idebugcanstopevent2getcodecontext"></a>IDebugCanStopEvent2::GetCodeContext
このイベントの場所を記述するコードコンテキストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCodeContext( 
   IDebugCodeContext2** ppCodeContext
);
```

```csharp
int GetCodeContext( 
   out IDebugCodeContext2 ppCodeContext
);
```

## <a name="parameters"></a>パラメーター
`ppCodeContext`\
入出力現在のコードの場所を表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 ほとんどのランタイムアーキテクチャでは、コードコンテキストは、特定の命令を指すプログラムの実行ストリームのアドレスと考えることができます。

 ソースコードの行の方向にあるドキュメントコンテキストを取得するには、 [Getdocumentcontext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugCanStopEvent2](../../../extensibility/debugger/reference/idebugcanstopevent2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetDocumentContext](../../../extensibility/debugger/reference/idebugcanstopevent2-getdocumentcontext.md)
