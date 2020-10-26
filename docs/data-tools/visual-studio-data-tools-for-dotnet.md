---
title: .NET 用のデータ ツール
ms.date: 11/04/2016
ms.topic: overview
ms.assetid: c3175080-1dfb-4ab8-a460-92dadbb844b4
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
- dotnet
ms.openlocfilehash: 67cf4969a5db8900910b375d4cf560b1e30da4eb
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85281072"
---
# <a name="visual-studio-data-tools-for-net"></a>.NET 用の Visual Studio データ ツール

Visual Studio と .NET を共に使用すると、データベースへの接続、メモリ内のデータのモデル化、データのユーザー インターフェイスでの表示などに使用できる、さまざまな API やツールを利用できます。 データへのアクセス機能を提供する .NET クラスは [ADO.NET](/dotnet/framework/data/adonet/index) と呼ばれています。 ADO.NET と Visual Studio のデータ ツールは、主にリレーショナル データベースと XML で使用できるように設計されています。 ADO.NET プロバイダーは、今日、多くのサードパーティの NoSQL データベース ベンダーによって提供されています。

[.NET Core](/dotnet/core/) では、データセットとそれに関連する型を除き、ADO.NET がサポートされています。 .NET Core を対象としていて、オブジェクト リレーショナル マッピング (ORM) レイヤーが必要な場合は、[Entity Framework Core](/ef/core/) を使用してください。

次の図に、基本アーキテクチャを簡略化したものを示します。

![ADO.NET のアーキテクチャ](../data-tools/media/raddata-ado-net-architecture-diagram.png)

## <a name="typical-workflow"></a>一般的なワークフロー

典型的なワークフローは次のとおりです。

1. お使いのローカル コンピューターに、開発データベースまたはテスト データベースをインストールします。 [データベース システム、ツール、およびサンプルのインストール](../data-tools/installing-database-systems-tools-and-samples.md)に関するページを参照してください。 この手順は、Azure データ サービスを使用している場合は必要ありません。

2. Visual Studio でそのデータベース (またはサービスまたはローカル ファイル) への接続をテストします。 [新しい接続の追加](../data-tools/add-new-connections.md)に関するページを参照してください。

3. (省略可能) ツールを使用して、新しいモデルを生成および構成します。 Entity Framework に基づくモデルは、新しいアプリケーションに既定で推奨されています。 いずれのモデルをお使いの場合も、それがアプリケーションによってやり取りをする、データ ソースとなります。 モデルは、データベースまたはサービスとアプリケーションの間に論理的に位置します。 [新しいデータ ソースの追加](../data-tools/add-new-data-sources.md)に関するページを参照してください。

4. **[データ ソース]** ウィンドウからデータ ソースを、Windows フォーム、ASP.NET、または Windows Presentation Foundation のデザイン サーフェイスにドラッグし、指定の方法でユーザーにデータを表示するデータ バインディング コードを生成します。 [Visual Studio でのデータへのコントロールのバインド](../data-tools/bind-controls-to-data-in-visual-studio.md)に関するページを参照してください。

5. ビジネス ルール、検索、データ検証などのカスタム コードを追加したり、基になるデータベースで公開されているカスタム機能を利用したりすることができます。

手順 3 は省略し、モデルを使用せず、.NET アプリケーションをプログラミングし、コマンドをデータベースに直接発行することができます。 この場合は、ここで、関連するドキュメントが表示されます: [ADO.NET](/dotnet/framework/data/adonet/index)します。 メモリに自分独自のオブジェクトを指定し、それらのオブジェクトに UI コントロールをデータバインドするとき、引き続き **[データ ソース構成ウィザード]** とデザイナーを使用してデータ バインディング コードを作成することも可能です。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
