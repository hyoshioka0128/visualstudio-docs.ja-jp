---
title: CommandName 要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- CommandName element (VSCT XML schema)
- VSCT XML schema elements, CommandName
ms.assetid: a338b767-aa7e-4536-9908-e19a50ab60ac
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 113f420aa4cbbed9454df1ee0c0dd8aafd09a548
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68184320"
---
# <a name="commandname-element"></a>CommandName 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

要素は、[ `CommandName` **オプション**] ダイアログボックスの [キーボード] カテゴリに表示されるテキストと、[**カスタマイズ**] ダイアログボックスの [**コマンド**] ボックスの一覧に表示されるテキストを指定します。  
  
## <a name="syntax"></a>構文  
  
```  
<CommandName>MyCommand</CommandName>  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
 なし。  
  
### <a name="child-elements"></a>子要素  
 なし。  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[Strings 要素](../extensibility/strings-element.md)|やなどのテキスト要素をグループ化し `ButtonText` `CommandName` ます。|  
  
## <a name="see-also"></a>参照  
 [Visual Studio Command Table (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
