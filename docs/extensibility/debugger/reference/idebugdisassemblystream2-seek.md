---
title: 'IDebugDisassemblyStream2:: Seek |Microsoft Docs'
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80732085"
---
# <a name="idebugdisassemblystream2seek"></a>IDebugDisassemblyStream2::Seek
指定された位置を基準として、逆アセンブルストリーム内の読み取りポインターを指定された数だけ移動します。

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
からシークプロセスを開始する相対位置を指定する [SEEK_START](../../../extensibility/debugger/reference/seek-start.md) 列挙の値。

`pCodeContext`\
からシーク操作の基準となるコードコンテキストを表す [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) オブジェクト。 このパラメーターは、の場合にのみ使用されます `dwSeekStart`  =  `SEEK_START_CODECONTEXT` 。それ以外の場合、このパラメーターは無視され、null 値を指定できます。

`uCodeLocationId`\
からシーク操作の基準となるコード位置識別子。 このパラメーターは、の場合に使用されます `dwSeekStart`  =  `SEEK_START_CODELOCID` 。それ以外の場合、このパラメーターは無視され、0に設定できます。 コードの場所の識別子の説明については、「 [Getcodelocationid](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md) メソッド」の「解説」を参照してください。

`iInstructions`\
からで指定された位置に相対的に移動する命令の数 `dwSeekStart` 。 逆方向に移動するには、この値を負の値にすることができます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 `S_FALSE`シーク位置が、使用可能な命令のリストを超えたポイントになった場合は、を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 シークがリストの先頭より前の位置にある場合、読み取り位置はリスト内の最初の命令に設定されます。 がリストの末尾の後の位置にある場合、読み取り位置はリストの最後の命令に設定されます。

## <a name="see-also"></a>関連項目
- [IDebugDisassemblyStream2](../../../extensibility/debugger/reference/idebugdisassemblystream2.md)
- [SEEK_START](../../../extensibility/debugger/reference/seek-start.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
- [GetCodeLocationId](../../../extensibility/debugger/reference/idebugdisassemblystream2-getcodelocationid.md)
