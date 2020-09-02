---
title: コマンド配置のガイドライン |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands, small command sets
- small command sets
- command sets
ms.assetid: 63b3478e-e08a-420b-a0ec-76767e0cb289
caps.latest.revision: 29
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5d88a477403c98ff11c5f7303b55f5eb713b668c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68195100"
---
# <a name="command-placement-guidelines"></a>コマンド配置のガイドライン
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

Visual Studio 統合開発環境 (IDE) でのコマンドの配置に関するベストプラクティスは、コマンドセットのサイズによって異なります。 コマンドは、vsct ファイル内の情報に従って定義され、配置されます。  
  
## <a name="best-practices-for-all-command-sets"></a>すべてのコマンドセットのベストプラクティス  
 コマンドのすべてのセットについて、次のガイドラインに従ってください。  
  
- コマンド構造のグラフを事前に準備します。 複数の場所で使用されるコマンド、コンボボックス、コマンドグループ、およびショートカットメニューを識別します。  
  
- 同じグループに表示されるコマンドは、関連付けられている必要があります。  
  
- 1つのコマンドだけを含むグループは許容されます。  
  
- パッケージでは、既存の Visual Studio メニューに多数のコマンドを追加することはできません。 代わりに、新しいコマンドをホストするメニューまたはサブメニューを作成する必要があります。  
  
- 既存のメニューにコマンドを配置する場合は、その目的を明確にし、既存のコマンドと混同しないように、コマンドにという名前を付けます。  
  
## <a name="best-practices-for-small-command-sets"></a>小さなコマンドセットのベストプラクティス  
 いくつかのコマンドを含む VSPackage を開発している場合は、次のガイドラインに従うこともできます。  
  
- 可能であれば、コマンド、コンボボックス、グループ、または子メニューの [親要素](../../extensibility/parent-element.md) を使用して、適切なグループに配置します。  
  
- これらのグループを VSPackage によって表示されるメニューに割り当てます。  
  
- 子メニューまたはコマンドの親は、 [Group 要素](../../extensibility/group-element.md)である必要があります。 コマンドと子メニューをグループに割り当ててから、そのグループを親メニューに割り当てます。  
  
- コマンドの定義の後に [Commandplacements element](../../extensibility/commandplacements-element.md) セクションを追加し、 `CommandPlacements Element` 追加の各グループの [commandplacements 要素](../../extensibility/commandplacement-element.md) にを追加することで、コマンドを追加のグループに配置できます。  
  
## <a name="best-practices-for-large-command-sets"></a>大きなコマンドセットのベストプラクティス  
 VSPackage に複数のコンテキストで表示される多数のコマンドが含まれる場合は、次のガイドラインにも従います。  
  
- メニュー、グループ、コマンドを自己親子化します。 つまり、 `Parent Element` 項目の定義にを割り当てないでください。  
  
- セクションのエントリを使用して、 `CommandPlacement Element` `CommandPlacements Element` メニュー、グループ、およびコマンドを親のメニューとグループに配置します。  
  
- セクションでは、 `CommandPlacements` 特定のメニューまたはグループに入力するエントリを互いに隣接させる必要があります。 これにより、読みやすさが向上し、ランキングがより `Priority` 簡単に判断できるようになります。  
  
## <a name="see-also"></a>参照  
 [Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Visual Studio Command Table (.Vsct) ファイル](../../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
