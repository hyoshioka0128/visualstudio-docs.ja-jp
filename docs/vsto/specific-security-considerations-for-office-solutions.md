---
title: Office ソリューションに関する特定のセキュリティの考慮事項
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- troubleshooting Office development in Visual Studio, security
- trusted code [Office development in Visual Studio]
- blocked code [Office development in Visual Studio]
- Outlook [Office development in Visual Studio], object model guard
- malicious code [Office development in Visual Studio]
- Outlook object model guard [Office development in Visual Studio]
- security [Office development in Visual Studio], troubleshooting
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 571b604b87fb7fac4e78c83a791c265d910fae94
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72985580"
---
# <a name="specific-security-considerations-for-office-solutions"></a>Office ソリューションに関する特定のセキュリティの考慮事項
  Microsoft .NET Framework および Microsoft Office には、Office ソリューションをセキュリティ上の脅威から保護するためのセキュリティ機能が備わっています。 このトピックでは、このような脅威のいくつかについて説明し、脅威対策に関する推奨事項を示します。 また、Microsoft Office のセキュリティ設定が Office ソリューションに及ぼす影響についても説明します。

 [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="trusted-code-is-repurposed-in-a-new-malicious-document"></a>信頼できるコードは、新しい悪意のあるドキュメントで転用されます。
 攻撃者は、たとえば、個人情報をダウンロードするための雇用アプリケーションのコードなど、ある特定の用途のための信頼されたコードを取得し、ワークシートなどの別のドキュメントでそのコードを再利用する可能性があります。 コードは元のドキュメントが実行されていないことを認識しないため、別のユーザーが開いた場合に他の脅威 (個人情報の漏洩や拡大された権限によるコードの実行など) を招くことがあります。 また、攻撃者は、ワークシート内のデータを変更することもできます。これにより、被害者に送信されると、予期せずに動作します。 悪意を持つユーザーは、コードにリンクされているワークシートの値、数式、または表示特性を変更して、変更後のファイルを送りつけて別のユーザーを攻撃する可能性があります。 また、ワークシートの値を修正して、許可されていない情報にアクセスすることもできます。

 実行するには、アセンブリの位置とドキュメントの位置の両方の証拠が十分でなければならないため、このような攻撃は簡単には実行できません。 たとえば、電子メール添付ファイルのドキュメントや信頼されていないイントラネット サーバーのドキュメントには、実行に必要なアクセス許可がありません。

 このような攻撃を可能にするには、コード自体が、信頼できない可能性のあるデータに基づいて決定を下すように作成されていなければなりません。 たとえば、非表示のセルにデータベース サーバーの名前を含むワークシートを作成するとします。 ユーザーがこのワークシートを ASPX ページに送信すると、SQL 認証およびハードコーディングされた SA パスワードを使用してそのサーバーに接続しようとします。 攻撃者は、非表示のセルの内容を別のコンピューター名に置き換え、SA パスワードを取得する可能性があります。 このような問題を回避するために、絶対にパスワードはハードコーディングしないでください。また、サーバーにアクセスする前に、必ず、既知の信頼できるサーバーを示す内部リストでそのサーバー ID を確認してください。

### <a name="recommendations"></a>推奨事項

- 入力内容およびデータのソースが、ユーザー、ドキュメント、データベース、Web サービス、その他のソースのどれであるかを常に確認してください。

- 特定の種類の機能を公開する場合には、注意が必要です。たとえば、権限の設定されたデータをユーザーに代わって取得し、保護されていないワークシートにこのデータを挿入する場合に注意が必要となります。

- アプリケーションの種類によっては、元のドキュメントが実行されていることを検証してからコードを実行することが有効な対策になります。 たとえば、既知の安全な場所に保存されているドキュメントから実行されていることを検証します。

- 権限の設定されたアクションを実行するアプリケーションの場合は、ドキュメントを開くときに警告メッセージを表示することをお勧めします。 たとえば、アプリケーションが個人情報にアクセスすることを知らせるスプラッシュ スクリーンやスタートアップのダイアログ ボックスを作成して、ユーザーに操作の続行またはキャンセルを選択してもらうことができます。 エンド ユーザーは、一見無害なドキュメントからこのような警告が表示された場合に、情報が漏洩する前にアプリケーションを終了できます。

## <a name="code-is-blocked-by-the-outlook-object-model-guard"></a>Outlook オブジェクトモデルの保護によってコードがブロックされる
 Microsoft Office では、オブジェクト モデルの特定のプロパティ、メソッド、およびオブジェクトをコードで使用できないように制限できます。 これらのオブジェクトへのアクセスを制限することで、電子メールワームやウイルスによってオブジェクトモデルが悪意のある目的で使用されるのを防ぐことができます。 このセキュリティ機能は、Outlook オブジェクト モデルの保護と呼ばれています。 オブジェクトモデルの保護が有効になっているときに、VSTO アドインが制限されたプロパティまたはメソッドを使用しようとすると、ユーザーが操作を停止できるようにセキュリティ警告が表示されます。また、ユーザーは、一定期間内にプロパティまたはメソッドへのアクセスを許可することもできます。 ユーザーが操作を中断した場合、Visual Studio で Office ソリューションを使用して作成された Outlook VSTO アドインは <xref:System.Runtime.InteropServices.COMException>をスローします。

 オブジェクト モデルの保護の対象にできる VSTO アドインは、Outlook を Microsoft Exchange Server と併用しているかどうかに応じて、次のように異なります。

- Outlook を Exchange と併用していない場合、管理者は、コンピューター上のすべての VSTO アドインを対象として、オブジェクト モデルの保護を有効または無効にできます。

- Outlook を Exchange と併用している場合、管理者は、コンピューター上のすべての VSTO アドインを対象としてオブジェクト モデルの保護を有効または無効にできるのに加え、オブジェクト モデルの保護の対象外として動作させる特定の VSTO アドインを指定できます。 また、管理者は、オブジェクト モデルの特定の領域でのオブジェクト モデルの保護の動作を変更することもできます。 たとえば、管理者は、オブジェクトモデルの保護が有効になっている場合でも、プログラムを使用して VSTO アドインが自動的に電子メールを送信できるようにすることができます。

  Outlook 2007 以降、オブジェクト モデルの保護の動作は、Outlook のセキュリティを維持しながらも、開発者やユーザー エクスペリエンスを向上させるように変更されています。 詳細については、「 [Outlook 2007 でのコードセキュリティの変更点](/previous-versions/office/developer/office-2007/bb226709(v=office.12))」を参照してください。

### <a name="minimize-object-model-guard-warnings"></a>オブジェクトモデルの保護の警告を最小化する
 制限されたプロパティおよびメソッドを使用したときのセキュリティ警告を回避するには、VSTO アドインで、Outlook オブジェクトをプロジェクト内の `Application` クラスの `ThisAddIn` フィールドから取得するようにします。 このフィールドの詳細については、「 [PROGRAM VSTO アドイン](../vsto/programming-vsto-add-ins.md)」を参照してください。

 オブジェクト モデルの保護が信頼するのは、このオブジェクトから取得された Outlook オブジェクトのみです。 一方、新しい `Microsoft.Office.Interop.Outlook.Application` オブジェクトから取得したオブジェクトは信頼されないため、オブジェクト モデルの保護が有効になっている場合には、制限されたプロパティおよびメソッドでセキュリティ警告が発生します。

 次のコード例は、オブジェクト モデルの保護が有効になっている場合に、セキュリティの警告を表示します。 `Microsoft.Office.Interop.Outlook.MailItem` クラスの `To` プロパティは、オブジェクト モデルの保護によって制限されています。 `Microsoft.Office.Interop.Outlook.MailItem`オブジェクトは信頼されていません。これは、このオブジェクトを `Microsoft.Office.Interop.Outlook.Application` フィールドから取得するのではなく、 **new**演算子を使用して作成されたから取得するためです `Application` 。

 [!code-csharp[Trin_VstcoreOutlookSecurity#1](../vsto/codesnippet/CSharp/Trin_VstcoreOutlookSecurity/ThisAddIn.cs#1)]
 [!code-vb[Trin_VstcoreOutlookSecurity#1](../vsto/codesnippet/VisualBasic/Trin_VstcoreOutlookSecurity/ThisAddIn.vb#1)]

 次のコード例は、 `Microsoft.Office.Interop.Outlook.MailItem` オブジェクトモデルの保護によって信頼されているオブジェクトの Restricted to プロパティを使用する方法を示しています。 コードは、信頼される `Application` フィールドを使用して `Microsoft.Office.Interop.Outlook.MailItem` を取得します。

 [!code-csharp[Trin_VstcoreOutlookSecurity#2](../vsto/codesnippet/CSharp/Trin_VstcoreOutlookSecurity/ThisAddIn.cs#2)]
 [!code-vb[Trin_VstcoreOutlookSecurity#2](../vsto/codesnippet/VisualBasic/Trin_VstcoreOutlookSecurity/ThisAddIn.vb#2)]

> [!NOTE]
> Outlook を Exchange と併用している場合、すべての Outlook オブジェクトを `ThisAddIn.Application` から取得しても、VSTO アドインが Outlook オブジェクト モデル全体にアクセスできるとは限りません。 たとえば、Exchange 管理者が outlook オブジェクトモデルを使用してアドレス情報へのアクセスを自動的に拒否するように Outlook を設定した場合、コード例では信頼されたフィールドを使用していても、前のコード例で To プロパティにアクセスすることはできません `ThisAddIn.Application` 。

### <a name="specify-which-add-ins-to-trust-when-using-exchange"></a>Exchange を使用するときに信頼するアドインを指定する
 Outlook を Exchange と併用している場合、管理者は、オブジェクト モデルの保護の対象外として動作させる特定の VSTO アドインを指定できます。 Visual Studio で Office ソリューションを使用して作成した個別の Outlook VSTO アドインは信頼できません。これらはグループとしてのみ信頼できます。

 Outlook は、vsto アドインのエントリポイント DLL のハッシュコードに基づいて VSTO アドインを信頼します。 を対象とするすべての Outlook VSTO アドインは、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] 同じエントリポイント DLL (*VSTOLoader.dll*) を使用します。 つまり、管理者がを対象とする VSTO アドインを信頼して、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] オブジェクトモデルの保護を検出せずに実行する場合、を対象とする他のすべての vsto アドイン [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] も信頼されます。 特定の VSTO アドインを信頼してオブジェクト モデルの保護の対象外として動作させる方法の詳細については、 [「Outlook でウイルス対策機能を管理するために使用する方法を指定する」](/previous-versions/office/office-2007-resource-kit/cc179194(v=office.12))を参照してください。

## <a name="permission-changes-do-not-take-effect-immediately"></a>アクセス許可の変更はすぐには反映されません
 管理者がドキュメントまたはアセンブリのアクセス許可を調整した場合、それらの調整を適用させるには、ユーザーがすべての Office アプリケーションを終了して再起動する必要があります。

 Microsoft Office アプリケーションをホストする他のアプリケーションが原因で、新しいアクセス許可が適用されない場合もあります。 セキュリティ ポリシーが変更された場合、ユーザーは Office を使用するすべてのアプリケーションを (ホストされているか、スタンドアロンであるかを問わず) 終了してください。

## <a name="trust-center-settings-in-the-microsoft-office-system-do-not-affect-add-ins-or-document-level-customizations"></a>Microsoft Office システムのセキュリティセンターの設定がアドインまたはドキュメントレベルのカスタマイズに影響しない
 ユーザーは、 **セキュリティ センター**でオプションを設定して、VSTO アドインの読み込みを禁止できます。 ただし、Visual Studio で Office ソリューションを使用して作成される VSTO アドインとドキュメント レベルのカスタマイズには、これらのセキュリティ設定は影響しません。

 **セキュリティ センター**を使用して VSTO アドインの読み込みを禁止した場合、次のタイプのアドインは読み込まれません。

- マネージド COM VSTO アドインおよびアンマネージド COM VSTO アドイン。

- マネージド スマート ドキュメントおよびアンマネージド スマート ドキュメント。

- マネージド オートメーション VSTO アドインおよびアンマネージド オートメーション VSTO アドイン。

- マネージド リアルタイム データ コンポーネントおよびアンマネージド リアルタイム データ コンポーネント。

  次の手順では、ユーザーが **[セキュリティ センター]** を使用して、Microsoft [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] および Microsoft Office 2010 で VSTO アドインの読み込みを制限する方法について説明します。 これらの手順は、Visual Studio で Office 開発ツールを使用して作成された VSTO アドインまたはカスタマイズには影響しません。

#### <a name="to-disable-vsto-add-ins-in-microsoft-office-2010-and-microsoft-office_15_short-applications"></a>Microsoft Office 2010 および Microsoft [!INCLUDE[Office_15_short](../vsto/includes/office-15-short-md.md)] アプリケーションの VSTO アドインを無効にするには

1. **[ファイル]** タブを選択します。

2. *[ApplicationName* **オプション]** ボタンを選択します。

3. [カテゴリ] ウィンドウで **[セキュリティ センター]** を選択します。

4. 詳細ウィンドウで **[セキュリティ センターの設定]** を選択します。

5. [カテゴリ] ウィンドウで **[アドイン]** を選択します。

6. 詳細ウィンドウで **[アプリケーション アドインに対し、信頼できる発行元の署名を必須にする]** または **[すべてのアプリケーション アドインを無効にする]** を選択します。

## <a name="see-also"></a>こちらもご覧ください
- [セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)
