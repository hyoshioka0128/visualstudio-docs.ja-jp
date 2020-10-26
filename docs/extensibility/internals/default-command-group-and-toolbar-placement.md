---
title: 既定のコマンド、グループ、およびツールバーの配置 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80708885"
---
# <a name="default-command-group-and-toolbar-placement"></a>既定のコマンド、グループ、およびツールバーの配置
製品の統一性と安定性を確保するために、UI には特定のコマンドグループが既定で表示され、コマンド [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] とコマンドグループの定義が用意されています。 Vspackage では、標準のコマンドとコマンドグループを使用することもできます。

 既定のコマンドグループは、IDE コマンド、製品コマンド、およびエディターコマンドの3つのカテゴリに分類されます。

## <a name="default-ide-commands"></a>既定の IDE コマンド
 既定の IDE ツールバーには、に含まれるすべての製品によって共有されるコマンドが含まれてい [!INCLUDE[vsprvs](../../code-quality/includes/vsprvs_md.md)] ます。 これには、[ **保存** ] コマンドや [ **項目の追加** ] コマンドなど、一般的なプロジェクト操作に関連するコマンドが含まれます。 Vspackage は、このツールバーを追加または削除しないでください。ただし、product または VSPackage で新しいツールウィンドウを追加すると、[ **表示** ] メニューの使用可能なツールウィンドウの一覧にウィンドウが追加されます。 新しい製品または Vspackage は、独自のツールバーを追加できます。

## <a name="default-product-commands"></a>既定の製品コマンド
 各製品では、IDE に、重要で頻繁に使用されるコマンドを含む独自の既定のツールバーが用意されています。 ただし、可能な場合は常に既存のメニューとツールバーを使用し、必要に応じて、他のタスク固有のツールバーでそれらを補完することをお勧めします。

 ツールバーの [優先順位] フィールドによって、その行の配置が決まります。 [優先順位なし] ツールバーは、メニューバー (行 1) と **標準** ツールバー (行 2) の下にある3行目に配置されます。 そのため、他のツールバーは行 (priority + 3) に表示されます。 ルームがある場合は、同じ行に後続のツールバーが配置されます。それ以外の場合は、次の行に自動的に移動されます。

## <a name="default-editor-commands"></a>既定のエディターコマンド
 カスタムエディターを提供する VSPackage には、そのエディターで最も重要で頻繁に使用されるコマンドを含む既定のツールバーが用意されている必要があります。 エディターがアクティブになっている場合はエディターのツールバーが表示され、エディターがアクティブでない場合は非表示になります。 この表示は `VisibilityConstraints` 、 *vsct* ファイルの要素で制御されます。

 エディターのツールバーは、IDE と製品ツールバーの下に配置する必要があります。

## <a name="see-also"></a>関連項目
- [IDE で定義されているコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)
- [Vspackage のユーザーインターフェイス要素の追加方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
