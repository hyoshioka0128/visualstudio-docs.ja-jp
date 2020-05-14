---
title: 既定のコマンド、グループ、およびツールバーの配置 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], default groups
- toolbars [Visual Studio], default
- commands [Visual Studio], default editor
- command groups
- commands [Visual Studio], default IDE
- commands [Visual Studio], default product
ms.assetid: 35342110-d639-4577-8367-00b21dcc6f07
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: b432b514231e876dda1393bad8a315030272d998
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80708885"
---
# <a name="default-command-group-and-toolbar-placement"></a>既定のコマンド、グループ、およびツールバーの配置
製品の統一性と安定性を確保するために、UI はデフォルトで特定の[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]コマンド グループを表示し、コマンドとコマンド グループの定義を提供します。 VSPackage は、標準のコマンドとコマンド グループを使用することもできます。

 デフォルトのコマンドグループは、IDE コマンド、プロダクトコマンド、エディタコマンドの 3 つのカテゴリに分類されます。

## <a name="default-ide-commands"></a>デフォルトの IDE コマンド
 デフォルトの IDE ツールバーには、 に含まれる[!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)]すべての製品で共有されるコマンドが含まれています。 これには、一般的なプロジェクト操作に関連するコマンド **([保存]** コマンドや **[項目の追加]** コマンドなど) が含まれます。 VSPackage は、このツール バーに追加または減算する必要があります、1 つの例外を除いて: 製品または VSPackage が新しいツール ウィンドウを追加する場合、ウィンドウを追加する必要があります、**表示**メニューで使用可能なツール ウィンドウの一覧にします。 新しい製品や VS パッケージは、独自のツール バーを追加できます。

## <a name="default-product-commands"></a>デフォルトの製品コマンド
 各製品は、重要なコマンドや頻繁に使用するコマンドを含む独自のデフォルトツールバーを IDE に提供できます。 ただし、既存のメニューやツールバーは可能な限り使用し、必要に応じて他のタスク固有のツールバーで補完することをお勧めします。

 ツールバーの優先度フィールドによって、その行の配置が決まります。 0 の優先順位は、ツールバーを 3 行目 (行 3) のメニュー バー (行 1) の下に配置し、[**標準**] ツールバー (行 2) に配置します。 したがって、他のツールバーは行に表示されます (優先度 + 3)。 スペースがある場合は、後続のツールバーが同じ行に配置されます。それ以外の場合は、自動的に次の行に移動します。

## <a name="default-editor-commands"></a>既定のエディター コマンド
 カスタム エディターを提供する VSPackage は、そのエディターで最も重要かつ頻繁に使用されるコマンドを含む既定のツール バーを提供する必要があります。 エディターがアクティブな場合はエディター のツール バーが表示され、エディターがアクティブでないときには非表示にする必要があります。 この可視性は`VisibilityConstraints`*、.vsct*ファイルの要素で制御されます。

 エディタツールバーは、IDE および製品ツールバーの下に配置する必要があります。

## <a name="see-also"></a>関連項目
- [IDE で定義されたコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)
- [VSPackages がユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
