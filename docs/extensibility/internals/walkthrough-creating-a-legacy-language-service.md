---
title: 'チュートリアル: 従来の言語サービスの作成 |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- language services [managed package framework], creating
ms.assetid: 6a5dd2c2-261b-4efd-a3f4-8fb90b73dc82
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dbdad85dd1c0f62b22bb33b5ed6ab2c597e62164
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905985"
---
# <a name="walkthrough-creating-a-legacy-language-service"></a>チュートリアル: 従来の言語サービスの作成
Managed package framework (MPF) 言語クラスを使用して、言語サービスをに実装するの [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] は簡単です。 言語サービス、言語サービス自体、および言語のパーサーをホストするための VSPackage が必要です。

## <a name="prerequisites"></a>必須コンポーネント
 このチュートリアルを行うには、Visual Studio SDK をインストールする必要があります。 詳細については、「 [Visual STUDIO SDK](../../extensibility/visual-studio-sdk.md)」を参照してください。

## <a name="locations-for-the-visual-studio-package-project-template"></a>Visual Studio パッケージ プロジェクト テンプレートの場所
 Visual Studio パッケージプロジェクトテンプレートは、[**新しいプロジェクト**] ダイアログボックスの3つの異なるテンプレートの場所にあります。

1. Visual Basic の機能拡張の下。 プロジェクトの既定の言語は Visual Basic です。

2. C# の機能拡張の下。 プロジェクトの既定の言語は C# です。

3. その他のプロジェクトの種類の機能拡張の下。 プロジェクトの既定の言語は C++ です。

### <a name="create-a-vspackage"></a>VSPackage を作成する

1. Visual Studio パッケージプロジェクトテンプレートを使用して、新しい VSPackage を作成します。

    既存の VSPackage に言語サービスを追加する場合は、次の手順をスキップし、「言語サービスクラスを作成する」の手順に直接進みます。

2. プロジェクトの名前として「My言語パッケージ」と入力し、[ **OK]** をクリックします。

    任意の名前を使用できます。 ここで説明する手順では、My言語パッケージを名前と想定しています。

3. 言語としてを選択し、 [!INCLUDE[csprcs](../../data-tools/includes/csprcs_md.md)] 新しいキーファイルを生成するオプションを選択します。 **[次へ]** をクリックします。

4. 適切な会社およびパッケージの情報を入力します。 **[次へ]** をクリックします。

5. **メニューコマンド**を選択します。 **[次へ]** をクリックします。

    コードスニペットをサポートしない場合は、[完了] をクリックするだけで、次の手順は無視できます。

6. **コマンド名**として「 **Insert スニペット**」と入力し、 `cmdidInsertSnippet` **コマンド ID**に「」と入力します。 **[完了]** をクリックします。

    **コマンド名**と**コマンド ID**は任意のものにすることができます。これらは例にすぎません。

### <a name="create-the-language-service-class"></a>言語サービスクラスを作成する

1. **ソリューションエクスプローラー**で、My言語パッケージプロジェクトを右クリックし、[**追加**]、[**参照**] の順に選択し、[**新しい参照の追加**] をクリックします。

2. [**参照の追加**] ダイアログボックスで、[ **.net** ] タブの [ **LanguageService** ] を選択し、[ **OK**] をクリックします。

     これは、言語パッケージプロジェクトに対して1回だけ実行する必要があります。

3. **ソリューションエクスプローラー**で、VSPackage プロジェクトを右クリックし、[**追加**]、[**クラス**] の順に選択します。

4. [テンプレート] ボックスの一覧で [**クラス**] が選択されていることを確認します。

5. クラスファイルの名前として「 **MyLanguageService.cs** 」と入力し、[**追加**] をクリックします。

     任意の名前を使用できます。 ここで説明する手順では `MyLanguageService` 、名前としてを想定しています。

6. MyLanguageService.cs ファイルで、次のディレクティブを追加し `using` ます。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#1](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_1.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#1](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_1.vb)]

