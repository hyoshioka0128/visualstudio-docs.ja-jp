---
title: ビジネスデータ接続モデルを設計する |Microsoft Docs
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- BDC [SharePoint development in Visual Studio], designing a model
- Business Data Connectivity service [SharePoint development in Visual Studio], designing a model
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 16a410b59cef6f282d2d27ad90a90013636d6489
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72984467"
---
# <a name="design-a-business-data-connectivity-model"></a>ビジネスデータ接続モデルを設計する
  エンティティとメソッドをモデルファイルに追加することによって、Business Data Connectivity (BDC) サービスのモデルを開発できます。 エンティティは、データフィールドのコレクションを記述します。 たとえば、エンティティはデータベース内のテーブルを表すことができます。 メソッドは、エンティティによって表されるデータの追加、削除、更新などのタスクを実行します。 詳細については、「 [SharePoint へのビジネスデータの統合](../sharepoint/integrating-business-data-into-sharepoint.md)」を参照してください。

## <a name="add-entities"></a>複数エンティティの追加
 エンティティを追加するには、Visual Studio の**ツールボックス**から BDC デザイナーに**エンティティ**をドラッグまたはコピーします。 詳細については、「 [方法: モデルにエンティティを追加](../sharepoint/how-to-add-an-entity-to-a-model.md)する」を参照してください。

 クラスのエンティティのフィールドを定義します。 たとえば、という名前のフィールドをクラスに追加することができ `Address` `Customer` ます。 新しいクラスをプロジェクトに追加するか、またはオブジェクトリレーショナルデザイナー (O/R デザイナー) などの他のツールを使用して作成された既存のクラスを使用することができます。 エンティティの名前と、エンティティを表すクラスの名前が一致している必要はありません。 モデルでメソッドを定義するときに、クラスをエンティティに関連付けます。

## <a name="add-methods"></a>メソッドの追加
 ユーザーがモデルに基づくリストまたは Web パーツの情報を表示、追加、更新、または削除すると、BDC サービスはモデル内のメソッドを呼び出します。 ユーザーが実行できるタスクごとに、モデルにメソッドを追加する必要があります。 [ **BDC メソッドの詳細** ] ウィンドウで、5つの基本メソッドの種類のいずれかを選択して、メソッドを作成します。 次の表では、BDC モデルの5つの基本的な方法について説明します。

|メソッド|説明|
|------------|-----------------|
|周り|エンティティインスタンスのコレクションを返します。 ユーザーがリストまたは Web パーツを開いたときに呼び出されます。 詳細については、「 [方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)」を参照してください。|
|SpecificFinder|特定のエンティティインスタンスを返します。 ユーザーがリスト内の特定の項目の詳細を表示するときに呼び出されます。 詳細については、「 [方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)」を参照してください。|
|Creator|エンティティのデータソースに新しいデータを追加します。 モデルに基づくリストのリボンの [ **新しい項目** ] ボタンをユーザーが選択すると呼び出されます。 詳細については、「 [方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)」を参照してください。|
|Updater|リスト内のデータを変更します。 ユーザーがリスト内の情報を更新するときに呼び出されます。 詳細については、「 [方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)」を参照してください。|
|Deleter|データを削除します。 ユーザーがリストから項目を削除したときに呼び出されます。 詳細については、「 [方法: 削除子メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)」を参照してください。|

## <a name="define-method-parameters"></a>メソッドパラメーターの定義
 メソッドを作成すると、Visual Studio によって、メソッドの型に適した入力パラメーターと出力パラメーターが追加されます。 これらのパラメーターは単なるプレースホルダーです。 ほとんどの場合、パラメーターを変更して渡すか、正しい型のデータを返すようにする必要があります。 たとえば、既定では、Finder メソッドは文字列を返します。 ほとんどの場合、エンティティのコレクションを返すように Finder メソッドの戻りパラメーターを変更します。 これを行うには、パラメーターの型記述子を変更します。 型記述子は、パラメーターのデータ型を記述する属性のコレクションです。 詳細については、「 [方法: パラメーターの型記述子を定義](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)する」を参照してください。

 Visual Studio では、モデル内のパラメーター間で型記述子をコピーできます。 たとえば、メソッドの戻りパラメーターとして、という名前の型記述子を定義でき `CustomerTD` `GetCustomer` ます。 `CustomerTD` **BDC エクスプローラー**で型記述子をコピーし、その型記述子をメソッドの入力パラメーターに貼り付けることができ `CreateCustomer` ます。 これにより、同じ型記述子を複数回定義する必要がなくなります。

