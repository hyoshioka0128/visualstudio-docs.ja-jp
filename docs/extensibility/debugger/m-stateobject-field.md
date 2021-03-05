---
description: アクションが使用するデータを表すオブジェクト。
title: m_stateObject Field |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_stateObject field, Task class [.NET Framework debug engines]
ms.assetid: 68c54b22-3e1c-4031-b9c7-b972c519d8a0
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 92fdad68506c62440c7f3e130caee49b4fe780da
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158762"
---
# <a name="m_stateobject-field"></a>m_stateObject フィールド
アクションが使用するデータを表すオブジェクト。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib ( *mscorlib.dll*)

 .NET Framework からこの内部メンバーにアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>構文

```
.field assembly object m_stateObject
```

## <a name="remarks"></a>解説
 これは、 `state` コンストラクターのパラメーターです <xref:System.Threading.Tasks.Task.%23ctor%2A> 。 これは、プロパティのバッキングフィールドでも <xref:System.Threading.Tasks.Task.AsyncState%2A?displayProperty=fullName> あります。

## <a name="see-also"></a>関連項目
- [Task クラス](../../extensibility/debugger/task-class-internal-members.md)
