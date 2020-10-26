---
title: Windows Communication Foundation と WCF Data Services
ms.date: 11/04/2016
ms.topic: overview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- services, WCF Data
- WCF services, binding to
- WCF services, asynchronous service methods
- service references [Visual Studio]
- WCF Data Services
- asynchronous calls
- service references [Visual Studio], type sharing
- endpoints [WCF]
- asynchronous service methods
- service references [Visual Studio] endpoints
- WCF services, type sharing
- Windows Communication Foundation, in Visual Studio
- services, WCF
- WCF service, Visual Studio
- data services, WCF
- services, in Visual Studio
- data binding [Visual Studio], WCF
- service endpoints [Visual Studio]
- service references [Visual Studio], asynchronous calls
- services, Windows Communication Foundation
- type sharing in WCF services
- WCF services, endpoints
- service method, called asynchronously[Visual Studio]
ms.assetid: d56f12cb-e139-4fec-b3e4-488383356642
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- data-storage
ms.openlocfilehash: c1f24a33a482b1994d0d8667b4fc71cf968e4625
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85281046"
---
# <a name="windows-communication-foundation-services-and-wcf-data-services-in-visual-studio"></a>Visual Studio での Windows Communication Foundation サービスと WCF データ サービス

Visual Studio では、分散型アプリケーションを作成するための Microsoft テクノロジである Windows Communication Foundation (WCF) と WCF Data Services で作業するためのツールを提供します。 このトピックでは、Visual Studio の観点から、これらのサービスの概要を説明します。 完全なドキュメントについては、「[WCF Data Services 4.5](/dotnet/framework/data/wcf/index)」を参照してください。

## <a name="what-is-wcf"></a>WCF とは

Windows Communication Foundation (WCF) は、セキュリティで保護され、信頼性が高く、トランザクションに対応し、相互運用可能な分散型アプリケーションを作成するための統合フレームワークです。 これは、ASMX Web サービス、.NET リモート処理、エンタープライズサービス (DCOM)、MSMQ などの古いプロセス間通信テクノロジに代わるものです。 WCF により、これらのすべてのテクノロジの機能が統一プログラミング モデルの下に統合され、 分散型アプリケーションの開発エクスペリエンスが簡素化されます。

### <a name="what-are-wcf-data-services"></a>WCF Data Services とは