## <a name="method-instances"></a>メソッドインスタンス
 メソッドを作成すると、Visual Studio によって既定のメソッドインスタンスが追加されます。 メソッドインスタンスは、メソッドへの参照と、パラメーターの既定値を加えたものです。 1つのメソッドには、複数のメソッドインスタンスを含めることができます。 各インスタンスは、メソッドシグネチャと一連の既定値を組み合わせたものです。 詳細については、「 [方法: パラメーターの型記述子を定義](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)する」を参照してください。

 プロジェクトを実行すると、SharePoint リストの上のドロップダウンリストにメソッドインスタンスが表示されます。 ユーザーは、メソッドインスタンスを選択してデータを表示できます。

 メソッドインスタンスに既定値を追加するには、モデルの XML を直接変更する必要があります。 詳細については、「 [DefaultValue](/previous-versions/office/developer/sharepoint-2010/ee559319(v=office.14))」を参照してください。

## <a name="add-filter-descriptors"></a>フィルター記述子の追加
 モデルのコンシューマーは、何らかの条件に一致するエンティティのインスタンスを取得することが必要になる場合があります。 この機能を有効にするには、メソッドにフィルター記述子を追加します。 フィルター記述子を使用すると、モデルコンシューマーは、実行前にメソッドに値を渡すことによって、メソッドの結果セットをフィルター処理できます。 詳細については、「 [方法: フィルターパラメーターを操作に追加して、外部システムからインスタンスを制限する](/previous-versions/office/developer/sharepoint-2010/ee554889(v=office.14))」を参照してください。

 SharePoint には、ユーザーがフィルター値を提供できるようにする機能がいくつか用意されています。 たとえば、ビジネスデータ Web パーツはフィルターテキストボックスを提供します。 ユーザーは、テキストボックスに値を入力することによって、リスト内のデータを制限できます。 メソッドにフィルター記述子を追加する方法の詳細については、「 [方法: フィルター記述子を Finder メソッドに追加](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)する」を参照してください。

### <a name="filter-descriptor-properties"></a>フィルター記述子のプロパティ
 フィルター記述子の **関連付けられている型記述子**、 **名前**、および **型** プロパティの値を設定する必要があります。 その他のすべてのプロパティは省略可能です。

 **関連付けられている型記述子**プロパティは、フィルター記述子を入力パラメーターに関連付けます。 ユーザーがフィルター値を指定すると、BDC サービスは入力パラメーターを使用してその値をメソッドに渡します。

 **Type**プロパティは、使用するフィルターパターンを表します。 SharePoint では、選択したフィルターパターンが、ユーザーインターフェイス (UI) に表示されるテキストに影響します。 たとえば、比較子フィルターパターンの場合、テキスト **は** ビジネスデータ Web パーツ上のコントロールとして表示されます。 各フィルター処理パターンの詳細については、「 [BDC でサポートされるフィルターの種類](/previous-versions/office/developer/sharepoint-2010/ee556392(v=office.14))」を参照してください。

 フィルター記述子のプロパティの詳細については、「 [FilterDescriptor](/previous-versions/office/developer/sharepoint-2010/ee557835(v=office.14))」を参照してください。

### <a name="provide-default-values"></a>既定値を指定する
 場合によっては、ユーザーがフィルター値を提供しないことがあります。 既定値を指定するには、メソッドインスタンスに既定値を追加するか、メソッドのコードに既定値を設定します。 メソッドインスタンスに既定値を追加する方法の詳細については、「 [MethodInstance](/previous-versions/office/developer/sharepoint-2010/ee556838(v=office.14))」を参照してください。 メソッドのコードで入力パラメーターの既定値を設定する方法の例については、「 [方法: フィルター記述子を Finder メソッドに追加](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)する」を参照してください。

## <a name="validate-the-model"></a>モデルを検証する
 開発中にモデルを検証することができます。 Visual Studio は、モデルが想定どおりに動作しない原因となる可能性がある問題を特定します。 これらの問題は、Visual Studio **エラー一覧**に表示されます。

 モデルを検証するには、BDC デザイナーのショートカットメニューを開き、[ **検証**] をクリックします。 モデルにエラーが含まれている場合は、 **エラー一覧**に表示されます。 エラーが含まれているコードにカーソルをすばやく移動するには、一覧のエラーをダブルクリックします。 別の方法として、 **f8**キーまたは**Shift**f8 キーを繰り返しクリックして、一覧のエラーを順 + **F8**方向または逆方向に移動することもできます。

 検証エラーは、何らかの方法でモデルのルールに違反した場合に発生する可能性があります。 たとえば、型記述子の **IsCollection** プロパティが **true**に設定されていても、子の型記述子が存在しない場合、検証エラーが表示されます。 場合によっては、Visual Studio **エラー一覧**に表示されるいくつかのエラーを理解するために、BDC モデルの規則を参照する必要があります。 BDC モデルのルールの詳細については、「 [BDCMetadata Schema](/previous-versions/office/developer/sharepoint-2010/ee556387(v=office.14))」を参照してください。

