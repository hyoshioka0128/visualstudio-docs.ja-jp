---
title: Used Commands 要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- UsedCommands
helpviewer_keywords:
- UsedCommands element (VSCT XML schema)
- VSCT XML schema elements, UsedCommands
ms.assetid: 5e000ee0-a919-46e9-9277-2a0659f1eb78
caps.latest.revision: 14
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ba37458e0f8abca27047574170ab8aa3cc7a44ce
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186289"
---
# <a name="usedcommands-element"></a>UsedCommands 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Used Commands 要素は、実行されたコマンド要素とその他の実行されたコマンドグループをグループ化します。  
  
 Used Commands 要素は省略可能です。 パッケージの外部で定義されたコマンドを呼び出さない場合は、このセクションを vsct ファイルに含める必要はありません。  
  
## <a name="syntax"></a>構文  
  
```  
<UsedCommands condition="Defined(DEBUG)">  
  <UsedCommand ... />  
</UsedCommands>  
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
|[UsedCommand 要素](../extensibility/usedcommand-element.md)|他のコードによって実装されるコマンド。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage が統合開発環境 (IDE) に提供するコマンド (メニュー項目、メニュー、ツールバー、コンボボックスなど) を表すすべての要素を定義します。|  
  
## <a name="example"></a>例  
  
```  
<UsedCommands>  
  <UsedCommand guid="guidVSStd97" id="cmdidCut"/>  
  <UsedCommand guid="guidVSStd97" id="cmdidCopy"/>  
  <UsedCommand guid="guidVSStd97" id="cmdidPaste"/>  
</UsedCommands>  
```  
  
## <a name="see-also"></a>参照  
 [Used Command 要素](../extensibility/usedcommand-element.md)   
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
