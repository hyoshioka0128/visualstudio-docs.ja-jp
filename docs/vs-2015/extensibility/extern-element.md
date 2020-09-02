---
title: Extern 要素 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- Extern
helpviewer_keywords:
- VSCT XML schema elements, Extern
- Extern element (VSCT XML schema)
ms.assetid: db6c3ddd-a1ba-450a-897a-bb568a5377fc
caps.latest.revision: 16
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 17477b7eb60aa332f6910019e28f4c53aa31ebf1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204399"
---
# <a name="extern-element"></a>Extern 要素
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Extern 要素は、コンパイル時に、vsct ファイルとマージする外部ヘッダー (.h) ファイルを参照します。 マージするファイルは、VSCT コンパイラに指定されたインクルードパスに存在するか、 [Include 要素](../extensibility/include-element.md)によって参照されている必要があります。 ファイルは、他の vsct ファイルまたは C++ ヘッダーファイルにすることができます。  
  
 ヘッダーファイル内の定義は、"#define [シンボル] [値]" の形式にする必要があります。以前に定義されている場合は、値が別のシンボルである可能性があります。 定義は、コマンド項目の条件付きステートメントで使用できます。 実際に使用されていないシンボルはすべて破棄されます。  
  
 CommandTable 要素  
Extern 要素  
  
## <a name="syntax"></a>構文  
  
```  
<Extern href="stdidcmd.h" />  
```  
  
## <a name="attributes-and-elements"></a>属性および要素  
 以降のセクションでは、属性、子要素、および親要素について説明します。  
  
### <a name="attributes"></a>属性  
  
|属性|説明|  
|---------------|-----------------|  
|href|必須です。 ヘッダーファイルのパス:<br /><br /> href = "stdidcmd"|  
|条件|省略可能。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|  
|language|省略可能。 コマンドテーブル内のすべての要素の既定の言語 [\<Strings>](../extensibility/strings-element.md) :<br /><br /> language = "en-us"|  
  
### <a name="child-elements"></a>子要素  
  
|要素|説明|  
|-------------|-----------------|  
|なし。|なし。|  
  
### <a name="parent-elements"></a>親要素  
  
|要素|説明|  
|-------------|-----------------|  
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage が IDE に提供するコマンド (メニュー項目、メニュー、ツールバー、およびコンボボックス) を表すすべての要素を定義します。|  
  
## <a name="example"></a>例  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-  
  18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    <Extern href="C:\VSCore\vscommon\inc\vsshlids.h"/>  
    …  
  <Commands package="guidMyPackage">  
</CommandTable>  
```  
  
## <a name="see-also"></a>参照  
 [Visual Studio コマンドテーブル (.Vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)   
 [Vspackage のユーザーインターフェイス要素の追加方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [コマンド、メニュー、およびツール バー](../extensibility/internals/commands-menus-and-toolbars.md)
