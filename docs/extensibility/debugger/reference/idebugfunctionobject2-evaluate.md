---
title: 関数オブジェクト2::評価 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- IDebugFunctionObject2::Evaluate
ms.assetid: bc54c652-904b-4297-a6db-faa329684881
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d87d7d3531d198a1478b4aaa55b354c3ac101302
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728437"
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
[in]入力パラメーターを表す[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトの配列。 これらの各パラメーターは、このインターフェイスで Create メソッドのいずれかを使用して作成されました。

`dwParams`\
[in]配列内のパラメーターの`ppParams`数。

`dwEvalFlags`\
[in]評価の実行方法を指定する[EVALFLAGS](../../../extensibility/debugger/reference/evalflags.md)列挙体のフラグの組み合わせ。

`dwTimeout`\
[in]このメソッドから戻るまでの最大待機時間をミリ秒単位で指定します。 **無限**に待機するには INFINITE を使用します。

`ppResult`\
[アウト]オブジェクトとして関数の値を表す**IDebugObject**を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="see-also"></a>関連項目
- [IDebugFunctionObject2](../../../extensibility/debugger/reference/idebugfunctionobject2.md)
