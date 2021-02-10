---
title: Office ドキュメントにクラス ダイアグラムの要素をコピーする
description: クラス デザイナーを使用して、.NET クラス ダイアグラムから他のドキュメントにシェイプをコピーする方法について説明します。シェイプまたはその基になるコードのコピーを取得します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- class diagrams, copying elements to Office documents
- Office documents [Visual Studio]
ms.assetid: c43061ad-d258-46b1-be66-f97a312e86d5
author: TerryGLee
ms.author: tglee
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: d9be1a6dc591757ec261120df917866d5e207f49
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99850244"
---
# <a name="how-to-copy-class-diagram-elements-to-a-microsoft-office-document"></a>方法: Microsoft Office ドキュメントにクラス ダイアグラムの要素をコピーする

図形を .NET クラス図 (*.cd* ファイル) から他のドキュメントにコピーできます。 貼り付け先のドキュメントの種類に基づいて、図形かその基になるコードのどちらかのコピーを入手します。 モデリング プロジェクト内の UML クラス ダイアグラムから図形をコピーするには、「[イメージとしてダイアグラムをエクスポートする](../../modeling/export-diagrams-as-images.md)」を参照してください。

## <a name="copy-a-single-element"></a>1 つの要素をコピーする

図形を右クリックし、**[イメージのコピー]** をクリックします。

## <a name="copy-several-elements"></a>複数の要素をコピーする

1. ダイアグラムで、コピーする図形を選択します。

2. 選択項目を右クリックし、**[イメージのコピー]** をクリックします。

## <a name="copy-all-the-elements-in-a-class-diagram"></a>クラス ダイアグラム内のすべての要素をコピーする

1. ダイアグラム サーフェイスを右クリックし、**[すべて選択]** をクリックするか、**Ctrl + A** キーを押します。

2. **[編集]** メニューで、**[イメージのコピー]** を選択します。

**[イメージのコピー]** の代わりに **[コピー]** を選択することもできます。 **[コピー]** は、イメージを通常のビットマップとしてコピーします。 **[イメージのコピー]** は、イメージをベクター ベースのイメージとしてコピーするので、ほとんどの Office アプリケーションにとってはこちらが向いています。

## <a name="see-also"></a>関連項目

- [方法: クラス ダイアグラムを印刷する](how-to-print-class-diagrams.md)
- [方法: クラス ダイアグラムをイメージとしてエクスポートする](how-to-export-class-diagrams-as-images.md)
