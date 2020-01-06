---
title: XML スキーマを作成する
ms.date: 03/05/2019
ms.topic: conceptual
ms.assetid: 1d6700a9-fd67-4794-8997-399589e99bec
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 857b75f22d45cbabc22062fd14b385e8f6ea5f14
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75592777"
---
# <a name="how-to-create-an-xml-schema-from-an-xml-document"></a>方法: XML ドキュメントから XML スキーマを作成する

Xml エディターでは、xml ドキュメントから XML スキーマ定義言語 (XSD) スキーマを作成できます。 XML ファイルは、次の方法でスキーマが生成される方法を決定します。

- XML ドキュメントにスキーマまたはドキュメント型定義 (DTD) が関連付けられていない場合は、新しい XML スキーマを推論するために XML ドキュメント内のデータが使用されます。

- 関連する DTD が XML ドキュメントに含まれている場合は、外部 DTD および内部サブセットが、対応する XML スキーマに変換されます。

- インラインの XDR (XML-Data Reduced) スキーマが XML ドキュメントに含まれている場合は、その XDR スキーマが、対応する XML スキーマに変換されます。

次に、作成されたスキーマを使用して、XML ファイルに IntelliSense を提供します。

スキーマ推論エンジンの詳細については、「 [XML スキーマの推論](/dotnet/standard/data/xml/inferring-an-xml-schema)」を参照してください。

## <a name="to-create-an-xml-schema"></a>XML スキーマを作成するには

1. Visual Studio で XML ファイルを開きます。

2. メニューバーで、[ **XML** > **スキーマの作成**] を選択します。

   Xml ファイル内の名前空間ごとに、XML スキーマドキュメントが作成されて開きます。 各スキーマは、一時的にその他のファイルとして開かれます。 スキーマは、ディスクに保存するか、プロジェクトに追加するか、破棄することができます。

## <a name="see-also"></a>関連項目

- [XML エディター](../xml-tools/xml-editor.md)
