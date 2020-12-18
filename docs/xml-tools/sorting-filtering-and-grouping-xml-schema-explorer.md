---
title: 並べ替え、フィルター処理、およびグループ化
description: XML スキーマ エクスプローラーのツール バーの並べ替え、フィルター処理、グループ化のオプション メニューで使用できるオプションについて学習します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 4a914de0-9ffc-4526-9603-92e460e52513
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 41f0aff39350b0307db6b02a148fb70022fb51ca
ms.sourcegitcommit: d10f37dfdba5d826e7451260c8370fd1efa2c4e4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2020
ms.locfileid: "96996254"
---
# <a name="sorting-filtering-and-grouping-xml-schema-explorer"></a>並べ替え、フィルター処理、およびグループ化 (XML スキーマ エクスプローラー)

このトピックでは、**XML スキーマ エクスプローラー** のツール バーの **[並べ替え、フィルター処理、およびグループ化オプション]** メニューで使用できるオプションについて説明します。

## <a name="filter-options"></a>フィルター オプション

次のフィルター オプションがあります。 既定では、 **[名前空間の表示]** オプションと **[スキーマ ファイルの表示]** オプションが選択されます。

- **[名前空間の表示]** 。

- **[スキーマ ファイルの表示]** 。

- **[コンポジターの表示 (sequence/choice/all)]** 。

## <a name="sorting-options"></a>並べ替えオプション

次の並べ替えオプションがあります。 既定の設定は、 **[種類で並べ替え]** です。 ファイルと名前空間には、 **[並べ替え]** オプションは適用されません。

- **[種類で並べ替え]** 。

- **[名前で並べ替え]** 。

- **[ドキュメントの順序]** 。

### <a name="sort-by-type"></a>[種類で並べ替え]

**[種類で並べ替え]** オプションが選択されている場合、グローバル ノードは次の順序で並べ替えられます。 さらに、各グループ内でアルファベット順に並べ替えられます。

1. `import` ノード

2. `include` ノード

3. `redefine` ノード

4. `attribute` ノード

5. `attributeGroup` ノード

6. `complexType` ノード

7. `simpleType` ノード

8. `element` ノード

9. `group` ノード

### <a name="sort-by-name"></a>[名前で並べ替え]

**[名前で並べ替え]** オプションが選択されている場合、グローバル ノードは次の順序で並べ替えられます。

1. `import` ノード (名前空間のアルファベット順)。

2. `include` ノード (`schemaLocation` 属性のアルファベット順)

3. `redefine` ノード (`schemaLocation` 属性のアルファベット順)

4. その他のグローバル ノード (アルファベット順)

### <a name="document-order"></a>[ドキュメントの順序]

**[ドキュメントの順序]** オプションは、 **[スキーマ ファイルの表示]** オプションが選択されている場合に使用できます。 **[ドキュメントの順序]** が選択されている場合、グローバル ノードはスキーマ ファイル内での順序で表示されます。

## <a name="persisting-sortfilter-options"></a>並べ替えおよびフィルター オプションの保存

設定の変更時に開かれていたソリューションやファイルにかかわらず、並べ替え、フィルター処理、およびグループ化のオプションは各ユーザーのレジストリに保存されます。
