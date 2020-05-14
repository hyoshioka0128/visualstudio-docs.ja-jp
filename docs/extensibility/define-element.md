---
title: 要素を定義する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- VSCT XML schema elements, Define
- Define element (VSCT XML schema)
ms.assetid: 5aee74e3-de41-4dc6-9618-93e158af56dd
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fc09de1d822f41b25397c7a56c7cce4449a9e551
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80712269"
---
# <a name="define-element"></a>要素の定義
シンボル名と値のペアを定義します。 このシンボルは、条件属性によって評価できます。 詳細については、「[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。 [「シンボル」要素](../extensibility/symbols-element.md)も参照してください。

## <a name="syntax"></a>構文

```
<Define name="Mode" value="Standard" />
```

## <a name="attributes-and-elements"></a>属性と要素
 以降のセクションでは、属性、子要素、および親要素について説明します。

### <a name="attributes"></a>属性

|属性|説明|
|---------------|-----------------|
|name|必須。 シンボルの名前:<br /><br /> 名前="モード"|
|value|必須。 シンボルの値:<br /><br /> 値="標準"|
|条件|省略可能。 詳細については、「[条件属性](../extensibility/vsct-xml-schema-conditional-attributes.md)」を参照してください。|

### <a name="child-elements"></a>子要素
 [なし] :

### <a name="parent-elements"></a>親要素

|要素|説明|
|-------------|-----------------|
|[コマンド テーブル要素](../extensibility/commandtable-element.md)|統合開発環境 (IDE) に VSPackage が提供するコマンドを表すすべての要素を定義します。 たとえば、メニュー項目、メニュー、ツールバー、コンボ ボックスなどです。|

## <a name="example"></a>例

```
<Define name="DEMO_UI"/>
<Define name="MODE" value="Standard"/>
```

## <a name="see-also"></a>関連項目
- [Visual Studio コマンド テーブル (.vsct) ファイル](../extensibility/internals/visual-studio-command-table-dot-vsct-files.md)
