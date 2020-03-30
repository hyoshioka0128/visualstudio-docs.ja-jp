---
title: ワークフロー デザイナー - 送信アクティビティ デザイナー
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- System.ServiceModel.Activities.Send.UI
ms.assetid: b514f2e4-767c-4b94-ac61-dd3a54d4b96d
author: jillre
ms.author: jillfra
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8690d5ccf18c752aacb37a71243d9f591fb9ee30
ms.sourcegitcommit: d6828e7422c8d74ec1e99146fedf0a05f757245f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2020
ms.locfileid: "80395220"
---
# <a name="send-activity-designer"></a>Send アクティビティ デザイナー

**Send**アクティビティ デザイナーは、アクティビティを作成および<xref:System.ServiceModel.Activities.Send>構成するために使用します。

## <a name="the-send-activity"></a>Send アクティビティ

 メッセージをサービスに送信するには、<xref:System.ServiceModel.Activities.Send> アクティビティを使用します。 <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティは、クライアントでの要求/応答メッセージ交換パターンの一部としてメッセージを受信する <xref:System.ServiceModel.Activities.Send> アクティビティにバインドできます。

### <a name="using-the-send-activity-designer"></a>Send アクティビティ デザイナーの使用

**[ツールボックス**] の [**メッセージング**] カテゴリにある **[送信**] アクティビティ デザイナにアクセスします。 **送信**アクティビティ デザイナーは **、ツールボックス**からドラッグして、アクティビティが通常配置されているワークフロー デザイナー画面にドロップできます。 この操作により、Send という既定の <xref:System.ServiceModel.Activities.Send> を持つ <xref:System.Activities.Activity.DisplayName%2A> アクティビティが作成されます。 は<xref:System.Activities.Activity.DisplayName%2A>、**送信**アクティビティ デザイナーのヘッダーまたはプロパティ グリッドの **[表示名**] ボックスで編集できます。

アクティビティを<xref:System.ServiceModel.Activities.ReceiveReply>作成して選択した<xref:System.ServiceModel.Activities.Send>アクティビティにバインドするには、**送信**アクティビティ デザイナーを右クリックし、コンテキスト メニューの **[受信返信の作成**] 項目をクリックすると **、Send**デザイナーの下に**ReceiveReplyForSend**デザイナーが表示されます。 <xref:System.ServiceModel.Activities.ReceiveReply> アクティビティは、クライアントでの要求/応答メッセージ交換パターンの一部としてメッセージを受信するアクティビティであり、 デザイナーを**使用**して構成できます。

または、**ツールボックス**の<xref:System.ServiceModel.Activities.Send>**メッセージング**カテゴリの**SendAndReceiveReply**テンプレート デザイナーを使用して、構成済みのアクティビティと<xref:System.ServiceModel.Activities.ReceiveReply>アクティビティのペアを作成できます。 **テンプレートの**使用の詳細については、[トピック](../workflow-designer/sendandreceivereply-template-designer.md)を参照してください。 **SendAndReceiveReply**

### <a name="the-send-activity-properties"></a>Send アクティビティのプロパティ

次の表に、<xref:System.ServiceModel.Activities.Send> のプロパティと、デザイナーでのその使用方法を示します。 これらのプロパティは、プロパティ グリッドまたはワークフロー デザイナー画面で編集できます。

