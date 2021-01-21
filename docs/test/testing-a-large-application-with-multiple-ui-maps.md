---
title: 複数の UI マップで大規模アプリケーションをテストする
description: 複数の UI マップを使用して大規模なアプリケーションをテストする際に、コード化された UI テストを使用する方法を説明します。 この機能には、Visual Studio Enterprise が必要です。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- coded UI tests, multiple UI maps
- coded UI tests, for large applications
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 93ae6aaa77a133a0d1805554a38b2714bff5b312
ms.sourcegitcommit: 9ce13a961719afbb389fa033fbb1a93bea814aae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/30/2020
ms.locfileid: "96330161"
---
# <a name="test-a-large-application-with-multiple-ui-maps"></a>複数の UI マップで大規模アプリケーションをテストする

このトピックでは、複数の UI マップを使って大規模なアプリケーションをテストする際に、コード化された UI テストを使用する方法を説明します。

[!INCLUDE [coded-ui-test-deprecation](includes/coded-ui-test-deprecation.md)]

**必要条件**

- Visual Studio Enterprise

新しいコード化された UI テストを作成すると、Visual Studio テスト フレームワークによってテスト用のコードが生成されます。既定では、このコードは [UIMap](/previous-versions/dd580454(v=vs.140)) クラスに生成されます。 コード化された UI テストを記録する方法の詳細については、「[コード化された UI テストを作成する](../test/use-ui-automation-to-test-your-code.md)」および「[コード化された UI テストの構造](../test/anatomy-of-a-coded-ui-test.md)」を参照してください。

UI マップに対して生成されるコードには、テストで操作する各オブジェクトに対応するクラスが含まれます。 生成されるメソッドごとに、そのメソッドに固有のメソッド パラメーターのコンパニオン クラスが生成されます。 アプリケーションで多数のオブジェクト、ページ、フォーム、およびコントロールが使用されていると、UI マップがかなりの大きさになる場合があります。 また、複数のテスト担当者で作業する場合、単一の大きな UI マップ ファイルでは、アプリケーションを扱いきれなくなります。

複数の UI マップ ファイルを使用すると、次のような利点があります。

- 各マップを、アプリケーションの論理的なサブセットに関連付けることができます。 このようにすると、変更を管理しやすくなります。

- 各テスト担当者が、それぞれアプリケーションの特定のセクションに取り組んで、アプリケーションの他のセクションで作業するテスト担当者に干渉することなく担当のコードをチェックインできます。

- アプリケーション UI への追加をインクリメンタル方式で行えるため、UI の他の部分のテストに与える影響が最小限になります。

## <a name="do-you-need-multiple-ui-maps"></a>複数の UI マップが必要な場合
次のような場合には、それぞれに複数の UI マップを作成してください。

- 互いに関連して論理演算を実行する複雑な複合 UI コントロールのセットが複数ある場合 (Web サイトでの登録ページや、買い物カゴの購入ページなど)。

- アプリケーションのさまざまな時点でアクセスする、独立したコントロールのセットがある場合 (複数の操作ページからなるウィザードなど)。 ウィザードのそれぞれのページが非常に複雑な場合には、ページごとに個別の UI マップを作成することもできます。

## <a name="add-multiple-ui-maps"></a>複数の UI マップを追加する

### <a name="to-add-a-ui-map-to-your-coded-ui-test-project"></a>コード化された UI テスト プロジェクトに UI マップを追加するには

1. **ソリューション エクスプローラー** で、コード化された UI テスト プロジェクト内にすべての UI マップを格納するフォルダーを作成します。それには、コード化された UI テスト プロジェクト ファイルを右クリックし、 **[追加]** をポイントして、 **[新しいフォルダー]** を選択します。 たとえば、`UIMaps` という名前を付けます。

    コード化された UI テスト プロジェクトの下に、新しいフォルダーが表示されます。

2. `UIMaps` フォルダーを右クリックし、**[追加]** をポイントして、**[新しい項目]** をクリックします。

    **[新しい項目の追加]** ダイアログ ボックスが表示されます。

   > [!NOTE]
   > 新しいコード化された UI テスト マップを追加するには、コード化されたテスト プロジェクト内で操作する必要があります。

