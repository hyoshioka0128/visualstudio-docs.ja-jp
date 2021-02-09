---
title: 'IDebugFunctionObject2:: Evaluate |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::Evaluate
ms.assetid: bc54c652-904b-4297-a6db-faa329684881
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 6b7d69434a6bd6aefb073a252ee35c07fccbee6c
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99920963"
---
# <a name="idebugfunctionobject2evaluate"></a>IDebugFunctionObject2::Evaluate
関数を呼び出し、結果の値をオブジェクトとして返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Evaluate (
   IDebugObject** ppParams,
   DWORD          dwParams,
   DWORD          dwEvalFlags,
   DWORD          dwTimeout,
   IDebugObject** ppResult
);
```

```csharp
int Evaluate (
   IDebugObject     ppParams,
   uint             dwParams,
   uint             dwEvalFlags,
   uint             dwTimeout,
   out IDebugObject ppResult
);
```

## <a name="parameters"></a>パラメーター
`ppParams`\
から入力パラメーターを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトの配列。 これらの各パラメーターは、このインターフェイスのいずれかの Create メソッドを使用して作成されています。

`dwParams`\
から配列内のパラメーターの数 `ppParams` 。

`dwEvalFlags`\
から評価を実行する方法を指定する、 [Evalflags](../../../extensibility/debugger/reference/evalflags.md) 列挙のフラグの組み合わせ。

`dwTimeout`\
からこのメソッドから制御が戻るまでに待機する最大時間をミリ秒単位で指定します。 無期限に待機するには、 **無制限** を使用します。

`ppResult`\
入出力関数の値をオブジェクトとして表す **IDebugObject** を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
