---
title: CommandPlacement 要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- CommandPlacements element (VSCT XML schema)
- VSCT XML schema elements, CommandPlacements
ms.assetid: 2cbd7ac8-c55a-43d8-a26d-713b3d790016
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 43fd417c4d54c0ab57133cf6dbff2c770c1ffc45
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184336"
---
# <a name="commandplacement-element"></a>CommandPlacement 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

CommandPlacement 要素を使用すると、ボタン、グループ、およびメニューを複数のグループまたはメニューに含めることができます。 CommandPlacement 要素を使用すると、ユーザーインターフェイスの外観を変更するために、これらの項目を完全に再定義する必要はありません。  
  
 詳細については、「 [再利用可能なボタンのグループの作成](../extensibility/creating-reusable-groups-of-buttons.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```  
<CommandPlacement guid=guidMyCommandSet" id="MyCommand" priority="0x001" >  
  <Parent>... </Parent>  
</CommandPlacement>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|guid|必須です。 [Symbols 要素](../extensibility/symbols-element.md)で定義されているコマンドセットの guid。|  
|id|必須です。 に定義されている、配置するメニュー、グループ、またはコマンドの id `Symbols Element` 。|  
|priority|必須です。 親要素内の項目の視覚的な位置を決定します。|  
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|Parent|必須です。 配置する項目をホストするメニューまたはグループ。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[CommandPlacements 要素](../extensibility/commandplacements-element.md)|Commandplacements 要素および Commandplacements 要素のグループを指定します。|  
  
## <a name="example"></a>例  
  
```  
<CommandPlacements>  
  <CommandPlacement guid="guidWidgetPackage" id="cmdidInsertOptions"  
    priority="0x0300">  
    <Parent guid="cmdGuidWidgetCommands" id="menuIDEditWidget"/>  
  </CommandPlacement>  
</CommandPlacements>  
```  
  
## <a name="see-also"></a>参照  
 [CommandPlacements 要素](../extensibility/commandplacements-element.md)   
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