## <a name="debug-the-solution-that-contains-the-model"></a>モデルを含むソリューションをデバッグする
 Visual Studio でコードをデバッグするのと同じように、コードをデバッグできます。 コードをデバッグするには、コード内の任意の場所にブレークポイントを設定し、デバッガーを起動します。 SharePoint サイトが開きます。 SharePoint で、ビジネスデータを使用するリストまたは Web パーツを作成します。 次に、コードをステップ実行できます。 SharePoint プロジェクトのデバッグの詳細については、「 [sharepoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」を参照してください。

 また、プロジェクトに追加するカスタムアセンブリのコードをデバッグすることもできます。 ただし、カスタムアセンブリ内のコードをデバッグするには、ソリューションパッケージにアセンブリを追加する必要があります。 詳細については、「 [方法: 追加のアセンブリを追加および削除](../sharepoint/how-to-add-and-remove-additional-assemblies.md)する」を参照してください。

 カスタムアセンブリをプロジェクトに追加する方法の詳細については、「 [方法: BDC 機能にカスタムアセンブリを含める](../sharepoint/how-to-include-a-custom-assembly-in-a-bdc-feature.md)」を参照してください。

### <a name="configure-bdc-security"></a>BDC のセキュリティを構成する
 ソリューションをデバッグする前に、SharePoint でセキュリティ設定を変更することが必要になる場合があります。 これらの設定を変更するには、SharePoint 2010 サーバーの全体管理 Web サイトでビジネスデータ接続サービスアプリケーションを開きます。 [ **メタデータストアのアクセス許可の設定** ] ダイアログボックスで、ユーザーアカウントを追加し、次のいずれかのオプションを選択します。

|タスク|オプション|
|----------|------------|
|モデルを BDC サービスにデプロイするには|[編集]|
|モデルで外部コンテンツタイプ (エンティティ) を使用してリストを作成し、Web パーツします。|選択可能なクライアント|
|エンティティデータの作成、読み取り、更新、および削除を行います。|実行|

 これらの設定の詳細については、「 [ビジネスデータ接続サービスの管理](/previous-versions/office/sharepoint-server-2010/ee661742(v=office.14))」を参照してください。

 また、個々のモデルまたは外部コンテンツタイプに対してセキュリティのアクセス許可を設定することもできます。 モデルのセキュリティアクセス許可を設定する方法の詳細については、「 [BDC モデル管理](/previous-versions/office/sharepoint-server-2010/ee524073(v=office.14))」を参照してください。 外部コンテンツタイプのセキュリティアクセス許可を設定する方法の詳細については、「 [外部コンテンツタイプの管理](/previous-versions/office/sharepoint-server-2010/ee524076(v=office.14))」を参照してください。

> [!NOTE]
> ローカルの SharePoint サーバー上のソリューションをデバッグするには、これらの設定を使用します。 運用 SharePoint サーバーで BDC 関連のセキュリティ設定を構成する方法の詳細については、「 [ビジネスデータ接続サービスのセキュリティの概要](/previous-versions/office/sharepoint-server-2010/ee661743(v=office.14))」を参照してください。

### <a name="retract-models-that-become-corrupt"></a>破損したモデルを取り消す
 デバッガーを初めて起動すると、Visual Studio によってモデル全体が SharePoint に配置されます。 その後は、Visual Studio によって SharePoint のモデルが更新され、デプロイの間に加えられた変更が反映されます。

 Visual Studio で SharePoint からモデルを完全に取り消すことが必要になる場合があります。 たとえば、モデルが破損している可能性があります。  モデルを SharePoint に再配置するには、モデルの " **増分更新** " プロパティを **False**に設定し、デバッガーを起動します。 **BDC エクスプローラー**でモデルを表すノードを選択すると、[**プロパティ**] ウィンドウに [**増分更新**] プロパティが表示されます。 既定では、モデルの名前は **BdcModel1**です。

### <a name="change-identifier-names-of-entities-in-the-model"></a>モデル内のエンティティの識別子名を変更する
 モデルの配置後に識別子の名前を変更すると、デプロイエラーが発生することがあります。 このエラーを解決するには、モデルの " **増分更新** " プロパティを **False**に設定します。 モデルを手動で取り消してから、ソリューションをもう一度配置する必要があります。 詳細については、「 [SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)」を参照してください。 このエラーを回避するには、最初にモデルを配置する前に " **増分更新** " プロパティを **False** に設定します。

## <a name="locate-documentation-for-bdc-model-elements"></a>BDC モデル要素のドキュメントを検索する
 Visual Studio では、作成した各エンティティ、メソッド、またはその他のアイテムのモデルに XML 要素が追加されます。 要素の属性は、[ **プロパティ** ] ウィンドウにプロパティとして表示されます。 モデルの設計時に Visual Studio によって生成される要素と属性の詳細については、「 [BDCMetadata Schema](/previous-versions/office/developer/sharepoint-2010/ee556387(v=office.14))」を参照してください。

## <a name="related-topics"></a>関連トピック

|Title|説明|
|-----------|-----------------|
|[BDC モデルのデザインツールの概要](../sharepoint/bdc-model-design-tools-overview.md)|BDC のモデルを視覚的に設計するために使用できるツールについて説明します。|
|[方法: モデルにエンティティを追加する](../sharepoint/how-to-add-an-entity-to-a-model.md)|外部コンテンツの種類 (エンティティ) をモデルに追加する方法について説明します。|
|[方法: Finder メソッドを追加する](../sharepoint/how-to-add-a-finder-method.md)|ユーザーがリストまたは Web パーツのエンティティの一覧を表示できるようにするメソッドを追加する方法について説明します。|
|[方法: 特定の Finder メソッドを追加する](../sharepoint/how-to-add-a-specific-finder-method.md)|特定のエンティティの詳細をユーザーが表示できるようにするメソッドを追加する方法について説明します。|
|[方法: Creator メソッドを追加する](../sharepoint/how-to-add-a-creator-method.md)|ユーザーがリストまたは Web パーツから直接データソースにレコードを追加できるようにするメソッドを追加する方法について説明します。|
|[方法: 削除子メソッドを追加する](../sharepoint/how-to-add-a-deleter-method.md)|ユーザーがリストまたは Web パーツのユーザーインターフェイス (UI) のオプションを使用してデータソースからデータを削除できるようにするメソッドを追加する方法について説明します。|
|[方法: Updater メソッドを追加する](../sharepoint/how-to-add-an-updater-method.md)|ユーザーがデータソースのデータレコードをリストまたは Web パーツから直接変更できるようにするメソッドを追加する方法について説明します。|
|[方法: メソッドにパラメーターを追加する](../sharepoint/how-to-add-a-parameter-to-a-method.md)|Visual Studio の [メソッドの詳細] ウィンドウを使用して、入力パラメーターと戻りパラメーターをメソッドに追加する方法について説明します。|
|[方法: パラメーターの型記述子を定義する](../sharepoint/how-to-define-the-type-descriptor-of-a-parameter.md)|モデルでパラメーターのデータ型を定義する方法について説明します。|
|[方法: メソッドインスタンスを定義する](../sharepoint/how-to-define-a-method-instance.md)|BDC で実行されるメソッドのインスタンスを作成する方法について説明します。|
|[方法: Finder メソッドにフィルター記述子を追加する](../sharepoint/how-to-add-a-filter-descriptor-to-a-finder-method.md)|Finder メソッドによって返されるインスタンスの数をユーザーが制限できるようにする方法について説明します。|
|[エンティティ間の関連付けの作成](../sharepoint/creating-an-association-between-entities.md)|モデル内のエンティティ間のリレーションシップを定義する方法について説明します。 ビジネスデータ Web パーツ、外部リスト、およびカスタムアプリケーションでは、これらのデータリレーションシップをユーザーインターフェイス (UI) に表示できます。|
|[方法: エンティティ間の関連付けを作成する](../sharepoint/how-to-create-an-association-between-entities.md)|モデル内のエンティティ間のリレーションシップを定義する方法について説明します。|
|[チュートリアル: ビジネスデータを使用して SharePoint の外部リストをするする](../sharepoint/walkthrough-creating-an-external-list-in-sharepoint-by-using-business-data.md)|SharePoint 外部リストに連絡先を表示するモデルを作成してテストする方法について、手順を追って説明します。|
|[SharePoint へのビジネスデータの統合](../sharepoint/integrating-business-data-into-sharepoint.md)|BDC サービスのモデルの作成と設計の概要について説明します。|
