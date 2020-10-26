---
title: コンボ要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- Combos element (VSCT XML schema)
- VSCT XML schema elements, Combos
ms.assetid: 392e3063-f0a0-4130-9583-23bd2aa3fa36
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: daa89266d653743a743f42e5f0b8e11c954adc1a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184409"
---
# <a name="combo-element"></a>Combo 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コンボボックスに表示されるコマンドを定義します。 次に示すように、DropDownCombo、DynamicCombo、IndexCombo、MRUCombo の4種類のコンボボックスがあります。  
  
## <a name="syntax"></a>構文  
  
```  
<combo guid="guidMyCommandSet" id="MyCommand" defaultWidth="20" idCommandList="MyCommandListID" priority="0x102" type="DropDownCombo">  
  <Parent>... </Parent  
  <CommandFlag>... </CommandFlag>  
  <Strings>... </Strings>  
</combo>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|guid|必須です。 GUID/ID コマンド識別子の GUID。|  
|id|必須です。 GUID/ID コマンド識別子の ID。|  
|defaultWidth|必須です。 コンボボックスのピクセル幅を指定する整数。|  
|idCommandList|必須です。 コンボボックスに表示される項目のリストを取得するために、アクティブなコマンドターゲットに送信される ID。 ID は、コントロールと同じ GUID スコープにあります。|  
|priority|省略可能。 優先度を示す数値です。|  
|型|省略可能。 ボタンの種類を指定する列挙値。<br /><br /> 指定されていない場合は、ボタンを使用します。<br /><br /> DropDownCombo<br /> VSPackage は、このコンボボックスの内容を入力する役割を担います。 ユーザーは、このドロップダウンリストのテキストボックスに何も入力できません。<br /><br /> DynamicCombo<br /> VSPackage は、このコンボボックスの内容を入力する役割を担います。 ユーザーはこのコンボボックスを編集して、その中の項目を選択することもできます。<br /><br /> IndexCombo<br /> テキストではなく項目のインデックスを生成する点を除いて、DynamicCombo と同じです。<br /><br /> MRUCombo<br /> VSPackage の代わりに統合開発環境 (IDE) によって塗りつぶされます。  ユーザーはこのコンボボックスで編集できます。 IDE では、コンボボックスごとに最後の16個のエントリが記憶されます。<br /><br /> ユーザーがコンボボックスで何かを選択するか、新しいものを入力すると、IDE によって適切な VSPackage が通知されます。|  
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|Parent|省略可能。 ボタンの親要素。|  
|CommandFlag|必須です。 「 [Command Flag 要素](../extensibility/command-flag-element.md)」を参照してください。 ボタンの CommandFlag の有効な値は次のとおりです。<br /><br /> -CaseSensitive<br /><br /> - CommandWellOnly<br /><br /> -DefaultDisabled<br /><br /> -Defaul/Visible<br /><br /> -DynamicVisibility<br /><br /> -フィルターフィルタ<br /><br /> -IconAndText<br /><br /> -NoAutoComplete<br /><br /> -NoButtonCustomize<br /><br /> -NoCustomize<br /><br /> -NoKeyCustomize<br /><br /> - StretchHorizontally|  
|文字列|必須です。 「 [Strings 要素](../extensibility/strings-element.md)」を参照してください。 子の ButtonText 要素を定義する必要があります。|  
|Annotation|コメント (省略可能)。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[Commands 要素](../extensibility/commands-element.md)|VSPackage ツールバーのコマンドのコレクションを表します。|  
  
## <a name="example"></a>例  
  
```  
<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"  
  defaultWidth="100" idCommandList="cmdidGetInsertOptionsList">  
  <CommandFlag>DynamicVisibility</CommandFlag>  
  <Strings>  
    <ButtonText>Select Insert Options</ButtonText>  
  </Strings>  
</Combo>  
  
<Combo guid="guidWidgetPackage" id="cmdidInsertOptions"  
  priority="0x0500" type="DropDownCombo" defaultWidth="100"  
  idCommandList="cmdidGetInsertOptionsList">  
  <Parent guid="cmdSetGuidWidgetCommands" id="groupIDFileEdit">  
  <CommandFlag>DynamicVisibility</CommandFlag>  
  <Strings>  
    <ButtonText>Select Insert Options</ButtonText>  
  </Strings>  
</Combo>  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
