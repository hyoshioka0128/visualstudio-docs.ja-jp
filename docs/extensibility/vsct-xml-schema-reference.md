---
title: VSCT XML スキーマ リファレンス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Visual Studio command table configuration files (VSCT), XML schema
- VSCT XML schema elements
ms.assetid: 49e7efae-e713-4762-a824-96fdaf92cdc9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 923a0c4b64fcae3a409a2298d6d481f6e1bb14db
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80697917"
---
# <a name="vsct-xml-schema-reference"></a>VSCT XML スキーマ リファレンス
コマンド テーブル コンパイラ スキーマ要素のテーブルを提供し、それぞれに許可された子要素と属性を示します。

 XML ベースのコマンド テーブル構成 (.vsct) ファイルは、VSPackage が統合開発環境 (IDE) に提供するコマンド要素を定義します。 これらの要素には、メニュー項目、メニュー、ツールバー、およびコンボ ボックスがあります。

> [!NOTE]
> VSCT コンパイラは、.vsct ファイルに対してプリプロセッサを実行できます。 これは通常、C++ プリプロセッサであるため、C++ ファイルで使用されるのと同じ構文を持つインクルードとマクロを定義できます。 この例は **、VSPackage プロジェクトの新しいプロジェクト**ウィザードが作成する .vsct ファイルで提供されます。

## <a name="optional-elements"></a>オプションの要素
 一部の VSCT 要素はオプションです。 引数が`Parent`指定されていない場合、Group_Undefined:0は暗示されます。 引数が`Icon`指定されていない場合は、暗黙の情報が示されます。 ショートカット キーを定義する場合、通常は使用しないエミュレーションは省略可能です。

 ビットマップ項目は、`href`引数内のビットマップストリップの位置を指定することによって、コンパイル時に埋め込むことができます。 ビットマップ ストリップは、DLL のリソースから抽出されるのではなく、マージ中にコピーされます。 引数を`href`指定すると、`usedList`引数はオプションになり、ビットマップストリップ内のすべてのスロットが使用されていると見なされます。

 すべての GUID および ID 値は、シンボル名を使用して定義する必要があります。 これらの名前は、ヘッダー ファイルまたは VSCT\<シンボル> セクションで定義できます。 シンボル名はローカル名、インクルード>\<要素、または Extern \<> 要素によって参照される必要があります。 シンボル名は、シンボル値の単純なパターンに従っている\<場合、Extern> 要素で指定されたヘッダー ファイルからインポート#define。 この値は、そのシンボルが既に定義されている限り、別のシンボルである場合があります。 GUID 定義は、OLE または C++ のいずれかの形式に従う必要があります。 ID 値は、次の行に示すように、0x の前に 10 進数または 16 進数を使用できます。

- {6D484634-E53D-4a2c-ADCB-55145C9362C8}

- { 0x6d484634, 0xe53d, 0x4a2c, { 0xad, 0xcb, 0x55, 0x14, 0x5c, 0x93, 0x62, 0xc8 } }

  XML コメントを使用することもできますが、ラウンドトリップ グラフィカル ユーザー インターフェイス (GUI) ツールによって、コメントが破棄される場合があります。 アノテーション>要素\<の内容は、形式に関係なく維持されます。

## <a name="schema-hierarchy"></a>スキーマの階層
 vsct ファイルには、次の主要な要素があります。

- [コマンド テーブル要素](../extensibility/commandtable-element.md)

- [エクスタン要素](../extensibility/extern-element.md)

- [要素を含める](../extensibility/include-element.md)

- [要素の定義](../extensibility/define-element.md)

- [コマンド要素](../extensibility/commands-element.md)

- [コマンド配置要素](../extensibility/commandplacements-element.md)

- [可視性制約要素](../extensibility/visibilityconstraints-element.md)

- [キーバインディング要素](../extensibility/keybindings-element.md)

- [使用済みコマンド要素](../extensibility/usedcommands-element.md)

- [親要素](../extensibility/parent-element.md)

- [アイコン要素](../extensibility/icon-element.md)

- [文字列要素](../extensibility/strings-element.md)

- [コマンド フラグ要素](../extensibility/command-flag-element.md)

- [シンボル要素](../extensibility/symbols-element.md)

- [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)

## <a name="see-also"></a>関連項目
- [VSPackages がユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [VS パッケージでのコマンド ルーティング](../extensibility/internals/command-routing-in-vspackages.md)
