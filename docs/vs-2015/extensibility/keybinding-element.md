---
title: キーバインド要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- VSCT XML schema elements, KeyBindings
- KeyBinding element (VSCT XML schema)
ms.assetid: e55a1098-15df-42a9-9f87-e3a99cf437dd
caps.latest.revision: 13
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 75d96098e8444aac9a4fc6f895099435b54f640b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180326"
---
# <a name="keybinding-element"></a>KeyBinding 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

キーバインド要素は、コマンドのキーボードショートカットを指定します。  
  
 コマンドには、単一キーバインドとデュアルキーバインドの両方を関連付けることができます。 1つのキーバインドの例としては、[ **保存** ] コマンドの CTRL + S があります。 デュアルキーバインドでは、コマンドをトリガーするために2つの連続するキーの組み合わせが必要です。 2つのキーのバインドの例として、CTRL + K、CTRL + K などがあります。  
  
## <a name="syntax"></a>構文  
  
```  
<Keybinding guid="MyGuid" id="MyId" Editor="MyEditor" key1="B" key2="x" mod1="Control" mod2="Alt" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|guid|必須です。|  
|id|必須です。|  
|エディター|必須です。 エディターの GUID は、このショートカットキーがアクティブになる編集コンテキストを示します。 グローバルバインドスコープの値は "guidVSStd97" です。|  
|key1|必須です。 有効な値には、すべての種類の英数字を含めることができます。また、2桁の16進値の前に0x と VK_constants を指定します。|  
|mod1|省略可能。 スペースで区切られた CTRL、ALT、および SHIFT の任意の組み合わせ。|  
|key2|省略可能。 有効な値には、すべての種類の英数字を含めることができます。また、2桁の16進値の前に0x と VK_constants を指定します。|  
|mod2|省略可能。 スペースで区切られた CTRL、ALT、および SHIFT の任意の組み合わせ。|  
|エミュレーター|省略可能。|  
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|Parent||  
|Annotation||  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[KeyBindings 要素](../extensibility/keybindings-element.md)|キーバインド要素とその他のキーバインドグループをグループ化します。|  
  
## <a name="example"></a>例  
  
```  
<KeyBindings>  
  <KeyBinding guid="guidWidgetPackage" id="cmdidUpdateWidget"   
    editor="guidWidgetEditor" key1="VK_F5"/>  
  <KeyBinding guid="guidWidgetPackage" id="cmdidRunWidget"   
    editor="guidWidgetEditor" key1="VK_F5" mod1="Control"/>  
</KeyBindings>  
```  
  
## <a name="see-also"></a>参照  
 [キーバインド要素](../extensibility/keybindings-element.md)   
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