3. リストから **[コード化された UI テスト マップ]** を選択します。

    **[名前]** ボックスに、新しい UI マップの名前を入力します。 マップが表すコンポーネントまたはページの名前を使用してください (例: `HomePageMap`)。

4. **[追加]** をクリックします。

    Visual Studio ウィンドウが最小化されて、**[コード化された UI テスト ビルダー]** ダイアログ ボックスが表示されます。

5. 最初のメソッドのアクションを記録して、**[コードの生成]** を選択します。

6. 最初のコンポーネントまたはページのすべてのアクションおよびアサーションを記録して、メソッド別にグループ化します。この作業が完了したら、**[コード化された UI テスト ビルダー]** ダイアログ ボックスを閉じます。

7. UI マップの作成を続けます。 アクションとアサーションを記録し、各コンポーネントのメソッド別にグループ化した後、コードを生成します。

   多くの場合、アプリケーションの最上位レベルのウィンドウは、すべてのウィザード、フォーム、ページで共有されます。 各 UI マップに、最上位レベルのウィンドウに対応するクラスがありますが、通常は、いずれのマップも同じ最上位レベルのウィンドウ (アプリケーションの全コンポーネントが実行されるウィンドウ) を参照しているはずです。 コード化された UI テストでは、最上位レベルのウィンドウから下に向かって、階層的にコントロールを検索します。そのため、複雑なアプリケーションでは、実際の最上位レベルのウィンドウが、すべての UI マップで複製される可能性があります。 実際の最上位レベルのウィンドウが複製されていると、そのウィンドウが変更された場合、そのウィンドウが複製されている UI マップごとに変更を繰り返さなければなりません。 したがって、UI マップを切り替えるときにパフォーマンスの問題が発生する可能性があります。

   この影響を最小限に抑えるには、UI マップの新しい最上位レベルのウィンドウが、メインの最上位レベルのウィンドウと同じになるように、`CopyFrom()` メソッドを使用することができます。

## <a name="example"></a>例

この例は、さまざまな UI マップで生成されるクラスによって表される各コンポーネントとその子コントロールにアクセスするユーティリティ クラスの一部です。

この例の `Contoso` という名前の Web アプリケーションには、ホーム ページ、製品ページ、買い物カゴ ページがあります。 これらのページのそれぞれが、同じ最上位レベルのウィンドウ (ブラウザー ウィンドウ) を共有しています。 ページごとに UI マップがあります。ユーティリティ クラスのコードは以下のようになります。

```csharp
using ContosoProject.UIMaps;
using ContosoProject.UIMaps.HomePageClasses;
using ContosoProject.UIMaps.ProductPageClasses;
using ContosoProject.UIMaps.ShoppingCartClasses;

namespace ContosoProject
{
    public class TestRunUtility
    {
        // Private fields for the properties
        private HomePage homePage = null;
        private ProductPage productPage = null;
        private ShoppingCart shoppingCart = null;

        public TestRunUtility()
        {
            homePage = new HomePage();
        }

        // Properties that get each UI Map
        public HomePage HomePage
        {
            get { return homePage; }
            set { homePage = value; }
        }

        // Gets the ProductPage from the ProductPageMap.
        public ProductPage ProductPageObject
        {
            get
            {
                if (productPage == null)
                {
                    // Instantiate a new page from the UI Map classes
                    productPage = new ProductPage();

                    // Since the Product Page and Home Page both use
                    // the same browser page as the top level window,
                    // get the top level window properties from the
                    // Home Page.
                    productPage.UIContosoFinalizeWindow.CopyFrom(
                        HomePage.UIContosoWindowsIWindow);
                }
                return productPage;
            }
        }

    // Continue to create properties for each page, getting the
    // page object from the corresponding UI Map and copying the
    // top level window properties from the Home Page.
}
```

## <a name="see-also"></a>関連項目

- [UIMap](/previous-versions/dd580454(v=vs.140))
- <xref:Microsoft.VisualStudio.TestTools.UITesting.BrowserWindow.CopyFrom%2A>
- [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)
- [コード化された UI テストを作成する](../test/use-ui-automation-to-test-your-code.md)
- [コード化された UI テストの構造](../test/anatomy-of-a-coded-ui-test.md)
