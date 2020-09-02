---
title: '方法: XML ドキュメントから XML スキーマを作成する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-xml-tools
ms.topic: conceptual
ms.assetid: 1d6700a9-fd67-4794-8997-399589e99bec
caps.latest.revision: 10
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 59e99320b122424e40da64b530bfe9a84a93eae1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72670928"
---
# <a name="how-to-create-an-xml-schema-from-an-xml-document"></a>方法 : XML ドキュメントから XML スキーマを作成する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

XML エディターを使用することで、XML ドキュメントから XML スキーマ定義言語 (XSD) スキーマを作成することができます。 スキーマがどのように生成されるかは、XML インスタンス ドキュメントによって、次の方法で決定されます。

- XML ドキュメントにスキーマまたはドキュメント型定義 (DTD) が関連付けられていない場合は、新しい XML スキーマを推論するために XML ドキュメント内のデータが使用されます。

- 関連する DTD が XML ドキュメントに含まれている場合は、外部 DTD および内部サブセットが、対応する XML スキーマに変換されます。

- インラインの XDR (XML-Data Reduced) スキーマが XML ドキュメントに含まれている場合は、その XDR スキーマが、対応する XML スキーマに変換されます。

  作成されたスキーマは次に、XML ドキュメントで IntelliSense を利用できるようにするために使用されます。

  スキーマ推論エンジンの詳細については、「 [XML スキーマの推論](https://msdn.microsoft.com/library/b18e7ffd-3c04-482d-9934-ba2f6a59b2c9)」を参照してください。

### <a name="to-create-an-xml-schema"></a>XML スキーマを作成するには

1. XML インスタンス ドキュメントを XML エディターに読み込みます。

2. **ツールバー**の [**スキーマの作成**] ボタンをクリックします。

     XML インスタンス ドキュメントで見つかった名前空間ごとに 1 つの XML スキーマ ドキュメントが作成され、開かれます。 各スキーマは、一時的にその他のファイルとして開かれます。

     スキーマは、ディスクに保存するか、プロジェクトに追加するか、破棄することができます。

    > [!NOTE]
    > [ **スキーマの作成** ] コマンドは、xml エディターのショートカットメニューおよび [ **xml** ] メニューからも使用できます。

## <a name="see-also"></a>参照
 [XML エディター](../xml-tools/xml-editor.md)
