---
description: カスタムデバッグエンジン (DE) インターフェイスを取得します。
title: 'IDebugQueryEngine2:: GetEngineInterface |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugQueryEngine2::GetEngineInterface
helpviewer_keywords:
- IDebugQueryEngine2::GetEngineInterface
ms.assetid: ed84aa98-7ec7-48f3-97ae-821090bc3664
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ca0bb320bfe55879b290093a60c347b3a820e35d
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083662"
---
# <a name="idebugqueryengine2getengineinterface"></a>IDebugQueryEngine2::GetEngineInterface
カスタムデバッグエンジン (DE) インターフェイスを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetEngineInterface( 
   IUnknown** ppUnk
);
```

```csharp
int GetEngineInterface( 
   out object ppUnk
);
```

## <a name="parameters"></a>パラメーター
`ppUnk`\
入出力オブジェクトが `IUnknown` デバッグエンジン (de) を表し、de に関連付けられた他の有効なインターフェイス ( [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md) 、 [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)など) に対してクエリを実行できることを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドから取得したインターフェイスを使用してを呼び出すとセッションデバッグマネージャーの処理が回避されるため、結果として得られるインターフェイスを注意して使用する必要があります。また、デバッグ中に SDM が不適切な状態になったり、エラーを生成したりする可能性があります。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugQueryEngine2](../../../extensibility/debugger/reference/idebugqueryengine2.md)
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEngineLaunch2](../../../extensibility/debugger/reference/idebugenginelaunch2.md)
