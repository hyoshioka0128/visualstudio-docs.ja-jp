---
title: 'IDebugProgram2:: EnumCodePaths |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumCodePaths
helpviewer_keywords:
- IDebugProgram2::EnumCodePaths
ms.assetid: fb100c3c-9c29-4d63-bd1f-a3e531cb395f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8e71085da547b87389a8d787f24580a7610fd33f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99844750"
---
# <a name="idebugprogram2enumcodepaths"></a>IDebugProgram2::EnumCodePaths
ソースファイル内の指定された位置のコードパスの一覧を取得します。

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
からIDE の [ **ソース** ] ビューまたは [ **逆アセンブル** ] ビューで、カーソルの下にある単語。

`pStart`\
から現在のコードコンテキストを表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。

`pFrame`\
から現在のブレークポイントに関連付けられているスタックフレームを表す [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) オブジェクト。

`fSource`\
から`TRUE`**ソース** ビューの場合は0以外 () `FALSE` 。**逆アセンブル** ビューの場合は 0 ()。

`ppEnum`\
入出力コードパスのリストを格納している [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md) オブジェクトを返します。

`ppSafety`\
入出力選択したコードパスがスキップされた場合にブレークポイントとして設定される追加のコードコンテキストを表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクトを返します。 これは、たとえば、サーキットのブール式の場合に発生する可能性があります。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 コードパスは、プログラムの実行中に現在のポイントにアクセスするために呼び出されたメソッドまたは関数の名前を記述します。 コードパスの一覧は、呼び出し履歴を表します。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IEnumCodePaths2](../../../extensibility/debugger/reference/ienumcodepaths2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
