---
title: コマンド配置のガイドライン |マイクロソフトドキュメント
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
ms.openlocfilehash: 021a5fd9f9931e3041a431d211c8ab49978bbbab
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80709563"
---
# <a name="command-placement-guidelines"></a>コマンド配置のガイドライン
Visual Studio 統合開発環境 (IDE) でコマンドを配置する際のベスト プラクティスは、コマンド セットのサイズによって異なります。 コマンドは *、.vsct*ファイルの情報に従って定義および配置されます。

## <a name="best-practices-for-all-command-sets"></a>すべてのコマンド セットのベスト プラクティス
 コマンドの各セットについて、次のガイドラインに従ってください。

- コマンド構造のチャートを事前に準備します。 複数の場所で使用するコマンド、コンボ ボックス、コマンド グループ、およびショートカット メニューを識別します。

- 同じグループに表示されるコマンドは関連付ける必要があります。

- 1 つのコマンドのみを含むグループは、受け入れられます。

- パッケージは、既存の Visual Studio メニューに多くのコマンドを追加しないでください。 代わりに、新しいコマンドをホストするメニューまたはサブメニューを作成する必要があります。

- 既存のメニューにコマンドを配置する場合は、コマンドの目的が明確になり、既存のコマンドと混同しないように、コマンドに名前を付けます。

## <a name="best-practices-for-small-command-sets"></a>小さいコマンド セットのベスト プラクティス
 コマンドが少ない VSPackage を開発する場合は、次のガイドラインにも従ってください。

- 可能な場合は、コマンド、コンボ ボックス、グループ、または子メニューの[Parent](../../extensibility/parent-element.md)要素を使用して、適切なグループに配置します。

- VSPackage によって表示されるメニューにこれらのグループを割り当てます。

- 子メニューまたはコマンドの親は[、グループ](../../extensibility/group-element.md)要素である必要があります。 コマンドと子メニューをグループに割り当て、親メニューに割り当てます。

- コマンドの定義の後に[CommandPlacements](../../extensibility/commandplacements-element.md)要素セクションを追加し、追加する各グループの[CommandPlacement](../../extensibility/commandplacement-element.md)要素を`CommandPlacements`要素に追加することで、コマンドを追加のグループに配置できます。

## <a name="best-practices-for-large-command-sets"></a>大きいコマンド セットのベスト プラクティス
 VSPackage に複数のコンテキストで表示されるコマンドが多数ある場合は、次のガイドラインにも従ってください。

- メニュー、グループ、コマンドを自己親子にする。 つまり、項目の`Parent`定義に要素を割り当てないでください。

- 要素`CommandPlacement`セクションの要素エントリ`CommandPlacements`を使用して、親メニューおよび親グループにメニュー、グループ、およびコマンドを配置します。

- `CommandPlacements`要素セクションでは、特定のメニューまたはグループに入力するエントリが互いに隣接している必要があります。 これは読みやすさを助け`Priority`、ランキングを判断しやすくします。

## <a name="see-also"></a>関連項目
- [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Visual Studio コマンド テーブル (.vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
