---
title: '方法: O/R デザイナーで生成されたコードを拡張するMicrosoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-data-tools
ms.topic: conceptual
ms.assetid: d6d1122e-2f55-4607-8d8b-48c3c22600fb
caps.latest.revision: 7
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: a1d60090ca16907e16bb58970d793124c5bb2dec
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72665945"
---
# <a name="how-to-extend-code-generated-by-the-or-designer"></a>方法 : O/R デザイナーで生成されたコードを拡張する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]で生成されたコードは、デザイナー サーフェイスでエンティティ クラスやその他のオブジェクトに変更を加えた場合に再生成されます。 このコードの再生成により、通常、生成されたコードに追加したコードは、デザイナーがコードを再生成するときに上書きされます。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]には、上書きされないコードを追加できる部分クラス ファイルの生成機能が用意されています。 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)]で生成されたコードに独自のコードを追加する例の 1 つとして、LINQ to SQL (エンティティ) クラスへのデータ検証の追加があります。 詳細については、「 [方法: エンティティクラスに検証を追加](../data-tools/how-to-add-validation-to-entity-classes.md)する」を参照してください。

 [!INCLUDE[note_settings_general](../includes/note-settings-general-md.md)]

## <a name="adding-code-to-an-entity-class"></a>エンティティ クラスへのコードの追加

#### <a name="to-create-a-partial-class-and-add-code-to-an-entity-class"></a>部分クラスを作成し、エンティティ クラスにコードを追加するには

1. で、新しい LINQ to SQL クラスファイル (**.dbml** ファイル) を開くか作成し [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。 (**ソリューションエクスプローラー** **.dbml** / で .dbml ファイルをダブルクリックします。**データベースエクスプローラー**。)

2. で、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] 検証を追加するクラスを右クリックし、[ **コードの表示**] をクリックします。

     コード エディターが開き、選択したエンティティ クラスの部分クラスが表示されます。

3. エンティティ クラスの部分クラス宣言内にコードを追加します。

## <a name="adding-code-to-a-datacontext"></a>DataContext へのコードの追加

#### <a name="to-create-a-partial-class-and-add-code-to-a-datacontext"></a>部分クラスを作成し、DataContext にコードを追加するには

1. で、新しい LINQ to SQL クラスファイル (**.dbml** ファイル) を開くか作成し [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] ます。 (**ソリューションエクスプローラー** **.dbml** / で .dbml ファイルをダブルクリックします。**データベースエクスプローラー**。)

2. で、 [!INCLUDE[vs_ordesigner_short](../includes/vs-ordesigner-short-md.md)] デザイナーの空の領域を右クリックし、[コードの **表示**] をクリックします。

     コード エディターが開き、DataContext の部分クラスが表示されます。

3. DataContext の部分クラス宣言内にコードを追加します。

## <a name="see-also"></a>参照
 [Visual Studio の LINQ to SQL ツール](../data-tools/linq-to-sql-tools-in-visual-studio2.md)[チュートリアル: LINQ to SQL クラスの作成 (O-R デザイナー)](https://msdn.microsoft.com/library/35aad4a4-2e8a-46e2-ae09-5fbfd333c233) [LINQ to SQL](https://msdn.microsoft.com/library/73d13345-eece-471a-af40-4cc7a2f11655) [チュートリアル: エンティティクラスへの検証の追加](https://msdn.microsoft.com/library/85b06a02-b2e3-4534-95b8-d077c8d4c1d7)
