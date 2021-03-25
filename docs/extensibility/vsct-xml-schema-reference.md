---
title: VSCT XML スキーマリファレンス |Microsoft Docs
description: VSCT XML スキーマのリファレンス記事では、コマンドテーブルコンパイラのスキーマ要素について説明し、それぞれに許可されている子要素と属性を示します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio command table configuration files (VSCT), XML schema
- VSCT XML schema elements
ms.assetid: 49e7efae-e713-4762-a824-96fdaf92cdc9
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 9f24d11c9458b56b5b66de495a18ec75491d3ac0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105062305"
---
# <a name="vsct-xml-schema-reference"></a>VSCT XML スキーマリファレンス
コマンドテーブルコンパイラスキーマ要素のテーブルを提供します。これには、許可されている子要素と属性がそれぞれ含まれています。

 XML ベースのコマンドテーブル構成 (vsct) ファイルは、VSPackage が統合開発環境 (IDE) に提供するコマンド要素を定義します。 これらの要素には、メニュー項目、メニュー、ツールバー、およびコンボボックスが含まれます。

> [!NOTE]
> VSCT コンパイラは、vsct ファイルでプリプロセッサを実行できます。 これは通常、C++ プリプロセッサであるため、C++ ファイルで使用されているのと同じ構文を持つインクルードマクロとマクロを定義できます。 この例は、 **新しいプロジェクト** ウィザードによって VSPackage プロジェクト用に作成される、vsct ファイルで提供されています。

## <a name="optional-elements"></a>オプションの要素
 一部の VSCT 要素は省略可能です。 `Parent`引数が指定されていない場合、Group_Undefined: 0は暗黙的に指定されます。 `Icon`引数が指定されていない場合、guidOfficeIcon: msotcidNoIcon が暗黙的に指定されます。 ショートカットキーが定義されている場合、通常は使用されていないエミュレーションがオプションです。

 ビットマップ項目は、コンパイル時に、引数にビットマップストリップの場所を指定することで埋め込むことができ `href` ます。 ビットマップストリップは、DLL のリソースから抽出されるのではなく、マージ中にコピーされます。 引数を指定した場合、 `href` `usedList` 引数は省略可能になり、ビットマップストリップ内のすべてのスロットが使用されていると見なされます。

 すべての GUID と ID の値は、シンボル名を使用して定義する必要があります。 これらの名前は、ヘッダーファイルまたは VSCT セクションで定義でき \<Symbols> ます。 シンボル名は、ローカルであるか、 \<Include> 要素を通じて、または要素によって参照されている必要があり \<Extern> ます。 シンボル名は、要素で指定されているヘッダーファイルから \<Extern> #define シンボル値の単純なパターンに従っている場合、そのファイルからインポートされます。 この値は、そのシンボルが既に定義されている限り、別のシンボルにすることができます。 GUID 定義は、OLE 形式または C++ 形式のいずれかに従う必要があります。 次の行に示すように、ID 値には、10進数または0x の前に0x が付く16進数を指定できます。

- {6D484634-E53D-4a2c-ADCB-55145C9362C8}

- {0x6d484634、0xe53d、0x4a2c、{0xad、0xcb、0xad、0x14、0x5c、0x93、0x62、0xcb}}

  XML コメントを使用することもできますが、ラウンドトリップグラフィカルユーザーインターフェイス (GUI) ツールはそれらを破棄する場合があります。 要素の内容は、 \<Annotation> 形式に関係なく維持されることが保証されます。

## <a name="schema-hierarchy"></a>スキーマの階層
 Vsct ファイルには、次の主要な要素があります。

- [CommandTable 要素](../extensibility/commandtable-element.md)

- [Extern 要素](../extensibility/extern-element.md)

- [Include 要素](../extensibility/include-element.md)

- [Define 要素](../extensibility/define-element.md)

- [Commands 要素](../extensibility/commands-element.md)

- [CommandPlacements 要素](../extensibility/commandplacements-element.md)

- [VisibilityConstraints 要素](../extensibility/visibilityconstraints-element.md)

- [キーバインド要素](../extensibility/keybindings-element.md)

- [Used Commands 要素](../extensibility/usedcommands-element.md)

- [親要素](../extensibility/parent-element.md)

- [Icon 要素](../extensibility/icon-element.md)

- [Strings 要素](../extensibility/strings-element.md)

- [Command Flag 要素](../extensibility/command-flag-element.md)

- [Symbols 要素](../extensibility/symbols-element.md)

- [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)

## <a name="see-also"></a>こちらもご覧ください
- [Vspackage のユーザーインターフェイス要素の追加方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [Vspackage でのコマンドルーティング](../extensibility/internals/command-routing-in-vspackages.md)
