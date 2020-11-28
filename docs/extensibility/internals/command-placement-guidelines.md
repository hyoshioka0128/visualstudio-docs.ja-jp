---
title: コマンド配置のガイドライン |Microsoft Docs
description: Visual Studio 統合開発環境 (IDE) でコマンドを配置するためのガイドラインとベストプラクティスについて説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands, small command sets
- small command sets
- command sets
ms.assetid: 63b3478e-e08a-420b-a0ec-76767e0cb289
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 11a1619eaa625e086ac93bfa0f9e208239f8c844
ms.sourcegitcommit: 2244665d5a0e22d12dd976417f2a782e68684705
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2020
ms.locfileid: "96305250"
---
# <a name="command-placement-guidelines"></a>コマンド配置のガイドライン
Visual Studio 統合開発環境 (IDE) でのコマンドの配置に関するベストプラクティスは、コマンドセットのサイズによって異なります。 コマンドは、 *vsct* ファイル内の情報に従って定義され、配置されます。

## <a name="best-practices-for-all-command-sets"></a>すべてのコマンドセットのベストプラクティス
 コマンドのすべてのセットについて、次のガイドラインに従ってください。

- コマンド構造のグラフを事前に準備します。 複数の場所で使用されるコマンド、コンボボックス、コマンドグループ、およびショートカットメニューを識別します。

- 同じグループに表示されるコマンドは、関連付けられている必要があります。

- 1つのコマンドだけを含むグループは許容されます。

- パッケージでは、既存の Visual Studio メニューに多数のコマンドを追加することはできません。 代わりに、新しいコマンドをホストするメニューまたはサブメニューを作成する必要があります。

- 既存のメニューにコマンドを配置する場合は、その目的を明確にし、既存のコマンドと混同しないように、コマンドにという名前を付けます。

## <a name="best-practices-for-small-command-sets"></a>小さなコマンドセットのベストプラクティス
 いくつかのコマンドを含む VSPackage を開発している場合は、次のガイドラインに従うこともできます。

- 可能であれば、コマンド、コンボボックス、グループ、または子メニューの [親](../../extensibility/parent-element.md) 要素を使用して、適切なグループに配置します。

- これらのグループを VSPackage によって表示されるメニューに割り当てます。

- 子メニューまたはコマンドの親は、 [Group](../../extensibility/group-element.md) 要素である必要があります。 コマンドと子メニューをグループに割り当ててから、そのグループを親メニューに割り当てます。

- コマンドの定義の後に [Commandplacements](../../extensibility/commandplacements-element.md) element セクションを追加し、要素に追加 `CommandPlacements` の各グループの [commandplacements](../../extensibility/commandplacement-element.md) 要素を追加することで、コマンドを追加のグループに配置できます。

## <a name="best-practices-for-large-command-sets"></a>大きなコマンドセットのベストプラクティス
 VSPackage に複数のコンテキストで表示される多数のコマンドが含まれる場合は、次のガイドラインにも従います。

- メニュー、グループ、コマンドを自己親子化します。 つまり、 `Parent` 項目の定義に要素を割り当てないでください。

- `CommandPlacement`要素セクションの要素エントリを使用して、 `CommandPlacements` メニュー、グループ、およびコマンドを親メニューおよびグループに配置します。

- 要素セクションでは、 `CommandPlacements` 特定のメニューまたはグループに入力するエントリを互いに隣接させる必要があります。 これにより、読みやすさが向上し、ランキングがより `Priority` 簡単に判断できるようになります。

## <a name="see-also"></a>関連項目
- [Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Visual Studio コマンドテーブル (vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
