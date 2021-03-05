---
description: このタスクに登録されている子タスクの一覧。
title: m_children Field |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5aaf29d76a7bbd81a416c86360f315bc5c09b76c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158870"
---
# <a name="m_children-field"></a>m_children フィールド
このタスクに登録されている子タスクの一覧。

 **名前空間:** <xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib ( *mscorlib.dll*)

 .NET Framework からこの内部メンバーにアクセスできないため、次の構文は、共通中間言語 (CIL) で提供されています。

## <a name="syntax"></a>構文

```csharp
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children
```

## <a name="remarks"></a>解説
 タスクの実行中は、タスクを実行するスレッドだけがこの配列にアクセスします。

 タスクが完了している場合は、他のスレッドがこのフィールドに何も追加していない限り、または削除しない限り、このフィールドにアクセスできます。

## <a name="see-also"></a>関連項目
- [ContingentProperties クラス](../../extensibility/debugger/contingentproperties-class-internal-members.md)