7. クラス `MyLanguageService` から派生するようにクラスを変更し <xref:Microsoft.VisualStudio.Package.LanguageService> ます。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#2](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_2.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#2](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_2.vb)]

8. "LanguageService" にカーソルを置き、[**編集**] の [ **IntelliSense** ] メニューから [**抽象クラスの実装**] を選択します。 これにより、言語サービスクラスを実装するために必要な最低限のメソッドが追加されます。

9. 「[従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service2.md)」で説明されているように、抽象メソッドを実装します。

### <a name="register-the-language-service"></a>言語サービスを登録する

1. MyLanguagePackagePackage.cs ファイルを開き、次のディレクティブを追加し `using` ます。

     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#3](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_3.vb)]
     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#3](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_3.cs)]

2. 「[従来の言語サービスの登録](../../extensibility/internals/registering-a-legacy-language-service1.md)」の説明に従って、言語サービスクラスを登録します。 これには、属性と "Proffering Language Service" セクションが含まれます。 MyLanguageService を使用します。このトピックでは、TestLanguageService を使用します。

### <a name="the-parser-and-scanner"></a>パーサーとスキャナー

1. 「[従来の言語サービスパーサーとスキャナー](../../extensibility/internals/legacy-language-service-parser-and-scanner.md)」で説明されているように、言語のパーサーとスキャナーを実装します。

     パーサーとスキャナーを実装する方法は、ユーザーによって完全に異なり、このトピックでは扱いません。

## <a name="language-service-features"></a>言語サービスの機能
 言語サービスで各機能を実装するには、通常、適切な MPF 言語サービスクラスからクラスを派生させ、必要に応じて抽象メソッドを実装して、適切なメソッドをオーバーライドします。 作成または派生元のクラスは、サポートする機能によって異なります。 これらの機能については、「[従来の言語サービス機能](../../extensibility/internals/legacy-language-service-features1.md)」で詳しく説明されています。 次の手順は、MPF クラスからクラスを派生させる一般的な方法です。

#### <a name="deriving-from-an-mpf-class"></a>MPF クラスからの派生

1. **ソリューションエクスプローラー**で、VSPackage プロジェクトを右クリックし、[**追加**]、[**クラス**] の順に選択します。

2. [テンプレート] ボックスの一覧で [**クラス**] が選択されていることを確認します。

     クラスファイルに適切な名前を入力し、[**追加**] をクリックします。

3. 新しいクラスファイルで、次のディレクティブを追加し `using` ます。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#4](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_4.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#4](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_4.vb)]

4. 目的の MPF クラスから派生するようにクラスを変更します。

5. 少なくとも基底クラスのコンストラクターと同じパラメーターを受け取り、コンストラクターのパラメーターを基底クラスのコンストラクターに渡すクラスコンストラクターを追加します。

     たとえば、クラスから派生したクラスのコンストラクターは、 <xref:Microsoft.VisualStudio.Package.Source> 次のようになります。

     [!code-csharp[CreatingALanguageService(ManagedPackageFramework)#5](../../extensibility/internals/codesnippet/CSharp/walkthrough-creating-a-legacy-language-service_5.cs)]
     [!code-vb[CreatingALanguageService(ManagedPackageFramework)#5](../../extensibility/internals/codesnippet/VisualBasic/walkthrough-creating-a-legacy-language-service_5.vb)]

6. 基本クラスに実装する必要がある抽象メソッドがある場合は、[**編集**]、[ **IntelliSense** ] メニューの [**抽象クラスの実装**] を選択します。

7. それ以外の場合は、クラス内にカレットを置き、オーバーライドするメソッドを入力します。

     たとえば、「」と入力すると、 `public override` そのクラスでオーバーライド可能なすべてのメソッドの一覧が表示されます。

## <a name="see-also"></a>関連項目
- [従来の言語サービスの実装](../../extensibility/internals/implementing-a-legacy-language-service1.md)
