---
title: 型指定されたデータセットと型指定されていないデータセットの比較
description: 型指定されたデータセットと型指定されていないデータセットの違いを理解する 型指定されたデータセットと型指定されていないデータセットでのデータアクセス
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
ms.assetid: c83ba0bb-5425-4d47-8891-6b4dbf937701
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: b2dc8d78f42d210741c904e3e475be33f2443e74
ms.sourcegitcommit: 72a49c10a872ab45ec6c6d7c4ac7521be84526ff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/20/2020
ms.locfileid: "94998058"
---
# <a name="typed-vs-untyped-datasets"></a>型指定されたデータセットと型指定されていないデータセットの比較
型指定されたデータセットは、最初に基本クラスから派生したデータセットで <xref:System.Data.DataSet> あり、 **データセットデザイナー** の情報を使用して .xsd ファイルに格納され、新しい厳密に型指定された dataset クラスを生成します。 スキーマ (テーブル、列など) からの情報が生成され、この新しいデータセットクラスとして、ファーストクラスのオブジェクトとプロパティのセットとしてコンパイルされます。 型指定されたデータセットは基本クラスから継承するため、 <xref:System.Data.DataSet> 型指定されたクラスはクラスのすべての機能を前提 <xref:System.Data.DataSet> としており、クラスのインスタンスをパラメーターとして受け取るメソッドで使用でき <xref:System.Data.DataSet> ます。

これに対し、型指定されていないデータセットには、対応する組み込みスキーマがありません。 型指定されたデータセットと同様に、型指定されていないデータセットにはテーブルや列などが含まれますが、これらはコレクションとしてのみ公開されます。 (ただし、型指定されていないデータセットのテーブルおよびその他のデータ要素を手動で作成した後は、データセットのメソッドを使用して、データセットの構造をスキーマとしてエクスポートでき <xref:System.Data.DataSet.WriteXmlSchema%2A> ます)。

## <a name="contrast-data-access-in-typed-and-untyped-datasets"></a>型指定され、型指定されていないデータセットでのデータアクセスのコントラスト
型指定されたデータセットのクラスには、そのプロパティがテーブルと列の実際の名前を取得するオブジェクトモデルがあります。 たとえば、型指定されたデータセットを操作する場合は、次のようなコードを使用して列を参照できます。

[!code-csharp[VbRaddataDatasets#4](../data-tools/codesnippet/CSharp/typed-vs-untyped-datasets_1.cs)]
[!code-vb[VbRaddataDatasets#4](../data-tools/codesnippet/VisualBasic/typed-vs-untyped-datasets_1.vb)]

これに対し、型指定されていないデータセットを使用している場合、同等のコードは次のようになります。

[!code-csharp[VbRaddataDatasets#5](../data-tools/codesnippet/CSharp/typed-vs-untyped-datasets_2.cs)]
[!code-vb[VbRaddataDatasets#5](../data-tools/codesnippet/VisualBasic/typed-vs-untyped-datasets_2.vb)]

型指定されたアクセスは、読みやすくなるだけでなく、Visual Studio **コードエディター** の IntelliSense でも完全にサポートされています。 操作が簡単になるだけでなく、型指定されたデータセットの構文では、コンパイル時に型チェックが行われるため、データセットのメンバーに値を代入する際にエラーが発生する可能性が大幅に減少します。 クラスの列の名前を変更して <xref:System.Data.DataSet> からアプリケーションをコンパイルすると、ビルドエラーが発生します。 **タスク一覧** でビルドエラーをダブルクリックすると、古い列名を参照する行またはコード行に直接進むことができます。 実行時には、型指定されたデータセット内のテーブルおよび列へのアクセスも、実行時に多少高速になります。これは、実行時にコレクションを使用するのではなく、コンパイル時にアクセスが決定されるためです。

型指定されたデータセットには多くの利点がありますが、型指定されていないデータセットはさまざまな状況で役立ちます。 最も明白なシナリオは、データセットで使用できるスキーマがない場合です。 このような状況が発生する可能性があります。たとえば、アプリケーションがデータセットを返すコンポーネントを操作していても、その構造を事前に把握していない場合などです。 同様に、静的な予測可能な構造を持たないデータを操作する場合もあります。 この場合、型指定されたデータセットを使用するのは現実的ではありません。これは、データ構造の変更を行うたびに、型指定された dataset クラスを再生成する必要があるためです。

一般に、スキーマを使用しなくても、データセットを動的に作成する場合が多くあります。 その場合、データをリレーショナルな方法で表現できる限り、データセットは単に便利な構造になり、情報を保持することができます。 同時に、データセットの機能を利用して、別のプロセスに渡す情報をシリアル化したり、XML ファイルを書き出したりすることができます。

## <a name="see-also"></a>こちらもご覧ください

- [データセットツール](../data-tools/dataset-tools-in-visual-studio.md)
