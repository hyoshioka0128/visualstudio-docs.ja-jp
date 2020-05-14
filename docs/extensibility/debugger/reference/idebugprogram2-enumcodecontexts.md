---
title: Iデバッグプログラム2::列挙体コンテキスト |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgram2::EnumCodeContexts
helpviewer_keywords:
- IDebugProgram2::EnumCodeContexts
ms.assetid: 478e06a2-07bb-4841-8887-deab0f42ebd0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c22a5ce398e76ee97b2f0448900fd4e38f996615
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80723041"
---
# <a name="idebugprogram2enumcodecontexts"></a>IDebugProgram2::EnumCodeContexts
ソース ファイル内の指定した位置のコード コンテキストの一覧を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumCodeContexts( 
   IDebugDocumentPosition2*  pDocPos,
   IEnumDebugCodeContexts2** ppEnum
);
```

```csharp
int EnumCodeContexts( 
   IDebugDocumentPosition2     pDocPos,
   out IEnumDebugCodeContexts2 ppEnum
);
```

## <a name="parameters"></a>パラメーター
`pDocPos`\
[in]IDE に認識されているソース ファイル内の抽象位置を表す[IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)オブジェクト。

`ppEnum`[アウト]コード[コンテキスト](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)の一覧を含むオブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドを使用すると、セッション デバッグ マネージャー (SDM) または IDE は、ソース ファイルの位置をコードの位置にマップできます。 ソースが複数のコード ブロック (たとえば、C++ テンプレート) を生成する場合は、複数のコード コンテキストが返されます。

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugDocumentPosition2](../../../extensibility/debugger/reference/idebugdocumentposition2.md)
- [IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)
