---
title: 型指定されたデータセットと型指定されていないデータセットの比較
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
ms.openlocfilehash: 430e57713f1bfb01219ea1ac8123f321ba0f5680
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586108"
---
# <a name="typed-vs-untyped-datasets"></a>型指定されたデータセットと型指定されていないデータセットの比較
型指定されたデータセットは、最初に基本 <xref:System.Data.DataSet> クラスから派生したデータセットであり、その後、.xsd ファイルに格納されている**データセットデザイナー**の情報を使用して、厳密に型指定された新しいデータセットクラスを生成します。 スキーマ (テーブル、列など) からの情報が生成され、この新しいデータセットクラスとして、ファーストクラスのオブジェクトとプロパティのセットとしてコンパイルされます。 型指定されたデータセットは基本 <xref:System.Data.DataSet> クラスから継承するため、型指定されたクラスは、<xref:System.Data.DataSet> クラスのすべての機能を前提とし、<xref:System.Data.DataSet> クラスのインスタンスをパラメーターとして受け取るメソッドで使用できます。

これに対し、型指定されていないデータセットには、対応する組み込みスキーマがありません。 型指定されたデータセットと同様に、型指定されていないデータセットにはテーブルや列などが含まれますが、これらはコレクションとしてのみ公開されます。 (ただし、型指定されていないデータセットのテーブルおよびその他のデータ要素を手動で作成した後は、データセットの <xref:System.Data.DataSet.WriteXmlSchema%2A> メソッドを使用して、データセットの構造をスキーマとしてエクスポートできます)。

## <a name="contrast-data-access-in-typed-and-untyped-datasets"></a>型指定され、型指定されていないデータセットでのデータアクセスのコントラスト
型指定されたデータセットのクラスには、そのプロパティがテーブルと列の実際の名前を取得するオブジェクトモデルがあります。 たとえば、型指定されたデータセットを操作する場合は、次のようなコードを使用して列を参照できます。

[!code-csharp[VbRaddataDatasets#4](../data-tools/codesnippet/CSharp/typed-vs-untyped-datasets_1.cs)]
[!code-vb[VbRaddataDatasets#4](../data-tools/codesnippet/VisualBasic/typed-vs-untyped-datasets_1.vb)]

これに対し、型指定されていないデータセットを使用している場合、同等のコードは次のようになります。

[!code-csharp[VbRaddataDatasets#5](../data-tools/codesnippet/CSharp/typed-vs-untyped-datasets_2.cs)]
[!code-vb[VbRaddataDatasets#5](../data-tools/codesnippet/VisualBasic/typed-vs-untyped-datasets_2.vb)]

型指定されたアクセスは、読みやすくなるだけでなく、Visual Studio**コードエディター**の IntelliSense でも完全にサポートされています。 操作が簡単になるだけでなく、型指定されたデータセットの構文では、コンパイル時に型チェックが行われるため、データセットのメンバーに値を代入する際にエラーが発生する可能性が大幅に減少します。 <xref:System.Data.DataSet> クラスの列の名前を変更してからアプリケーションをコンパイルすると、ビルドエラーが発生します。 **タスク一覧**でビルドエラーをダブルクリックすると、古い列名を参照する行またはコード行に直接進むことができます。 実行時には、型指定されたデータセット内のテーブルおよび列へのアクセスも、実行時に多少高速になります。これは、実行時にコレクションを使用するのではなく、コンパイル時にアクセスが決定されるためです。

型指定されたデータセットには多くの利点がありますが、型指定されていないデータセットはさまざまな状況で役立ちます。 最も明白なシナリオは、データセットで使用できるスキーマがない場合です。 このような状況が発生する可能性があります。たとえば、アプリケーションがデータセットを返すコンポーネントを操作していても、その構造を事前に把握していない場合などです。 同様に、静的な予測可能な構造を持たないデータを操作する場合もあります。 この場合、型指定されたデータセットを使用するのは現実的ではありません。これは、データ構造の変更を行うたびに、型指定された dataset クラスを再生成する必要があるためです。

一般に、スキーマを使用しなくても、データセットを動的に作成する場合が多くあります。 その場合、データをリレーショナルな方法で表現できる限り、データセットは単に便利な構造になり、情報を保持することができます。 同時に、データセットの機能を利用して、別のプロセスに渡す情報をシリアル化したり、XML ファイルを書き出したりすることができます。

## <a name="see-also"></a>関連項目

- [データセットのツール](../data-tools/dataset-tools-in-visual-studio.md)
