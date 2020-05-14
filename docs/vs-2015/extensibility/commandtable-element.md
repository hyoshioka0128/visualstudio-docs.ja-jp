---
title: CommandTable 要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- CommandTable
helpviewer_keywords:
- CommandTable element (VSCT XML schema)
- VSCT XML schema elements, CommandTable
ms.assetid: 15c38159-660a-4ef4-9643-aa6fcfca82a9
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bb2b874f7bbe94e383e9e7fba755dcc373a93150
ms.sourcegitcommit: 374f5ec9a5fa18a6d4533fa2b797aa211f186755
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2020
ms.locfileid: "77477051"
---
# <a name="commandtable-element"></a>CommandTable 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

CommandTable は、. vsct ファイルのルート要素です。 これは、VSPackage が IDE に提供するコマンドの実際のレイアウトと種類を定義するファイルです。 コマンドには、メニュー項目、メニュー、ツールバー、およびコンボボックスを含めることができます。 詳細については、「 [Visual Studio Command Table (.Vsct) Files](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)」を参照してください。  
  
## <a name="syntax"></a>構文  
  
```xml  
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema" >  
  <Extern>... </Extern>  
  <Include>... </Include>  
  <Define>... </Define>  
  <Commands>... </Commands>  
  <CommandPlacements>... </CommandPlacements>  
  <VisibilityConstraints>... </VisibilityConstraints>  
  <KeyBindings>... </KeyBindings>  
  <UsedCommands... </UsedCommands>  
  <Symbols>... </Symbols>  
</CommandTable>  
```  
  
## <a name="attributes-and-elements"></a>属性と要素  
 次のセクションでは、属性、子要素、親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
| 属性 |                                                                                                                   説明                                                                                                                   |
|-----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   xmlns   |                                   必須。 XML 名前空間:<br /><br /> `xmlns="<http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable>"`<br /><br /> `xmlns:xs="<http://www.w3.org/2001/XMLSchema>"`                                   |
| language  | 省略可。 Language 属性は、コマンドテーブル内のすべての \<文字列 > 要素の既定の言語を指定するために使用できます。  言語が指定されていない場合は、現在のプロセスの言語が使用されます。<br /><br /> language="en-us" |
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|[Extern 要素](../extensibility/extern-element.md)|省略可。 コンパイラのプリプロセッサディレクティブを格納します。|  
|[Include 要素](../extensibility/include-element.md)|省略可。 コンパイルに含めるすべてのファイルへのパスを格納します。|  
|[Define 要素](../extensibility/define-element.md)|省略可。 名前と値を指定してシンボルを定義します。|  
|[Commands 要素](../extensibility/commands-element.md)|省略可。 他のすべての要素を含む VSPackage のすべてのコマンドを定義する親要素。|  
|[CommandPlacements 要素](../extensibility/commandplacements-element.md)|省略可。 コマンドバーのどこにコマンドを配置するかを定義します。|  
|[VisibilityConstraints 要素](../extensibility/visibilityconstraints-element.md)|省略可。 コマンドおよびツールバーを静的に表示するかどうかを決定します。|  
|[KeyBindings 要素](../extensibility/keybindings-element.md)|省略可。 コマンドのショートカットキーの組み合わせ (存在する場合) を指定します。|  
|[UsedCommands 要素](../extensibility/usedcommands-element.md)|省略可。 VSPackage は、必要に応じて、他の Vspackage でサポートされていた独自のバージョンの機能を実装できます。|  
|[Symbols 要素](https://msdn.microsoft.com/f2ddd0aa-c3dd-439e-834d-28f136a27ffa)|省略可。 コンパイラのシンボルデータ (Guid、Id など) が含まれています。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|なし||  
  
## <a name="see-also"></a>参照  
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
