---
title: VisibilityConstraints 要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- VisibilityConstraints
helpviewer_keywords:
- VSCT XML schema elements, VisibilityConstraints
- VisibilityConstraints element (VSCT XML schema)
ms.assetid: d6dcd314-6fe4-4693-a189-91fa026c7b34
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 06f6a74fabfc1bd86f54656c6b30b55690940a0d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62585127"
---
# <a name="visibilityconstraints-element"></a>VisibilityConstraints 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

VisibilityConstraints 要素は、コマンドおよびツールバーのグループの静的表示を決定します。 可視性は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] VSPackage を読み込まずに、統合開発環境 (IDE) によって最初に制御されます。  
  
## <a name="syntax"></a>構文  
  
```  
<VisibilityConstraints>  
  <VisibilityConstraint>... </VisibilityConstraint>  
  <VisibilityConstraint>... </VisibilityConstraint>  
</VisibilityConstraint>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[VisibilityItem 要素](../extensibility/visibilityitem-element.md)|コマンドおよびツールバーを静的に表示するかどうかを決定します。|  
|[VisibilityConstraints](../extensibility/visibilityconstraints-element.md)|コマンドおよびツールバーのグループを静的に表示するかどうかを決定します。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage が IDE に提供するコマンド (メニュー項目、メニュー、ツールバー、コンボボックスなど) を表すすべての要素を定義します。|  
  
## <a name="example"></a>例  
  
```  
<VisibilityConstraints>  
  <VisibilityItem guid="cmdSetGuidMyProductCommands"     id="cmdidAddWidget"  
    context="guidNotViewSourceMode"/>  
</VisibilityConstraints>  
```  
  
## <a name="see-also"></a>参照  
 [VisibilityItem 要素](../extensibility/visibilityitem-element.md)   
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
