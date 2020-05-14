---
title: IDebugdisアセンブリストリーム2::シーク |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugDisassemblyStream2::Seek
helpviewer_keywords:
- IDebugDisassemblyStream2::Seek
ms.assetid: afec3008-b1e0-4803-ad24-195dbfb6497e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4954b3b278b3c7a6b798a4ffda3856ab8bb200c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80732085"
---
# <a name="idebugdisassemblystream2seek"></a>IDebugDisassemblyStream2::Seek
指定した位置に対する指定した数の命令を逆アセンブリ ストリーム内の読み取りポインターに移動します。

## <a name="syntax"></a>構文

```cpp
HRESULT Seek( 
   SEEK_START          dwSeekStart,
   IDebugCodeContext2* pCodeContext,
   UINT64              uCodeLocationId,
   INT64               iInstructions
);
```

```csharp
int Seek( 
   enum_SEEK_START    dwSeekStart,
   IDebugCodeContext2 pCodeContext,
   ulong              uCodeLocationId,
   long               iInstructions
);
```

## <a name="parameters"></a>パラメーター
`dwSeekStart`\
[in]シーク処理を開始する相対位置を指定する[SEEK_START](../../../extensibility/debugger/reference/seek-start.md)列挙体の値。

`pCodeContext`\
[in]シーク操作の相対位置にあるコード コンテキストを表す[IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)オブジェクト。 このパラメータは、 `dwSeekStart`  =  `SEEK_START_CODECONTEXT`;それ以外の場合、このパラメーターは無視され、null 値にすることができます。

`uCodeLocationId`\
[in]シーク操作の相対位置であるコードの場所の識別子。 このパラメータは、 `dwSeekStart`  =  `SEEK_START_CODELOCID`;それ以外の場合、このパラメーターは無視され、0 に設定できます。 コードの場所識別子の説明については[、GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)メソッドの解説セクションを参照してください。

`iInstructions`\
[in]で指定した位置を基準に移動する命令の数`dwSeekStart`。 この値は、逆方向に移動する場合に負の値にすることができます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`シーク位置が使用可能な命令のリストを超えるポイントに戻ります。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 シークがリストの先頭の前の位置に置かれた場合、読み取り位置はリストの最初の命令に設定されます。 参照がリストの末尾の後の位置に設定されている場合、読み取り位置はリストの最後の命令に設定されます。

## <a name="see-also"></a>関連項目
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [SEEK_START](../../../extensibility/debugger/reference/seek-start.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)
