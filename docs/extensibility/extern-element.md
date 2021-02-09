---
title: Extern 要素 |Microsoft Docs
description: Extern 要素は、コンパイル時に、vsct ファイルとマージする外部ヘッダー (.h) ファイルを参照します。
ms.custom: SEO-VS-2020
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
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8892de377d2383e5aed3ec7824616d626bc5164f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99862097"
---
# <a name="extern-element"></a>Extern 要素
Extern 要素は、コンパイル時に、 *vsct* ファイルとマージする外部ヘッダー (*.h*) ファイルを参照します。 マージするファイルは、VSCT コンパイラに指定されたインクルードパスに存在するか、 [include 要素](../extensibility/include-element.md)によって参照されている必要があります。 ファイルは、他の *vsct* ファイルまたは C++ ヘッダーファイルにすることができます。

 ヘッダーファイル内の定義は、"#define [シンボル] [値]" の形式にする必要があります。以前に定義されている場合は、値が別のシンボルである可能性があります。 定義は、コマンド項目の条件付きステートメントで使用できます。 実際に使用されていないシンボルはすべて破棄されます。

 CommandTable 要素 Extern 要素

## <a name="syntax"></a>構文

```xml
<Extern href="stdidcmd.h" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|href|必須。 ヘッダーファイルのパス:<br /><br /> href = "stdidcmd"|
|条件|任意。 「 [条件付き属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|
|language|任意。 コマンドテーブル内のすべての要素の既定の言語 [\<Strings>](../extensibility/strings-element.md) :<br /><br /> language = "en-us"|

### <a name="child-elements"></a>子要素

|要素|説明|
|-------------|-----------------|
|[なし] :|[なし] :|

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[CommandTable 要素](../extensibility/commandtable-element.md)|VSPackage が IDE に提供するコマンド (メニュー項目、メニュー、ツールバー、およびコンボボックス) を表すすべての要素を定義します。|

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
- [Visual Studio コマンドテーブル (vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
- [Vspackage のユーザーインターフェイス要素の追加方法](../extensibility/internals/how-vspackages-add-user-interface-elements.md)
- [コマンド、メニュー、およびツールバー](../extensibility/internals/commands-menus-and-toolbars.md)
