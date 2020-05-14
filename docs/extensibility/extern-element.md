---
title: エクスタン要素 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- Extern
helpviewer_keywords:
- VSCT XML schema elements, Extern
- Extern element (VSCT XML schema)
ms.assetid: db6c3ddd-a1ba-450a-897a-bb568a5377fc
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 2cf6f9db77abaa7034af8d074b9833a4c1560f07
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80711484"
---
# <a name="extern-element"></a>エクスタン要素
Extern 要素は、コンパイル時に *.vsct*ファイルとマージする外部ヘッダー (*.h*) ファイルを参照します。 マージするファイルは、VSCT コンパイラに指定されたインクルード パス、または[Include 要素](../extensibility/include-element.md)によって参照されるパスに含める必要があります。 ファイルは、他の *.vsct*ファイルまたは C++ ヘッダー ファイルである場合があります。

 ヘッダーファイル内の定義は、"#define[シンボル][値]"の形式でなければなりません。 定義は、コマンド項目の条件ステートメントで使用できます。 実際に使用されていないシンボルは破棄されます。

 コマンドテーブル要素エクスターン要素

## <a name="syntax"></a>構文

```xml
<Extern href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|href|必須。 ヘッダー ファイルへのパス:<br /><br /> href="stdidcmd.h"|
|条件|省略可能。 [条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)を参照してください。|
|language|省略可能。 コマンド テーブル内のすべての[\<文字列>](../extensibility/strings-element.md)要素の既定の言語:<br /><br /> 言語="en-us"|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[なし] :|[なし] :|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[コマンド テーブル要素](../extensibility/commandtable-element.md)|コマンドを表す要素 、つまり、メニュー項目、メニュー、ツールバー、およびコンボ ボックスを表す、VSPackage が IDE に提供するすべての要素を定義します。|

## <a name="example"></a>例

```xml
<?xml version="1.0" encoding="utf-8"?>
<CommandTable xmlns="http://schemas.microsoft.com/VisualStudio/2005-10-
  18/CommandTable" xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <Extern href="C:\VSCore\vscommon\inc\vsshlids.h"/>
    ...
  <Commands package="guidMyPackage">
</CommandTable>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [VSPackages がユーザー インターフェイス要素を追加する方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
