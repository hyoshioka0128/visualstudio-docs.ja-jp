---
title: 'チュートリアル: 従来の言語サービスの作成 |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- language services [managed package framework], creating
ms.assetid: 6a5dd2c2-261b-4efd-a3f4-8fb90b73dc82
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 59ec18ab0c97ec89422e06f5b33804adcc750d5a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80703684"
---
# <a name="walkthrough-creating-a-legacy-language-service"></a>チュートリアル: 従来の言語サービスの作成
マネージ パッケージ フレームワーク (MPF) 言語クラスを使用して、[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]言語サービスを実装するのは簡単です。 言語サービス、言語サービス自体、および言語のパーサーをホストする VSPackage が必要です。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual Studio SDK](../../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio パッケージ プロジェクト テンプレートの場所
 Visual Studio パッケージ プロジェクト テンプレートは、[**新しいプロジェクト**] ダイアログ ボックスの 3 つの異なるテンプレートの場所にあります。

1. Visual Basic の機能拡張の下。 プロジェクトの既定の言語は Visual Basic です。

2. C# の機能拡張の下。 プロジェクトの既定の言語は C# です。

3. その他のプロジェクトの種類の機能拡張の下。 プロジェクトの既定の言語は C++ です。

### <a name="create-a-vspackage"></a>VS パッケージの作成

1. Visual Studio パッケージ プロジェクト テンプレートを使用して新しい VSPackage を作成します。

    既存の VSPackage に言語サービスを追加する場合は、次の手順をスキップして、「言語サービス クラスの作成」の手順に直接進みます。

2. プロジェクトの名前として MyLanguagePackage と入力し **、[OK]** をクリックします。

    任意の名前を使用できます。 ここで説明するこれらの手順では、名前として MyLanguagePackage を想定しています。

3. 言語[!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)]として選択し、新しいキーファイルを生成するオプションを選択します。 **[次へ]** をクリックします。

4. 適切な会社情報とパッケージ情報を入力します。 **[次へ]** をクリックします。

5. メニュー**コマンド を**選択します。 **[次へ]** をクリックします。

    コード スニペットをサポートしない場合は、[完了] をクリックして次の手順を無視します。

6. **コマンド名**として、コマンド**ID**`cmdidInsertSnippet`に **「スニペットを挿入**」と入力します。 **[完了]** をクリックします。

    **コマンド名**と**コマンド ID**は、必要に応じて指定できます。

### <a name="create-the-language-service-class"></a>言語サービス クラスの作成

1. **ソリューション エクスプローラー**で、MyLanguagePackage プロジェクトを右クリックし、[**追加**]、[**参照**] の順に選択し、[**新しい参照の追加**] ボタンをクリックします。

2. [**参照の追加**] ダイアログ ボックスで **、[.NET]** タブで **[Microsoft.VisualStudio.Package.LanguageService]** を選択し **、[OK]** をクリックします。

     これは、言語パッケージ プロジェクトに対して 1 回だけ行う必要があります。

3. **ソリューション エクスプローラー**で、VSPackage プロジェクトを右クリックし、[**追加**] の [**クラス**] をクリックします。

4. テンプレートリストで **[クラス**]が選択されていることを確認します。

5. クラス ファイルの名前を**MyLanguageService.cs**入力し、[**追加**] をクリックします。

     任意の名前を使用できます。 ここで説明するこれらの手順`MyLanguageService`は、名前を想定しています。

6. MyLanguageService.cs ファイルに、次`using`のディレクティブを追加します。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#1](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_1.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#1](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_1.vb)]

7. クラスから`MyLanguageService`派生するようにクラスを<xref:Microsoft.VisualStudio.Package.LanguageService>変更します。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#2](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_2.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#2](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_2.vb)]

8. "LanguageService" にカーソルを合わせ、[**編集]** メニューの **[IntelliSense]** メニューの [**抽象クラスの実装**] をクリックします。 これにより、言語サービス クラスを実装するために必要な最小限のメソッドが追加されます。

9. [「レガシ言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)」の説明に従って、抽象メソッドを実装します。

### <a name="register-the-language-service"></a>言語サービスの登録

1. MyLanguagePackagePackage.csファイルを開き、次`using`のディレクティブを追加します。

     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#3](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_3.vb)]
     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#3](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_3.cs)]

2. 「レガシ言語サービスの登録」の説明に従って[、言語サービスクラスを登録](../../extensibility/internals/registering-a-legacy-language-service1.md)します。 これには、ProvideXX 属性と「言語サービスの提供」セクションが含まれます。 このトピックでテスト言語サービスを使用する場合は、MyLanguageService を使用します。

### <a name="the-parser-and-scanner"></a>パーサーとスキャナー

1. 「レガシ言語サービス パーサーおよびスキャナ」で説明されているように、使用している言語用の[パーサーとスキャナを](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)実装します。

     パーサーとスキャナーの実装方法は、完全にユーザーに任され、このトピックの範囲を超えています。

## <a name="language-service-features"></a>言語サービスの機能
 言語サービスで各機能を実装するには、通常、適切な MPF 言語サービス クラスからクラスを派生させ、必要に応じて抽象メソッドを実装し、適切なメソッドをオーバーライドします。 作成または派生元のクラスは、サポートする必要がある機能によって異なります。 これらの機能については、「[レガシ言語サービスの機能](../../extensibility/internals/legacy-language-service-features1.md)」で詳しく説明します。 次の手順は、MPF クラスからクラスを派生するための一般的なアプローチです。

#### <a name="deriving-from-an-mpf-class"></a>MPF クラスから派生する

1. **ソリューション エクスプローラー**で、VSPackage プロジェクトを右クリックし、[**追加**] の [**クラス**] をクリックします。

2. テンプレートリストで **[クラス**]が選択されていることを確認します。

     クラス ファイルに適した名前を入力し、[**追加**] をクリックします。

3. 新しいクラス ファイルに、次`using`のディレクティブを追加します。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#4](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_4.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#4](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_4.vb)]

4. 目的の MPF クラスから派生するようにクラスを変更します。

5. 基本クラスのコンストラクターと同じパラメーターを受け取り、そのコンストラクター パラメーターを基本クラスのコンストラクターに渡すクラス コンストラクターを追加します。

     たとえば、<xref:Microsoft.VisualStudio.Package.Source>クラスから派生したクラスのコンストラクターは、次のようになります。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#5](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_5.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#5](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_5.vb)]

6. 基本クラスに実装する必要のある抽象メソッドがある場合は、[**編集]** の **[IntelliSense]** メニューから [**抽象クラスの実装**] を選択します。

7. それ以外の場合は、クラス内にキャレットを配置し、オーバーライドするメソッドを入力します。

     たとえば、クラスで`public override`オーバーライドできるすべてのメソッドの一覧を表示するには、型を入力します。

## <a name="see-also"></a>関連項目
- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)
