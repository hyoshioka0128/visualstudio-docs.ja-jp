---
title: コンティンジェントプロパティクラス - 内部メンバー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ContingentProperties class [.NET Framework debug engines]
- debug engines, ContingentProperties class [.NET Framework]
ms.assetid: c49d1362-ab1c-4b6d-9950-fcae40e0e66b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: c6441cafcc34a06464061b41691ea5faa32fc359
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739102"
---
# <a name="contingentproperties-class---internal-members"></a>コンティンジェントプロパティクラス - 内部メンバー
オブジェクトの追加プロパティを<xref:System.Threading.Tasks.Task>格納します。

 **名前空間:**<xref:System.Threading.Tasks?displayProperty=fullName>

 **アセンブリ:** mscorlib (mscorlib.dll 内)

 これらの内部メンバには .NET Framework からアクセスできないため、次の構文は CIL (共通中間言語) で提供されています。

## <a name="syntax"></a>構文

```csharp
.class auto ansi nested assembly beforefieldinit ContingentProperties
       extends System.Object
```

## <a name="members"></a>メンバー

### <a name="fields"></a>フィールド

|名前|説明|
|----------|-----------------|
|[m_children](../../extensibility/debugger/m-children-field.md)|このタスクに登録されている子タスクの一覧。|

## <a name="remarks"></a>Remarks
 .NET Framework では、このクラスのフィールドは必要な場合にのみ初期化されます。

## <a name="see-also"></a>関連項目
- [NET フレームワークの並列拡張内部](../../extensibility/debugger/parallel-extension-internals-for-the-dotnet-framework.md)