WCF Data Services は、Open Data (OData) Protocol 標準の実装です。  WCF Data Services では、表形式データが一連の REST API として公開されるため、GET、POST、PUT、DELETE などの標準的な HTTP 動詞を使用してデータを返すことができます。 サーバー側では、新しい OData サービスを作成するための [ASP.NET Web API](https://dotnet.microsoft.com/apps/aspnet/apis) によって WCF Data Services が置き換えられます。 WCF Data Services クライアント ライブラリは引き続き、Visual Studio ( **[プロジェクト]**  >  **[サービス参照の追加]** ) から .NET アプリケーションの OData サービスを使用するのに適しています。 詳細については、「[WCF Data Services 4.5](/dotnet/framework/data/wcf)」を参照してください。

### <a name="wcf-programming-model"></a>WCF プログラミング モデル

WCF プログラミング モデルは、2 つのエンティティ (WCF サービスと WCF クライアント) 間の通信に基づきます。 このプログラミング モデルは、.NET の <xref:System.ServiceModel> 名前空間にカプセル化されます。

### <a name="wcf-service"></a>WCF サービス

WCF サービスは、サービスとクライアント間のコントラクトを定義するインターフェイスに基づきます。 次のコードに示すように、これは、<xref:System.ServiceModel.ServiceContractAttribute> 属性でマークされます。

[!code-csharp[WCFWalkthrough#6](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_1.cs)]
[!code-vb[WCFWalkthrough#6](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_1.vb)]

WCF サービスによって公開される関数またはメソッドは、<xref:System.ServiceModel.OperationContractAttribute> 属性でマークすることによって定義します。

[!code-csharp[WCFWalkthrough#1](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_2.cs)]
[!code-vb[WCFWalkthrough#1](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_2.vb)]

さらに、複合型を <xref:System.Runtime.Serialization.DataContractAttribute> 属性でマークすると、シリアル化されたデータを公開することもできます。 これにより、クライアント内でデータ バインディングが可能になります。

インターフェイスとそのメソッドを定義すると、それらは、インターフェイスを実装するクラスにカプセル化されます。 単一の WCF サービス クラスで複数のサービス コントラクトを実装できます。

WCF サービスは、"*エンドポイント*" と呼ばれるものを介して使用するために公開されます。 エンドポイントは、このサービスと通信できる唯一の方法です。他のクラスの場合のように、直接参照を介してサービスにアクセスすることはできません。

エンドポイントは、アドレス、バインド、コントラクトで構成されます。 アドレスでは、サービスが配置されている場所を定義します。これは、URL、FTP アドレス、ネットワークまたはローカル パスを指定できます。 バインドは、サービスとの通信方法を定義します。 WCF バインドでは、プロトコル (HTTP、FTP など)、のセキュリティ メカニズム (Windows 認証、ユーザー名とパスワードなど) などを指定するための汎用性のあるモデルを提供します。 コントラクトには、WCF サービス クラスによって公開される操作が含まれます。

単一の WCF サービスについて複数のエンドポイントを公開できます。 これにより、さまざまなクライアントが、異なる方法で同じサービスと通信できるようになります。 たとえば、バンキング サービスでは、あるエンドポイントを従業員に、別のエンドポイントを外部の顧客に提供し、それぞれが異なるアドレス、バインド、またはコントラクトを使用するようにすることができます。

### <a name="wcf-client"></a>WCF クライアント

WCF クライアントは、アプリケーションが WCF サービスと通信できるようにする "*プロキシ*" と、サービスに対して定義されたエンドポイントと一致するエンドポイントで構成されます。 プロキシは、クライアント側の *app.config* ファイルで生成され、サービスによって公開される型とメソッドに関する情報が含まれます。 複数のエンドポイントを公開するサービスの場合、クライアントでは、ニーズ (たとえば、HTTP 経由で通信し、Windows 認証を使用するなど) に最も適したエンドポイントが選択されます。

WCF クライアントを作成した後、他のオブジェクトと同様に、コード内でサービスを参照します。 たとえば、前に示した `GetData` メソッドを呼び出すには、次のようなコードを記述します。

[!code-csharp[WCFWalkthrough#3](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_3.cs)]
[!code-vb[WCFWalkthrough#3](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_3.vb)]

## <a name="wcf-tools-in-visual-studio"></a>Visual Studio の WCF ツール

Visual Studio では、WCF サービスと WCF クライアントの両方を作成するのに役立つツールを提供します。 ツールに関するチュートリアルについては、「[チュートリアル: Windows フォームで簡単な WCF サービスを作成する](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md)」を参照してください。

### <a name="create-and-test-wcf-services"></a>WCF サービスを作成してテストする

独自のサービスをすばやく作成するためのひな型として、WCF Visual Studio テンプレートを使用することができます。 その後、WCF サービスの自動ホストと WCF テスト クライアントを使用して、サービスのデバッグとテストを行うことができます。 これらのツールを組み合わせることで、高速で便利なデバッグおよびテスト サイクルが実現され、早い段階でホスティング モデルにコミットする必要がなくなります。

#### <a name="wcf-templates"></a>WCF テンプレート

WCF Visual Studio テンプレートによって、サービス開発のための基本的なクラス構造が提供されます。 一部の WCF テンプレートは、 **[新しいプロジェクトの追加]** ダイアログ ボックスで使用できます。 これらには、WCF サービス Library プロジェクト、WCF サービス Web サイト、WCF サービス項目テンプレートが含まれます。

テンプレートを選択すると、サービス コントラクト、サービス実装、サービス構成用のファイルが追加されます。 必要なすべての属性が既に追加され、単純な "Hello World" 型のサービスが作成されているため、コードを記述する必要はありません。 もちろん、実際のサービスの関数とメソッドを提供するコードを追加する必要はありますが、テンプレートによって基本的なひな型が提供されます。

WCF テンプレートの詳細については、「[WCF Visual Studio テンプレート](/dotnet/framework/wcf/wcf-vs-templates)」を参照してください。

#### <a name="wcf-service-host"></a>WCF サービス ホスト

WCF サービス プロジェクトの Visual Studio デバッガーを起動すると (**F5** キーを押す)、WCF サービス ホスト ツールが自動的に起動し、サービスをローカルでホストします。 WCF サービス ホストでは、サービス プロジェクト内のサービスを列挙し、プロジェクトの構成を読み込んで、検出した各サービスのためのホストをインスタンス化します。

WCF サービス ホストを使用すると、追加のコードを記述したり、開発時に特定のホストにコミットしたりすることなく、WCF サービスをテストできます。

WCF サービス ホストの詳細については、「[WCF サービス ホスト (WcfSvcHost.exe)](/dotnet/framework/wcf/wcf-service-host-wcfsvchost-exe)」を参照してください。

#### <a name="wcf-test-client"></a>WCF テスト クライアント

WCF テスト クライアント ツールを使用すると、テスト パラメーターを入力し、その入力を WCF サービスに送信し、サービスから返される応答を表示できます。 これを WCF サービス ホストと組み合わせると、便利なサービス テスト エクスペリエンスが提供されます。 ツールは、 *%ProgramFiles(x86)%\Microsoft Visual Studio\2017\Enterprise\Common7\IDE* フォルダー内にあります。

**F5** キーを押して WCF サービス プロジェクトをデバッグすると、WCF テスト クライアントが開いて、構成ファイルで定義されているサービス エンドポイントの一覧が表示されます。 ユーザーは、パラメーターをテストしてサービスを起動することができ、このプロセスを繰り返して、サービスのテストおよび検証を継続的に行うことができます。

WCF テスト クライアントの詳細については、「[WCF のテスト用クライアント (WcfTestClient.exe)](/dotnet/framework/wcf/wcf-test-client-wcftestclient-exe)」を参照してください。

### <a name="accessing-wcf-services-in-visual-studio"></a>Visual Studio での WCF サービスへのアクセス

Visual Studio では、WCF クライアントを作成するタスクが簡素化され、 **[サービス参照の追加]** ダイアログ ボックスを使用して追加するサービスのプロキシとエンドポイントが自動的に生成されます。 必要なすべての構成情報が *app.config* ファイルに追加されます。 ほとんどの場合、サービスを使用するには、それをインスタンス化するだけで済みます。

**[サービス参照の追加]** ダイアログ ボックスを使用すると、サービスのアドレスを入力したり、ソリューションで定義されたサービスを検索したりすることができます。 このダイアログ ボックスでは、サービスの一覧と、それらのサービスによって提供される操作が返されます。 また、これを使用すると、コードでサービスを参照する名前空間を定義することもできます。

**[サービス参照の構成]** ダイアログ ボックスでは、サービスの構成をカスタマイズできます。 サービスのアドレスの変更、アクセス レベル、非同期動作、およびメッセージ コントラクト型の指定、型の再利用の構成を行うことができます。

## <a name="how-to-select-a-service-endpoint"></a>方法: サービス エンドポイントを選択する

一部の Windows Communication Foundation (WCF) サービスでは、クライアントでサービスとの通信に使用される複数のエンドポイントを公開します。 たとえば、あるサービスでは、HTTP バインドとユーザー名およびパスワードのセキュリティを使用するエンドポイントと、FTP と Windows 認証を使用する 2 番目のエンドポイントを公開するとしましょう。 最初のエンドポイントは、ファイアウォールの外部からサービスにアクセスするアプリケーションによって使用され、2 番目は、イントラネット上で使用されます。

このような場合、サービス参照のコンストラクターのパラメーターとして、`endpointConfigurationName` を指定できます。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-select-a-service-endpoint"></a>サービス エンドポイントを選択する

1. **ソリューション エクスプローラー** でプロジェクト ノードを右クリックし、 **[サービス参照の追加]** を選択して、WCF サービスへの参照を追加します。

2. コード エディターで、サービス参照のコンストラクターを追加します。

    ```vb
    Dim proxy As New ServiceReference.Service1Client(
    ```

    ```csharp
    ServiceReference.Service1Client proxy = new ServiceReference.Service1Client(
    ```

    > [!NOTE]
    > *ServiceReference* をサービス参照の名前空間に置き換え、*Service1Client* をサービスの名前に置き換えます。

3. IntelliSense の一覧には、コンストラクターのオーバーロードが含まれます。 `endpointConfigurationName As String` オーバーロードを選択します。

4. オーバーロードの後に、「`=` *ConfigurationName*」と入力します。ここで、*ConfigurationName* は、使用するエンドポイントの名前です。

    > [!NOTE]
    > 使用可能なエンドポイントの名前がわからない場合は、*app.config* ファイルで見つけることができます。

### <a name="to-find-the-available-endpoints-for-a-wcf-service"></a>WCF サービスに使用できるエンドポイントを見つける

1. **ソリューション エクスプローラー**で、サービス参照を含むプロジェクトの **app.config** ファイルを右クリックし、 **[開く]** をクリックします。 コード エディターにファイルが表示されます。

2. ファイル内で `<Client>` タグを検索します。

3. `<Client>` タグの下で、`<Endpoint>` から始まるタグを検索します。

     サービス参照で複数のエンドポイントが提供される場合、2 つ以上の `<Endpoint` タグがあります。

4. `<EndPoint>` タグ内で、`name="`*SomeService*`"` パラメーター (ここで、*SomeService* はエンドポイント名を表します) を探します。 これは、サービス参照のコンストラクターの `endpointConfigurationName As String` オーバーロードに渡すことができるエンドポイントの名前です。

## <a name="how-to-call-a-service-method-asynchronously"></a>方法: サービス メソッドを非同期に呼び出す

Windows Communication Foundation (WCF) サービスのほとんどのメソッドは、同期または非同期のいずれかで呼び出すことができます。 メソッドを非同期に呼び出すことにより、アプリケーションは、低速接続で動作している場合、メソッドを呼び出している間も動作を継続することができます。

既定では、サービス参照がプロジェクトに追加されたときに、メソッドを同期的に呼び出すように構成されます。 メソッドを非同期に呼び出すように動作を変更するには、 **[サービス参照の構成]** ダイアログ ボックスで設定を変更します。

> [!NOTE]
> このオプションは、サービスごとに設定します。 サービスの 1 つのメソッドが非同期に呼び出される場合、すべてのメソッドを非同期に呼び出す必要があります。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-call-a-service-method-asynchronously"></a>サービス メソッドを非同期に呼び出す

1. **ソリューション エクスプローラー**で、サービス参照を選択します。

2. **[プロジェクト]** メニューで、 **[サービス参照の構成]** をクリックします。

3. **[サービス参照の構成]** ダイアログ ボックスで、 **[非同期操作の生成]** チェック ボックスをオンにします。

## <a name="how-to-bind-data-returned-by-a-service"></a>方法: サービスから返されたデータをバインドする

他のデータソースをコントロールにバインドする場合と同様に、Windows Communication Foundation (WCF) サービスから返されたデータをコントロールにバインドすることができます。 WCF サービスへの参照を追加すると、データを返す複合型がサービスに含まれている場合、それらは自動的に **[データ ソース]** ウィンドウに追加されます。

### <a name="to-bind-a-control-to-single-data-field-returned-by-a-wcf-service"></a>WCF サービスから返された単一のデータ フィールドにコントロールをバインドする

1. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

   **[データ ソース]** ウィンドウが表示されます。

2. **[データ ソース]** ウィンドウで、サービス参照のノードを展開します。 サービスから返された複合型が表示されます。

3. 型のノードを展開します。 その型のデータ フィールドが表示されます。

4. フィールドを選択し、ドロップダウン矢印をクリックして、そのデータ型に使用できるコントロールの一覧を表示します。

5. バインド先のコントロールの型をクリックします。

6. フィールドをフォームにドラッグします。 コントロールが、<xref:System.Windows.Forms.BindingSource> コンポーネントおよび <xref:System.Windows.Forms.BindingNavigator> コンポーネントと共にフォームに追加されます。

7. バインドする他のフィールドについて、手順 4 から 6 を繰り返します。

### <a name="to-bind-a-control-to-composite-type-returned-by-a-wcf-service"></a>WCF サービスから返される複合型にコントロールをバインドする

1. **[データ]** メニューで、 **[データ ソースの表示]** を選択します。 **[データ ソース]** ウィンドウが表示されます。

2. **[データ ソース]** ウィンドウで、サービス参照のノードを展開します。 サービスから返された複合型が表示されます。

3. 型のノードを選択し、ドロップダウン矢印をクリックして、使用可能なオプションの一覧を表示します。

4. **[DataGridView]** をクリックしてグリッドにデータを表示するか、 **[詳細]** をクリックして、個々のコントロールにデータを表示します。

5. ノードをフォームにドラッグします。 コントロールが、<xref:System.Windows.Forms.BindingSource> コンポーネントおよび <xref:System.Windows.Forms.BindingNavigator> コンポーネントと共にフォームに追加されます。

## <a name="how-to-configure-a-service-to-reuse-existing-types"></a>方法: 既存の型を再利用するようにサービスを構成する

サービス参照をプロジェクトに追加すると、サービスで定義されている型がローカル プロジェクトに生成されます。 多くの場合、これにより、サービスが共通の .NET 型を使用する場合、または型が共有ライブラリで定義されている場合は、重複する型が作成されます。

この問題を回避するには、既定により、参照されたアセンブリ内の型を共有します。 1 つ以上のアセンブリに対して型の共有を無効にする必要がある場合は、 **[サービス参照の構成]** ダイアログ ボックスで無効にすることができます。

### <a name="to-disable-type-sharing-in-a-single-assembly"></a>単一のアセンブリで型の共有を無効にする

1. **ソリューション エクスプローラー**で、サービス参照を選択します。

2. **[プロジェクト]** メニューで、 **[サービス参照の構成]** をクリックします。

3. **[サービス参照の構成]** ダイアログ ボックスで、 **[参照されたアセンブリを指定して型を再利用]** を選択します。

4. 型の共有を有効にする各アセンブリのチェック ボックスをオンにします。 アセンブリに対して型の共有を無効にするには、チェック ボックスをオフのままにします。

### <a name="to-disable-type-sharing-in-all-assemblies"></a>すべてのアセンブリで型の共有を無効にする

1. **ソリューション エクスプローラー**で、サービス参照を選択します。

2. **[プロジェクト]** メニューで、 **[サービス参照の構成]** をクリックします。

3. **[サービス参照の構成]** ダイアログ ボックスで、 **[参照されたアセンブリで型を再利用]** チェック ボックスをオフにします。

## <a name="related-topics"></a>関連トピック

| Title | [説明] |
| - | - |
| [チュートリアル : Windows フォームでの簡単な WCF サービスの作成](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md) | Visual Studio で WCF サービスを作成して使用する例をステップバイステップで説明します。 |
| [チュートリアル: WPF と Entity Framework を使用した WCF データ サービスの作成](../data-tools/walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework.md) | Visual Studio で WCF Data Services を作成して使用する方法をステップバイステップで説明します。 |
| [WCF 開発ツールの使用](/dotnet/framework/wcf/using-the-wcf-development-tools) | Visual Studio で WCF サービスを作成してテストする方法を説明します。 |
| | [方法: WCF データ サービス参照を追加、更新、または削除する](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md) |
| [サービス参照のトラブルシューティング](../data-tools/troubleshooting-service-references.md) | サービス参照で発生する化膿性のある一般的なエラーとそれを防ぐ方法について説明します。 |
| [WCF サービスのデバッグ](../debugger/debugging-wcf-services.md) | WCF サービスのデバッグ時に発生する可能性のある一般的なデバッグ問題と手法について説明します。 |
| [チュートリアル: n 層データ アプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md) | 型指定されたデータセットを作成し、TableAdapter とデータセット コードを複数のプロジェクトに分離する手順について説明します。 |
| [[サービス参照の構成] ダイアログ ボックス](../data-tools/configure-service-reference-dialog-box.md) | **[サービス参照の構成]** のユーザー インターフェイス要素について説明します。 |

## <a name="reference"></a>関連項目

- <xref:System.ServiceModel>
- <xref:System.Data.Services>

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
