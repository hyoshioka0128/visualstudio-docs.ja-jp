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
ms.sourcegitcommit: 1d4f6cc80ea343a667d16beec03220cfe1f43b8e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85281046"
---
# <a name="windows-communication-foundation-services-and-wcf-data-services-in-visual-studio"></a>Visual Studio での Windows Communication Foundation サービスと WCF データ サービス

Visual Studio には、分散アプリケーションを作成するための Microsoft テクノロジで Windows Communication Foundation (WCF) および WCF Data Services を操作するためのツールが用意されています。 このトピックでは、Visual Studio の観点から見たサービスの概要について説明します。 完全なドキュメントについては、「 [WCF Data Services 4.5](/dotnet/framework/data/wcf/index)」を参照してください。

## <a name="what-is-wcf"></a>WCF とは

Windows Communication Foundation (WCF) は、セキュリティで保護され、信頼性が高く、トランザクションに対応し、相互運用可能な分散アプリケーションを作成するための統合フレームワークです。 これにより、ASMX web サービス、.NET リモート処理、エンタープライズサービス (DCOM)、MSMQ などの古いプロセス間通信テクノロジが置き換えられます。 WCF は、これらのすべてのテクノロジの機能を統一されたプログラミングモデルで統合します。 これにより、分散アプリケーションの開発経験が簡単になります。

### <a name="what-are-wcf-data-services"></a>WCF Data Services とは

