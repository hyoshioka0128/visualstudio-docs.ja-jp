---
title: 親要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, Parent
- Parent element (VSCT XML schema)
ms.assetid: e4624ac8-1b9a-4940-910a-528a661cefad
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 2086473bc484fed4e8e351f0c3838074557586c9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68194076"
---
# <a name="parent-element"></a>Parent 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ボタンまたはコンボボックスの親は、グループのみになることができます。 メニューまたはグループの親は、他のメニューまたはグループの場合もあります。 [Commandplacement 要素](../extensibility/commandplacement-element.md)では、この要素は必須です。それ以外のすべてのインスタンスでは、省略可能です。 この要素が省略された場合、の親は `Group_Undefined:0` 暗黙的に指定されます。  
  
## <a name="syntax"></a>構文  
  
```  
<Parent guid="guidMyCommandSet" id="MyParentGroupOrMenu" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|guid|必須です。 GUID/ID コマンド識別子の GUID。|  
|id|必須です。 GUID/ID コマンド識別子の ID。|  
  
### <a name="child-elements"></a>子要素  
 なし  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage が統合開発環境 (IDE) に提供するコマンドを表すすべての要素を定義します。 たとえば、メニュー項目、メニュー、ツールバー、コンボボックスなどです。|  
|[Buttons 要素](../extensibility/buttons-element.md)|グループ [ボタン要素](../extensibility/button-element.md) の要素。|  
|[Menus 要素](../extensibility/menus-element.md)|VSPackage が実装するすべてのメニューを定義します。|  
|[Groups 要素](../extensibility/groups-element.md)|VSPackage のコマンドグループを定義するエントリが含まれています。|  
  
## <a name="see-also"></a>参照  
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
