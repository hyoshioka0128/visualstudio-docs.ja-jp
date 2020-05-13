---
title: Iデバッグプログラム2::列挙コードパス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumCodePaths
helpviewer_keywords:
- IDebugProgram2::EnumCodePaths
ms.assetid: fb100c3c-9c29-4d63-bd1f-a3e531cb395f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b99651811cedbdb8ec0eca5b766e6d75651dd5d7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723035"
---
# <a name="idebugprogram2enumcodepaths"></a>IDebugProgram2::EnumCodePaths
ソース ファイル内の指定した位置のコード パスの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumCodePaths( 
   LPCOLESTR            pszHint,
   IDebugCodeContext2*  pStart,
   IDebugStackFrame2*   pFrame,
   BOOL                 fSource,
   IEnumCodePaths2**    ppEnum,
   IDebugCodeContext2** ppSafety
);
```

```csharp
int EnumCodePaths( 
   string                 pszHint,
   IDebugCodeContext2     pStart,
   IDebugStackFrame2      pFrame,
   Int                    fSource,
   out IEnumCodePaths2    ppEnum,
   out IDebugCodeContext2 ppSafety
);
```

## <a name="parameters"></a>パラメーター
`pszHint`\
[in]IDE の**ソース**ビューまたは**逆アセンセンブリ**ビューでカーソルの下にある単語。

`pStart`\
[in]現在のコード コンテキストを表す[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)オブジェクト。

`pFrame`\
[in]現在のブレークポイントに関連付けられているスタック フレームを表す[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)オブジェクト。

`fSource`\
[in]ソース ビュー`TRUE`の場合は**Source**0 以外の場合は`FALSE`0 以外、**逆アセンブリ**ビューでは 0 ( ) 以外の値を返します。

`ppEnum`\
[アウト]コード パスの一覧を含む[IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)オブジェクトを返します。

`ppSafety`\
[アウト]選択したコード パスがスキップされた場合にブレークポイントとして設定される追加のコード コンテキストを表す[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)オブジェクトを返します。 たとえば、短絡式のブール式の場合に発生する可能性があります。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 コード パスは、プログラムの実行の現在のポイントに到達するために呼び出されたメソッドまたは関数の名前を表します。 コード パスの一覧は、呼び出し履歴を表します。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