WCF Data Services は、Open Data (OData) プロトコル標準の実装です。  WCF Data Services を使用すると、表形式のデータを一連の REST Api として公開できるため、GET、POST、PUT、DELETE などの標準的な HTTP 動詞を使用してデータを返すことができます。 サーバー側では、新しい OData サービスを作成するために[ASP.NET Web API](https://dotnet.microsoft.com/apps/aspnet/apis)によって WCF Data Services が置き換えられます。 WCF Data Services クライアントライブラリは、Visual Studio (**Project**サービス参照の追加) から .net アプリケーションで OData サービスを使用する場合にも引き続き適して  >  **Add Service Reference**います。 詳細については、「[WCF Data Services 4.5](/dotnet/framework/data/wcf)」を参照してください。

### <a name="wcf-programming-model"></a>WCF プログラミングモデル

Wcf プログラミングモデルは、WCF サービスと WCF クライアントの2つのエンティティ間の通信に基づいています。 プログラミングモデルは、.NET の名前空間にカプセル化されてい <xref:System.ServiceModel> ます。

### <a name="wcf-service"></a>WCF サービス

WCF サービスは、サービスとクライアントの間のコントラクトを定義するインターフェイスに基づいています。 <xref:System.ServiceModel.ServiceContractAttribute>次のコードに示すように、属性でマークされています。

[!code-csharp[WCFWalkthrough#6](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_1.cs)]
[!code-vb[WCFWalkthrough#6](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_1.vb)]

WCF サービスによって公開される関数またはメソッドは、属性でマークすることによって定義し <xref:System.ServiceModel.OperationContractAttribute> ます。

[!code-csharp[WCFWalkthrough#1](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_2.cs)]
[!code-vb[WCFWalkthrough#1](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_2.vb)]

さらに、複合型を属性でマークすることによって、シリアル化されたデータを公開でき <xref:System.Runtime.Serialization.DataContractAttribute> ます。 これにより、クライアントでのデータバインディングが有効になります。

インターフェイスとそのメソッドを定義すると、インターフェイスを実装するクラスにカプセル化されます。 1つの WCF サービスクラスは、複数のサービスコントラクトを実装できます。

WCF サービスは、*エンドポイント*と呼ばれるものを通じて使用するために公開されます。 エンドポイントは、サービスと通信する唯一の方法を提供します。他のクラスの場合と同じように、直接参照を使用してサービスにアクセスすることはできません。

エンドポイントは、アドレス、バインディング、およびコントラクトで構成されます。 アドレスは、サービスが存在する場所を定義します。URL、FTP アドレス、またはネットワークまたはローカルパスを指定できます。 バインディングは、サービスとの通信方法を定義します。 WCF バインドは、HTTP や FTP などのプロトコル、Windows 認証やユーザー名やパスワードなどのセキュリティメカニズムなどを指定するための、汎用性のあるモデルを提供します。 コントラクトには、WCF サービスクラスによって公開される操作が含まれます。

1つの WCF サービスに対して複数のエンドポイントを公開できます。 これにより、さまざまなクライアントが異なる方法で同じサービスと通信できるようになります。 たとえば、銀行のサービスでは、従業員に対して1つのエンドポイントを提供し、外部の顧客に対してそれぞれ異なる住所、バインド、または契約を使用することができます。

### <a name="wcf-client"></a>WCF クライアント

WCF クライアントは、アプリケーションが WCF サービスと通信できるようにする*プロキシ*と、サービスに対して定義されているエンドポイントと一致するエンドポイントで構成されます。 プロキシは、 *app.config*ファイルのクライアント側で生成され、サービスによって公開される型とメソッドに関する情報が含まれます。 複数のエンドポイントを公開するサービスでは、クライアントは、HTTP を介して通信し、Windows 認証を使用するなど、ニーズに最適なエンドポイントを選択できます。

WCF クライアントを作成した後は、他のオブジェクトの場合と同様に、コード内でサービスを参照します。 たとえば、前に示したメソッドを呼び出すに `GetData` は、次のようなコードを記述します。

[!code-csharp[WCFWalkthrough#3](../data-tools/codesnippet/CSharp/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_3.cs)]
[!code-vb[WCFWalkthrough#3](../data-tools/codesnippet/VisualBasic/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio_3.vb)]

## <a name="wcf-tools-in-visual-studio"></a>Visual Studio の WCF ツール

Visual Studio には、WCF サービスと WCF クライアントの両方を作成するのに役立つツールが用意されています。 ツールを示すチュートリアルについては、「[チュートリアル: Windows フォームでの単純な WCF サービスの作成](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md)」を参照してください。

### <a name="create-and-test-wcf-services"></a>WCF サービスの作成とテスト

WCF Visual Studio テンプレートを基礎として使用して、独自のサービスをすばやく作成することができます。 その後、WCF サービスの自動ホストと WCF テストクライアントを使用して、サービスのデバッグとテストを行うことができます。 これらのツールを一緒に使用すると、高速で便利なデバッグとテストのサイクルが実現し、初期段階でホスティングモデルにコミットする必要がなくなります。

#### <a name="wcf-templates"></a>WCF テンプレート

WCF Visual Studio テンプレートは、サービス開発のための基本クラス構造を提供します。 [**新しいプロジェクトの追加**] ダイアログボックスでは、いくつかの WCF テンプレートを使用できます。 これには、WCF サービス lLibrary プロジェクト、WCF サービス web サイト、および WCF サービス項目テンプレートが含まれます。

テンプレートを選択すると、サービスコントラクト、サービス実装、およびサービス構成のファイルが追加されます。 必要なすべての属性が既に追加されており、単純な "Hello World" 型のサービスが作成されており、コードを記述する必要はありませんでした。 もちろん、実際のサービスの関数とメソッドを提供するコードを追加する必要がありますが、テンプレートには基本的な基盤が用意されています。

WCF テンプレートの詳細については、「 [Wcf Visual Studio テンプレート](/dotnet/framework/wcf/wcf-vs-templates)」を参照してください。

#### <a name="wcf-service-host"></a>WCF サービス ホスト

WCF サービスプロジェクトに対して**F5**キーを押して Visual Studio デバッガーを起動すると、サービスをローカルでホストするために Wcf サービスホストツールが自動的に開始されます。 Wcf サービスホストは、WCF サービスプロジェクト内のサービスを列挙し、プロジェクトの構成を読み込み、検出された各サービスのホストをインスタンス化します。

WCF サービスホストを使用すると、追加のコードを記述したり、開発中に特定のホストにコミットしたりせずに、WCF サービスをテストできます。

WCF サービスホストの詳細については、「 [wcf サービスホスト」 (WcfSvcHost.exe)](/dotnet/framework/wcf/wcf-service-host-wcfsvchost-exe)を参照してください。

#### <a name="wcf-test-client"></a>WCF テスト クライアント

WCF テストクライアントツールを使用すると、テストパラメーターを入力し、その入力を WCF サービスに送信し、サービスから返される応答を表示できます。 WCF サービスホストと組み合わせて使用すると、便利なサービステストエクスペリエンスが提供されます。 *% ProgramFiles (x86)% \ Microsoft Visual Studio\2017\Enterprise\Common7\IDE*フォルダーでツールを見つけます。

**F5**キーを押して wcf サービスプロジェクトをデバッグすると、Wcf テストクライアントが開き、構成ファイルで定義されているサービスエンドポイントの一覧が表示されます。 パラメーターをテストしてサービスを開始し、このプロセスを繰り返してサービスを継続的にテストして検証することができます。

WCF テストクライアントの詳細については、「 [wcf テストクライアント (WcfTestClient.exe)](/dotnet/framework/wcf/wcf-test-client-wcftestclient-exe)」を参照してください。

### <a name="accessing-wcf-services-in-visual-studio"></a>Visual Studio での WCF サービスへのアクセス

Visual Studio を使用すると、WCF クライアントを作成するタスクが簡単になります。また、[**サービス参照の追加**] ダイアログボックスを使用して追加するサービスのプロキシとエンドポイントも自動的に生成されます。 必要な構成情報がすべて*app.config*ファイルに追加されます。 ほとんどの場合、使用するためにサービスをインスタンス化するだけで済みます。

[**サービス参照の追加**] ダイアログボックスでは、サービスのアドレスを入力したり、ソリューションで定義されているサービスを検索したりできます。 このダイアログボックスでは、サービスの一覧と、それらのサービスによって提供される操作が返されます。 また、コード内でサービスを参照するときに使用する名前空間を定義することもできます。

[**サービス参照の構成**] ダイアログボックスを使用して、サービスの構成をカスタマイズできます。 サービスのアドレスの変更、アクセスレベル、非同期動作、およびメッセージコントラクト型の指定、および型の再利用の構成を行うことができます。

## <a name="how-to-select-a-service-endpoint"></a>方法: サービスエンドポイントを選択する

一部の Windows Communication Foundation (WCF) サービスは、クライアントがサービスと通信するために使用される複数のエンドポイントを公開します。 たとえば、サービスは、HTTP バインド、ユーザー名とパスワードのセキュリティ、および FTP と Windows 認証を使用する2番目のエンドポイントを使用する1つのエンドポイントを公開する場合があります。 最初のエンドポイントは、ファイアウォールの外部からサービスにアクセスするアプリケーションによって使用される場合があります。一方、2番目のエンドポイントは、イントラネットで使用される可能性があります。

このような場合は、 `endpointConfigurationName` サービス参照のコンストラクターのパラメーターとしてを指定できます。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-select-a-service-endpoint"></a>サービスエンドポイントを選択するには

1. **ソリューションエクスプローラー**でプロジェクトノードを右クリックし、[**サービス参照の追加**] を選択して、WCF サービスへの参照を追加します。

2. コードエディターで、サービス参照のコンストラクターを追加します。

    ```vb
    Dim proxy As New ServiceReference.Service1Client(
    ```

    ```csharp
    ServiceReference.Service1Client proxy = new ServiceReference.Service1Client(
    ```

    > [!NOTE]
    > *ServiceReference*をサービス参照の名前空間に置き換え、 *Service1Client*をサービスの名前に置き換えます。

3. IntelliSense の一覧には、コンストラクターのオーバーロードが含まれています。 オーバーロードを選択し `endpointConfigurationName As String` ます。

4. オーバーロードの後に「 `=` *configurationname*」と入力します。 *configurationname*は、使用するエンドポイントの名前です。

    > [!NOTE]
    > 使用可能なエンドポイントの名前がわからない場合は、 *app.config*ファイルで見つけることができます。

### <a name="to-find-the-available-endpoints-for-a-wcf-service"></a>WCF サービスで使用可能なエンドポイントを検索するには

1. **ソリューションエクスプローラー**で、サービス参照を含むプロジェクトの**app.config**ファイルを右クリックし、[**開く**] をクリックします。 ファイルがコードエディターに表示されます。

2. `<Client>`ファイル内のタグを検索します。

3. タグの下 `<Client>` で、で始まるタグを検索 `<Endpoint>` します。

     サービス参照に複数のエンドポイントが指定されている場合は、2つ以上のタグがあり `<Endpoint` ます。

4. タグ内 `<EndPoint>` には、(この場合は `name="` *SomeService* `"` エンドポイント名を表す) *SomeService*パラメーターがあります。 これは、 `endpointConfigurationName As String` サービス参照のコンストラクターのオーバーロードに渡すことができるエンドポイントの名前です。

## <a name="how-to-call-a-service-method-asynchronously"></a>方法: サービスメソッドを非同期に呼び出す

Windows Communication Foundation (WCF) サービスのほとんどのメソッドは、同期的または非同期的に呼び出すことができます。 メソッドを非同期的に呼び出すことで、低速接続で動作しているときにメソッドが呼び出されている間も、アプリケーションを引き続き動作させることができます。

既定では、サービス参照がプロジェクトに追加されると、メソッドを同期的に呼び出すように構成されます。 [**サービス参照の構成**] ダイアログボックスの設定を変更することで、メソッドを非同期に呼び出す動作を変更できます。

> [!NOTE]
> このオプションはサービスごとに設定します。 サービスの1つのメソッドを非同期に呼び出す場合は、すべてのメソッドを非同期に呼び出す必要があります。

[!INCLUDE[note_settings_general](../data-tools/includes/note_settings_general_md.md)]

### <a name="to-call-a-service-method-asynchronously"></a>サービスメソッドを非同期的に呼び出すには

1. **ソリューションエクスプローラー**で、サービス参照を選択します。

2. [**プロジェクト**] メニューの [**サービス参照の構成**] をクリックします。

3. [**サービス参照の構成**] ダイアログボックスで、[**非同期操作を生成**する] チェックボックスをオンにします。

## <a name="how-to-bind-data-returned-by-a-service"></a>方法: サービスによって返されるデータをバインドする

他のデータソースをコントロールにバインドするのと同じように、Windows Communication Foundation (WCF) サービスから返されたデータをコントロールにバインドすることができます。 WCF サービスへの参照を追加すると、データを返す複合型がサービスに含まれている場合は、自動的に [**データソース**] ウィンドウに追加されます。

### <a name="to-bind-a-control-to-single-data-field-returned-by-a-wcf-service"></a>WCF サービスによって返される単一のデータフィールドにコントロールをバインドするには

1. **[データ]** メニューの **[データ ソースの表示]** をクリックします。

   [**データソース**] ウィンドウが表示されます。

2. [**データソース**] ウィンドウで、サービス参照のノードを展開します。 サービスによって返される複合型。

3. 型のノードを展開します。 その型のデータフィールドが表示されます。

4. フィールドを選択し、ドロップダウン矢印をクリックすると、そのデータ型で使用できるコントロールの一覧が表示されます。

5. バインド先のコントロールの種類をクリックします。

6. フィールドをフォームにドラッグします。 コントロールは、コンポーネントおよびコンポーネントと共にフォームに追加され <xref:System.Windows.Forms.BindingSource> <xref:System.Windows.Forms.BindingNavigator> ます。

7. バインドするその他のフィールドに対して、手順 4. ~ 6. を繰り返します。

### <a name="to-bind-a-control-to-composite-type-returned-by-a-wcf-service"></a>WCF サービスによって返される複合型にコントロールをバインドするには

1. [**データ**] メニューの [**データソースの表示**] をクリックします。 [**データソース**] ウィンドウが表示されます。

2. [**データソース**] ウィンドウで、サービス参照のノードを展開します。 サービスによって返される複合型。

3. 種類のノードを選択し、ドロップダウン矢印をクリックすると、使用可能なオプションの一覧が表示されます。

4. [ **DataGridView** ] をクリックすると、グリッドまたは**詳細**にデータが表示され、個々のコントロールにデータが表示されます。

5. ノードをフォームにドラッグします。 コントロールは、コンポーネントおよびコンポーネントと共にフォームに追加され <xref:System.Windows.Forms.BindingSource> <xref:System.Windows.Forms.BindingNavigator> ます。

## <a name="how-to-configure-a-service-to-reuse-existing-types"></a>方法: 既存の型を再利用するようにサービスを構成する

サービス参照がプロジェクトに追加されると、サービスで定義されているすべての型がローカルプロジェクトに生成されます。 多くの場合、サービスが共通の .NET 型を使用している場合や、共有ライブラリで型が定義されている場合は、重複する型が作成されます。

この問題を回避するために、参照されたアセンブリ内の型は既定で共有されます。 1つ以上のアセンブリの型の共有を無効にする場合は、[**サービス参照の構成**] ダイアログボックスで行うことができます。

### <a name="to-disable-type-sharing-in-a-single-assembly"></a>1つのアセンブリで型の共有を無効にするには

1. **ソリューションエクスプローラー**で、サービス参照を選択します。

2. [**プロジェクト**] メニューの [**サービス参照の構成**] をクリックします。

3. [**サービス参照の構成**] ダイアログボックスで、[**指定した参照アセンブリの型を再利用**する] を選択します。

4. 型の共有を有効にする各アセンブリのチェックボックスをオンにします。 アセンブリの型の共有を無効にするには、チェックボックスをオフのままにします。

### <a name="to-disable-type-sharing-in-all-assemblies"></a>すべてのアセンブリで型の共有を無効にするには

1. **ソリューションエクスプローラー**で、サービス参照を選択します。

2. [**プロジェクト**] メニューの [**サービス参照の構成**] をクリックします。

3. [**サービス参照の構成**] ダイアログボックスで、[参照された**アセンブリの型を再利用**する] チェックボックスをオフにします。

## <a name="related-topics"></a>関連トピック

| Title | 説明 |
| - | - |
| [チュートリアル : Windows フォームでの簡単な WCF サービスの作成](../data-tools/walkthrough-creating-a-simple-wcf-service-in-windows-forms.md) | Visual Studio で WCF サービスを作成および使用する方法を順を追って説明します。 |
| [チュートリアル: WPF と Entity Framework を使用した WCF データサービスの作成](../data-tools/walkthrough-creating-a-wcf-data-service-with-wpf-and-entity-framework.md) | Visual Studio で WCF Data Services を作成して使用する方法をステップバイステップで説明します。 |
| [WCF 開発ツールの使用](/dotnet/framework/wcf/using-the-wcf-development-tools) | Visual Studio で WCF サービスを作成およびテストする方法について説明します。 |
| | [方法: WCF データサービス参照を追加、更新、または削除する](../data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference.md) |
| [サービス参照のトラブルシューティング](../data-tools/troubleshooting-service-references.md) | サービス参照で発生する可能性のある一般的なエラーと、それらを回避する方法について説明します。 |
| [WCF サービスのデバッグ](../debugger/debugging-wcf-services.md) | WCF サービスのデバッグ時に発生する可能性のある一般的なデバッグの問題と手法について説明します。 |
| [チュートリアル: n 層データアプリケーションの作成](../data-tools/walkthrough-creating-an-n-tier-data-application.md) | 型指定されたデータセットを作成し、TableAdapter とデータセット コードを複数のプロジェクトに分離する手順について説明します。 |
| [[サービス参照の構成] ダイアログ ボックス](../data-tools/configure-service-reference-dialog-box.md) | [**サービス参照の構成**] ダイアログボックスのユーザーインターフェイス要素について説明します。 |

## <a name="reference"></a>関連項目

- <xref:System.ServiceModel>
- <xref:System.Data.Services>

## <a name="see-also"></a>関連項目

- [.NET 用の Visual Studio データ ツール](../data-tools/visual-studio-data-tools-for-dotnet.md)
