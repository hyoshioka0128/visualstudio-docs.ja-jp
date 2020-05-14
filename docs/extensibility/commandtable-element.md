---
title: コマンドテーブル要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- CommandTable
helpviewer_keywords:
- CommandTable element (VSCT XML schema)
- VSCT XML schema elements, CommandTable
ms.assetid: 15c38159-660a-4ef4-9643-aa6fcfca82a9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: a362763d34335b9a18c4114a7c35b23f0efee020
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739646"
---
# <a name="commandtable-element"></a>コマンド テーブル要素
コマンド テーブルは *、.vsct*ファイルのルート要素です。 これは、VSPackage が IDE に提供するコマンドの実際のレイアウトと種類を定義するファイルです。 コマンドには、メニュー項目、メニュー、ツールバー、コンボ ボックスなどがあります。 詳細については、「 [Visual Studio コマンド テーブル (.vsct) ファイル 」](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)を参照してください。

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
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

| 属性 | 説明 |
|-----------| - |
| xmlns | 必須。 XML 名前空間:<br /><br /> `xmlns=http://schemas.microsoft.com/VisualStudio/2005-10-18/CommandTable`<br /><br /> xmlns:xs="<http://www.w3.org/2001/XMLSchema> |
| language | 省略可能。 言語属性を使用して、コマンド テーブル内のすべての\<文字列>要素の既定の言語を指定できます。  言語が指定されていない場合、現在のプロセスの言語が使用されます。<br /><br /> 言語="en-us" |

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[エクスタン要素](../extensibility/extern-element.md)|省略可能。 コンパイラのプリプロセッサ ディレクティブを含みます。|
|[要素を含める](../extensibility/include-element.md)|省略可能。 コンパイルに含める任意のファイルへのパスを含みます。|
|[要素の定義](../extensibility/define-element.md)|省略可能。 名前と値を指定してシンボルを定義します。|
|[コマンド要素](../extensibility/commands-element.md)|省略可能。 他のすべての要素を含む VSPackage のすべてのコマンドを定義する親要素。|
|[コマンド配置要素](../extensibility/commandplacements-element.md)|省略可能。 コマンド バーのどこにコマンドを配置する位置を定義します。|
|[可視性制約要素](../extensibility/visibilityconstraints-element.md)|省略可能。 コマンドとツール バーの静的な表示を決定します。|
|[キーバインディング要素](../extensibility/keybindings-element.md)|省略可能。 コマンドのショートカット キーの組み合わせを指定します(存在する場合)。|
|[使用済みコマンド要素](../extensibility/usedcommands-element.md)|省略可能。 VSPackage は、他の VSPackage でもともとサポートされている独自のバージョンの機能をオプションで実装できるようにします。|
|[シンボル要素](https://www.microsoft.com/download/details.aspx?id=55984)|省略可能。 コンパイラのシンボル データ (GUID、ID など) を格納します。|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|なし||

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
