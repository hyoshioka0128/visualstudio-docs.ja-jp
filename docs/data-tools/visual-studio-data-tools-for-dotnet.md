---
title: .NET 用データツール
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: c3175080-1dfb-4ab8-a460-92dadbb844b4
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
- dotnet
ms.openlocfilehash: 1dcd8c256259baeef36939e19ce785e5efe7c80b
ms.sourcegitcommit: d233ca00ad45e50cf62cca0d0b95dc69f0a87ad6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/01/2020
ms.locfileid: "75586043"
---
# <a name="visual-studio-data-tools-for-net"></a>.NET 用の Visual Studio データ ツール

Visual Studio と .NET では、データベースへの接続、メモリ内のデータのモデル化、ユーザーインターフェイスでのデータの表示など、さまざまな API とツールがサポートされています。 データアクセス機能を提供する .NET クラスは、 [ADO.NET](/dotnet/framework/data/adonet/index)と呼ばれています。 ADO.NET は、Visual Studio のデータツールと共に、主にリレーショナルデータベースと XML をサポートするように設計されています。 これらの日、多くの NoSQL データベースベンダー、またはサードパーティが ADO.NET プロバイダーを提供しています。

[.Net Core](/dotnet/core/)は、データセットとそれに関連する型を除き、ADO.NET をサポートしています。 .NET Core を対象としていて、オブジェクトリレーショナルマッピング (ORM) レイヤーが必要な場合は、 [Entity Framework Core](/ef/core/)を使用します。

次の図は、基本的なアーキテクチャの簡略化されたビューを示しています。

![ADO.NET のアーキテクチャ](../data-tools/media/raddata-ado-net-architecture-diagram.png)

## <a name="typical-workflow"></a>一般的なワークフロー

一般的なワークフローは次のとおりです。

1. 開発データベースまたはテストデータベースをローカルコンピューターにインストールします。 「[データベースシステム、ツール、サンプルのインストール](../data-tools/installing-database-systems-tools-and-samples.md)」を参照してください。 Azure データサービスを使用している場合、この手順は必要ありません。

2. Visual Studio でデータベース (またはサービスまたはローカルファイル) への接続をテストします。 「[新しい接続の追加](../data-tools/add-new-connections.md)」を参照してください。

3. Optionalツールを使用して、新しいモデルを生成して構成します。 Entity Framework に基づくモデルは、新しいアプリケーションの既定の推奨事項です。 使用するモデルはいずれも、アプリケーションがやり取りするデータソースです。 モデルは、データベースまたはサービスとアプリケーションの間で論理的に配置されます。 「[新しいデータソースの追加](../data-tools/add-new-data-sources.md)」を参照してください。

4. データソースを **[データソース]** ウィンドウから Windows フォーム、ASP.NET、または Windows Presentation Foundation デザインサーフェイスにドラッグして、指定した方法でユーザーにデータを表示するデータバインドコードを生成します。 「 [Visual Studio でのデータへのコントロールのバインド」を](../data-tools/bind-controls-to-data-in-visual-studio.md)参照してください。

5. ビジネスルール、検索、データ検証などのカスタムコードを追加したり、基になるデータベースが公開するカスタム機能を利用したりできます。

モデルを使用するのではなく、手順3をスキップし、.NET アプリケーションをプログラミングして、コマンドをデータベースに直接発行することができます。 この場合は、ここで、関連するドキュメントが表示されます: [ADO.NET](/dotnet/framework/data/adonet/index)します。 ただし、**データソース構成ウィザード**とデザイナーを使用して、メモリ内に独自のオブジェクトを設定し、それらのオブジェクトに UI コントロールをデータバインドするときに、データバインディングコードを生成することができます。

## <a name="see-also"></a>関連項目

- [Visual Studio でのデータへのアクセス](../data-tools/accessing-data-in-visual-studio.md)
