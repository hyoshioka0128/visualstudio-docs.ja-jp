---
title: 'IDebugProgramPublisher2:: UnpublishProgramNode |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugProgramPublisher2::UnpublishProgramNode
helpviewer_keywords:
- IDebugProgramPublisher2::UnpublishProgramNode
ms.assetid: 57c7e6e1-b84e-4e14-ad83-cbbb64e2f526
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 69afe6dba5db73b2b2af80031612ada5b18ae0a3
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99916178"
---
# <a name="idebugprogrampublisher2unpublishprogramnode"></a>IDebugProgramPublisher2::UnpublishProgramNode
指定されたプログラムノードを可用性からデバッグエンジン (DEs) およびセッションデバッグマネージャー (SDM) に削除します。

## <a name="syntax"></a>構文

```cpp
HRESULT UnpublishProgramNode(
   IDebugProgramNode2* pProgramNode
);
```

```csharp
int UnpublishProgramNode(
   IDebugProgramNode2 pProgramNode
);
```

## <a name="parameters"></a>パラメーター
`pProgramNode`\
から削除されるプログラムノードを表す [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>解説
 削除されると、プログラムの情報を照会するためのプログラムノードを使用できなくなります。

 プログラムノードを使用できるようにするには、 [Publishprogramnode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugProgramPublisher2](../../../extensibility/debugger/reference/idebugprogrampublisher2.md)
- [IDebugProgramNode2](../../../extensibility/debugger/reference/idebugprogramnode2.md)
- [PublishProgramNode](../../../extensibility/debugger/reference/idebugprogrampublisher2-publishprogramnode.md)
