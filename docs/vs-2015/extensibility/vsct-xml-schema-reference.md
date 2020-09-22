---
title: VSCT XML スキーマリファレンス |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- Visual Studio command table configuration files (VSCT), XML schema
- VSCT XML schema elements
ms.assetid: 49e7efae-e713-4762-a824-96fdaf92cdc9
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: e56de828d3b357762da98cde3b9591033c6b5d19
ms.sourcegitcommit: fb8babf5cd72f1fc2f97ffe4ad7b62d91f325f61
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/07/2020
ms.locfileid: "90841777"
---
# <a name="vsct-xml-schema-reference"></a>VSCT XML スキーマ リファレンス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

コマンドテーブルコンパイラスキーマ要素のテーブルを提供します。これには、許可されている子要素と属性がそれぞれ含まれています。  
  
 XML ベースのコマンドテーブル構成 (vsct) ファイルは、VSPackage が統合開発環境 (IDE) に提供するコマンド要素を定義します。 これらの要素には、メニュー項目、メニュー、ツールバー、およびコンボボックスが含まれます。  
  
> [!NOTE]
> VSCT コンパイラは、vsct ファイルでプリプロセッサを実行できます。 これは通常、C++ プリプロセッサであるため、C++ ファイルで使用されているのと同じ構文を持つインクルードマクロとマクロを定義できます。 この例は、 **新しいプロジェクト** ウィザードによって VSPackage プロジェクト用に作成される、vsct ファイルで提供されています。  
  
## <a name="optional-elements"></a>省略可能な要素  
 一部の VSCT 要素は省略可能です。 `Parent`引数が指定されていない場合、Group_Undefined: 0は暗黙的に指定されます。 `Icon`引数が指定されていない場合、guidOfficeIcon: msotcidNoIcon が暗黙的に指定されます。 ショートカットキーが定義されている場合、通常は使用されていないエミュレーションがオプションです。  
  
 ビットマップ項目は、コンパイル時に、引数にビットマップストリップの場所を指定することで埋め込むことができ `href` ます。 ビットマップストリップは、DLL のリソースから抽出されるのではなく、マージ中にコピーされます。 引数を指定した場合、 `href` `usedList` 引数は省略可能になり、ビットマップストリップ内のすべてのスロットが使用されていると見なされます。  
  
 すべての GUID と ID の値は、シンボル名を使用して定義する必要があります。 これらの名前は、ヘッダーファイルまたは VSCT セクションで定義でき \<Symbols> ます。 シンボル名は、ローカルであるか、 \<Include> 要素を通じて、または要素によって参照されている必要があり \<Extern> ます。 シンボル名は、要素で指定されているヘッダーファイルから \<Extern> #define シンボル値の単純なパターンに従っている場合、そのファイルからインポートされます。 この値は、そのシンボルが既に定義されている限り、別のシンボルにすることができます。 GUID 定義は、OLE 形式または C++ 形式のいずれかに従う必要があります。 次の行に示すように、ID 値には、10進数または0x の前に0x が付く16進数を指定できます。  
  
- {6D484634-E53D-4a2c-ADCB-55145C9362C8}  
  
- {0x6d484634、0xe53d、0x4a2c、{0xad、0xcb、0xad、0x14、0x5c、0x93、0x62、0xcb}}  
  
  XML コメントを使用することもできますが、ラウンドトリップグラフィカルユーザーインターフェイス (GUI) ツールはそれらを破棄する場合があります。 要素の内容は、 \<Annotation> 形式に関係なく維持されることが保証されます。  
  
## <a name="schema-hierarchy"></a>スキーマの階層  
 Vsct ファイルには、次の主要な要素があります。  
  
 [CommandTable 要素](../extensibility/commandtable-element.md)  
  
 [Extern 要素](../extensibility/extern-element.md)  
  
 [Include 要素](../extensibility/include-element.md)  
  
 [Define 要素](../extensibility/define-element.md)  
  
 [Commands 要素](../extensibility/commands-element.md)  
  
 [CommandPlacements 要素](../extensibility/commandplacements-element.md)  
  
 [VisibilityConstraints 要素](../extensibility/visibilityconstraints-element.md)  
  
 [KeyBindings 要素](../extensibility/keybindings-element.md)  
  
 [UsedCommands 要素](../extensibility/usedcommands-element.md)  
  
 [親要素](../extensibility/parent-element.md)  
  
 [Icon 要素](../extensibility/icon-element.md)  
  
 [Strings 要素](../extensibility/strings-element.md)  
  
 [Command Flag 要素](../extensibility/command-flag-element.md)  
  
 [Symbols 要素](../extensibility/symbols-element.md)  
  
 [Conditional 属性](../extensibility/vsct-xml-schema-conditional-attributes.md)  
  
## <a name="see-also"></a>参照  
 [Vspackage のユーザーインターフェイス要素の追加方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)   
 [Vspackage のコマンド ルーティング](../extensibility/internals/command-routing-in-vspackages.md)
