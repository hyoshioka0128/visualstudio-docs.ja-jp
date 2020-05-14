---
title: m_childrenフィールド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- m_children field, ContingentProperties class [.NET Framework debug engines]
ms.assetid: 0a3b5653-7bc0-4a7a-8963-9020bc52b9cb
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 07933fd4c9f359e72714600abdf8b4ee29268f84
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738429"
---
# <a name="m_children-field"></a>m_childrenフィールド
このタスクに登録されている子タスクの一覧。

 **名前空間:**<xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib *(mscorlib.dll*内)

 この内部メンバには .NET Framework からアクセスできないため、次の構文は CIL (共通中間言語) で提供されています。

## <a name="syntax"></a>構文

```csharp
.field public class System.Collections.Generic.List`1<class System.Threading.Tasks.Task> m_children
```

## <a name="remarks"></a>Remarks
 タスクの実行中は、タスクを実行するスレッドだけがこの配列にアクセスする必要があります。

 タスクが完了すると、他のスレッドは、そのフィールドに何も追加しないか、または削除しない限り、このフィールドにアクセスできます。

## <a name="see-also"></a>関連項目
- [偶発プロパティ クラス](../../extensibility/debugger/contingentproperties-class-internal-members.md)