| プロパティ名 | 必須 | 使用法 |
|-|----------|-|
| <xref:System.Activities.Activity.DisplayName%2A> | False | <xref:System.ServiceModel.Activities.Send> アクティビティの表示名。 既定値は Send です。 <xref:System.Activities.Activity.DisplayName%2A> は必須ではありませんが、使用することをお勧めします。 |
| <xref:System.ServiceModel.Activities.Send.OperationName%2A> | True | この <xref:System.ServiceModel.Activities.Send> アクティビティによって呼び出されるサービス操作の名前。 このプロパティは **、Action**プロパティが明示的に設定されていない場合に**Action**プロパティの既定値を作成するために使用されます。 |
| <xref:System.ServiceModel.Activities.Send.ServiceContractName%2A> | True | 呼び出されるサービスが実装するサービス コントラクトの名前。 |
| <xref:System.ServiceModel.Activities.Send.Content%2A> | False | 受信するメッセージまたはパラメーターの内容を指定します。 <xref:System.ServiceModel.Activities.ReceiveMessageContent> アクティビティまたは <xref:System.ServiceModel.Activities.ReceiveParametersContent> アクティビティを指定できます。 このプロパティを編集するには、プロパティ グリッドの **[コンテンツ]** フィールドの横にある省略記号ボタンを選択するか **、または Receive**アクティビティ デザイナー画面の **[コンテンツ]** ラベルの横にある [**定義..** ] ボタンをクリックします。 両方とも **[コンテンツ定義]ダイアログボックス**を表示します。 このボックスの使用方法の詳細については[、「[コンテンツ定義] ダイアログ ボックス」を](../workflow-designer/content-definition-dialog-box.md)参照してください。 |
| <xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A> | False | 適切なワークフロー インスタンスにメッセージをルーティングするために使用される <xref:System.ServiceModel.Activities.CorrelationHandle> を指定します。<br /><br /> プロパティ グリッドで<xref:System.ServiceModel.Activities.Send.CorrelatesWith%2A>プロパティの横にある省略記号ボタンをクリックして、[**式エディター** ] ダイアログ ボックスを開きます。 このダイアログ ボックスの使用方法の詳細については、「[方法: 式エディターの使用」](../workflow-designer/how-to-use-the-expression-editor.md)を参照してください。 |
| <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> | False | ワークフロー内のこの <xref:System.ServiceModel.Activities.CorrelationInitializer> アクティビティを構成する複数の <xref:System.ServiceModel.Activities.CorrelationHandle> オブジェクトを初期化する <xref:System.ServiceModel.Activities.Send> オブジェクトのコレクションを指定します。 プロパティ グリッドで<xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A>プロパティの横にある省略記号ボタンをクリックして、[**相互関係初期化子の追加**] ダイアログ ボックスを開きます。 このボックスの使用方法の詳細については[、「[相互関係初期化子の追加] ダイアログ ボックス」を参照してください](../workflow-designer/add-correlationinitializers-dialog-box.md)。 |
| <xref:System.ServiceModel.Activities.Send.KnownTypes%2A> | False | この <xref:System.ServiceModel.Activities.Send> アクティビティによって呼び出されるサービス操作の既知の型のコレクション。 このプロパティは、<xref:System.ServiceModel.Activities.Receive.SerializerOption%2A> に設定された <xref:System.Runtime.Serialization.DataContractSerializer> プロパティと共に使用する必要があります。 <xref:System.Xml.Serialization.XmlSerializer> が使用されている場合は無視されます。<br /><br /> プロパティ グリッドの [**既知の種類]** フィールドの横にある省略記号ボタンを選択すると、関連する型を追加できる **[型コレクション エディター]** ダイアログが表示されます。<br /><br /> プロパティ グリッドの [**既知の種類]** フィールドの横にある省略記号ボタンを選択すると、関連する型を追加できる **[型コレクション エディター]** ダイアログ ボックスが表示されます。 このボックスの使用方法の詳細については、「[型コレクション エディターダイアログ ボックス」を](../workflow-designer/type-collection-editor-dialog-box.md)参照してください。 |
| <xref:System.ServiceModel.Activities.Send.ProtectionLevel%2A> | True | メッセージの <xref:System.Net.Security.ProtectionLevel> を指定します。<br /><br /> 1.<xref:System.Net.Security.ProtectionLevel>認証のみを意味します。<br />2.<xref:System.Net.Security.ProtectionLevel>送信されたデータの整合性を確保するために、データに署名することを意味します。<br />3.<xref:System.Net.Security.ProtectionLevel>データの暗号化と署名を行い、送信データの機密性と整合性を確保します。 |
| <xref:System.ServiceModel.Activities.Send.SerializerOption%2A> | True | <xref:System.ServiceModel.Activities.Send> アクティビティによって呼び出されるサービス操作に使用するシリアライザー。 既定値は <xref:System.Runtime.Serialization.DataContractSerializer> です。このシリアライザーは、ある型のインスタンスを、提供されたデータ コントラクトを使用する XML ストリームまたはドキュメントへとシリアル化または逆シリアル化します。 |
| <xref:System.ServiceModel.Activities.Send.Action%2A> | False | メッセージのアクション ヘッダーを指定します。 明示的に設定されていない場合、その値はデフォルトで: です`https://tempuri.org/{service contract namespace}/{service contract name}/{operation name}`。 <xref:System.ServiceModel.Activities.Send> アクティビティで指定した場合は、メッセージを正しく配信するために、メッセージを受信する <xref:System.ServiceModel.Activities.Receive> アクティビティに同じ値を設定する必要があります。 |
| <xref:System.ServiceModel.Activities.Send.TokenImpersonationLevel%2A> | | メッセージの受信側に許可される <xref:System.Security.Principal.TokenImpersonationLevel>。 このクラスは、サーバー プロセスがクライアント プロセスの代わりに動作できる度合いを制御するセキュリティ偽装レベルを定義します。<xref:System.Security.Principal.TokenImpersonationLevel>  は、偽装レベルが割り当てられていないことを示します。 <xref:System.Security.Principal.TokenImpersonationLevel>サーバー プロセスがクライアントに関する識別情報を取得できず、クライアントを偽装できないことを示します。 <xref:System.Security.Principal.TokenImpersonationLevel>サーバー プロセスは、セキュリティ識別子や特権などのクライアントに関する情報を取得できるが、クライアントを偽装できないことを示します。 これは、テーブルとビューをエクスポートするデータベース製品など、独自のオブジェクトをエクスポートするサーバーで役立ちます。 サーバーは、このクライアントのセキュリティ コンテキストを使用する他のサービスを使用できなくても、取得したクライアントのセキュリティ情報を使用してアクセス検証に関する決定を行うことができます。 <xref:System.Security.Principal.TokenImpersonationLevel>サーバー プロセスがローカル システム上でクライアントのセキュリティ コンテキストを偽装できることを示します。 サーバーは、リモート システムにあるクライアントを偽装できません。 <xref:System.Security.Principal.TokenImpersonationLevel>サーバー プロセスがリモート システム上のクライアントのセキュリティ コンテキストを偽装できることを示します。 |
| <xref:System.ServiceModel.Activities.Send.Endpoint%2A> | | <xref:System.ServiceModel.Endpoint> アクティビティによるメッセージの送信先の <xref:System.ServiceModel.Activities.Send>。 このプロパティを設定する場合<xref:System.ServiceModel.Activities.Send.EndpointConfigurationName%2A>、プロパティは**null**にする必要があります。 |
| <xref:System.ServiceModel.Activities.Send.EndpointAddress%2A> | | メッセージの送信先となる <xref:System.ServiceModel.EndpointAddress>。 |
| <xref:System.ServiceModel.Activities.Send.EndpointConfigurationName%2A> | | エンドポイント構成の名前。 このプロパティは、エンドポイントを構成ファイルで構成している場合に設定します。 このプロパティは、構成ファイルの**\<エンドポイント>** 要素に指定された名前に設定する必要があります。 このプロパティが設定されている場合、<xref:System.ServiceModel.Activities.Send.Endpoint%2A>プロパティは**null**にする必要があります。 |

## <a name="see-also"></a>関連項目

- [InitializeCorrelation](../workflow-designer/initializecorrelation-activity-designer.md)
- [CorrelationScope](../workflow-designer/correlationscope-activity-designer.md)
- [ReceiveAndSendReply](../workflow-designer/receiveandsendreply-template-designer.md)
- [受信](../workflow-designer/receive-activity-designer.md)
- [SendAndReceiveReply](../workflow-designer/sendandreceivereply-template-designer.md)
- [TransactedReceiveScope](../workflow-designer/transactedreceivescope-activity-designer.md)