---
title: 既定のコマンド、グループ、およびツールバーの配置 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- commands [Visual Studio], default groups
- toolbars [Visual Studio], default
- commands [Visual Studio], default editor
- command groups
- commands [Visual Studio], default IDE
- commands [Visual Studio], default product
ms.assetid: 35342110-d639-4577-8367-00b21dcc6f07
caps.latest.revision: 31
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a7fc877332f7db7b27c4a30c23f1ac395a4fc22e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68196889"
---
# <a name="default-command-group-and-toolbar-placement"></a>既定のコマンド、グループ、およびツール バーの配置
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

製品の統一性と安定性を確保するために、UI には特定のコマンドグループが既定で表示され、コマンド [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] とコマンドグループの定義が用意されています。 Vspackage では、標準のコマンドとコマンドグループを使用することもできます。  
  
 既定のコマンドグループは、IDE コマンド、製品コマンド、およびエディターコマンドの3つのカテゴリに分類されます。  
  
## <a name="default-ide-commands"></a>既定の IDE コマンド  
 既定の IDE ツールバーには、に含まれるすべての製品によって共有されるコマンドが含まれてい [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] ます。 これには、[ **保存** ] コマンドや [ **項目の追加** ] コマンドなど、一般的なプロジェクト操作に関連するコマンドが含まれます。 Vspackage は、このツールバーを追加または削除しないでください。ただし、product または VSPackage で新しいツールウィンドウを追加すると、[ **表示** ] メニューの使用可能なツールウィンドウの一覧にウィンドウが追加されます。 新しい製品または Vspackage は、独自のツールバーを追加できます。  
  
## <a name="default-product-commands"></a>既定の製品コマンド  
 各製品では、IDE に、重要で頻繁に使用されるコマンドを含む独自の既定のツールバーが用意されています。 ただし、可能な場合は常に既存のメニューとツールバーを使用し、必要に応じて、他のタスク固有のツールバーでそれらを補完することをお勧めします。  
  
 ツールバーの [優先順位] フィールドによって、その行の配置が決まります。 [優先順位なし] ツールバーは、メニューバー (行 1) と **標準** ツールバー (行 2) の下にある3行目に配置されます。 そのため、他のツールバーは行 (priority + 3) に表示されます。 ルームがある場合は、同じ行に後続のツールバーが配置されます。それ以外の場合は、次の行に自動的に移動されます。  
  
## <a name="default-editor-commands"></a>既定のエディターコマンド  
 カスタムエディターを提供する VSPackage には、そのエディターで最も重要で頻繁に使用されるコマンドを含む既定のツールバーが用意されている必要があります。 エディターがアクティブになっている場合はエディターのツールバーが表示され、エディターがアクティブでない場合は非表示になります。 この表示は、 `VisibilityConstraints Element` vsct ファイルので制御されます。  
  
 エディターのツールバーは、IDE と製品ツールバーの下に配置する必要があります。  
  
## <a name="see-also"></a>参照  
 [IDE で定義されているコマンド、メニュー、およびグループ](../../extensibility/internals/ide-defined-commands-menus-and-groups.md)   
 [VSPackage でユーザー インターフェイス要素を追加する方法](../../extensibility/internals/how-vspackages-add-user-interface-elements.md)
