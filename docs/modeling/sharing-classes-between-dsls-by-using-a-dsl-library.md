---
title: DSL ライブラリによる DSL 間でのクラスの共有
description: Visual Studio の視覚化およびモデリング SDK で、別の DSL にインポートできる不完全な DSL 定義を作成する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: e1685fe4fc7db6728ebc1ca6a12e27bb6f42589b
ms.sourcegitcommit: 4d394866b7817689411afee98e85da1653ec42f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2020
ms.locfileid: "97363758"
---
# <a name="sharing-classes-between-dsls-by-using-a-dsl-library"></a>DSL ライブラリによる DSL 間でのクラスの共有
Visual Studio の視覚化およびモデリング SDK では、別の DSL にインポートできる不完全な DSL 定義を作成できます。 これにより、類似するモデルの一般的な部分を考慮することができます。

## <a name="creating-and-using-dsl-libraries"></a>DSL ライブラリの作成と使用

#### <a name="to-create-a-dsl-library"></a>DSL ライブラリを作成するには

1. 新しい DSL プロジェクトを作成し、DSL ライブラリソリューションテンプレートを選択します。

     空のモデルを使用して、単一の DSL プロジェクトが作成されます。

2. ドメインクラス、リレーションシップ、図形などを追加できます。

     ライブラリ内の要素は、1つの埋め込みツリーを形成する必要がありません。

     インポーターが使用できるリレーションシップを定義するには、2つのドメインクラスを作成し、それらの間にリレーションシップを作成します。

     ドメインクラスの **継承修飾子** をに設定することを検討してください `Abstract` 。

3. DSL エクスプローラーで定義した要素 (接続ビルダーなど) を追加できます。

4. 検証制約など、追加のコードを必要とするカスタマイズを追加することができます。

5. [ **すべてのテンプレートの変換**] をクリックします。

6. プロジェクトをビルドします。

7. 他のユーザーが使用できるように DSL を配布する場合は、コンパイルされたアセンブリ (DLL) とファイルの両方を指定する必要があり `DslDefinition.dsl` ます。 コンパイルされたアセンブリは、の下のフォルダーにあります。 `Dsl\bin\*`

#### <a name="to-import-a-dsl-library"></a>DSL ライブラリをインポートするには

1. 別の DSL 定義の **Dsl エクスプローラー** で、dsl のルートクラスを右クリックし、[ **新しい Dsllibrary インポートの追加**] をクリックします。

2. プロパティウィンドウで、ライブラリの **ファイルパス** を設定します。 相対パスと絶対パスのどちらを使用してもかまいません。

    インポートしたライブラリは、DSL エクスプローラーの読み取り専用モードで表示されます。

3. インポートしたクラスを基底クラスとして使用できます。 インポートする DSL にドメインクラスを作成し、プロパティウィンドウで、インポートされたクラスに **基本クラス** を設定します。

4. [すべてのテンプレートの変換] をクリックします。

5. Dsl ライブラリプロジェクトによって作成されたアセンブリ (DLL) への参照を DSL プロジェクトに追加します。

6. ソリューションをビルドします。

   DSL ライブラリは、他のライブラリをインポートできます。 ライブラリをインポートすると、そのインポートも DSL エクスプローラーに自動的に表示されます。

## <a name="see-also"></a>関連項目

- [方法: ドメイン固有言語を定義する](../modeling/how-to-define-a-domain-specific-language.md)

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]
