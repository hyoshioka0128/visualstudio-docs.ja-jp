---
title: SharePoint ソリューションのデバッグ |Microsoft Docs
description: Visual Studio デバッガーを使用して SharePoint ソリューションをデバッグします。 F5 キーのデバッグと配置プロセス、ワークフローのデバッグ、および機能イベントレシーバーのデバッグについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.WebConfigModificationDialog
- VS.SharePointTools.Project.DebuggingNotEnabled
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, debugging
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: f1a6abfbafcbafb9daa52fdc6af85156700efef7
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99948948"
---
# <a name="debug-sharepoint-solutions"></a>SharePoint ソリューションのデバッグ
  SharePoint ソリューションは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デバッガーを使用してデバッグできます。 デバッグを開始すると、に [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] よってプロジェクトファイルが sharepoint サーバーに配置され、Web ブラウザーで sharepoint サイトのインスタンスが開かれます。 以下のセクションでは、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で SharePoint アプリケーションをデバッグする方法について説明します。

- [デバッグの有効化](#enable-debugging)

- [F5 キーのデバッグと配置のプロセス](#f5-debug-and-deployment-process)

- [SharePoint プロジェクトの機能](#sharepoint-project-features)

- [デバッグ ワークフロー](#debug-workflows)

- [フィーチャーイベントレシーバーのデバッグ](#debug-feature-event-receivers)

- [Ehanced デバッグ情報を有効にする](#enable-enhanced-debugging-information)

## <a name="enable-debugging"></a>デバッグの有効化
 SharePoint ソリューションを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で初めてデバッグするとき、デバッグを有効にするように web.config ファイルが構成されていないことを警告するダイアログ ボックスが表示されます。 web.config ファイルは SharePoint サーバーのインストール時に作成されます。 詳細については、「 [Web.config ファイルの操作](/previous-versions/office/developer/sharepoint-2010/ms460914(v=office.14))」を参照してください)。このダイアログボックスには、デバッグまたは web.config ファイルの変更を行わずにプロジェクトを実行して、デバッグを有効にするオプションが表示されます。 前者を選択した場合、プロジェクトは通常どおりに実行されます。 後者を選択した場合、web.config ファイルは次のように構成されます。

- 呼び出し履歴は有効にする (`CallStack="true"`)

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]() でカスタムエラーを無効にする `<customErrors mode="Off" />`

- コンパイル デバッグは有効にする (`<compilation debug="true">`)

  結果として生成される web.config ファイルは、次のとおりです。

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
    <configuration>
        ...
        <SharePoint>
            <SafeMode MaxControls="200"
                CallStack="true"
                DirectFileDependencies="10"
                TotalFileDependencies="50"
                AllowPageLevelTrace="false">
                ...
            </SafeMode>
        ...
        </SharePoint>
        <system.web>
            ...
            <customErrors mode="Off" />
            ...
            <compilation debug="true">
            ...
            </compilation>
            ...
        </system.web>
        ...
    </configuration>
```

 変更を元に戻してデバッグを無効にするには、web.config ファイルで次のように変更し [!INCLUDE[TLA2#tla_xml](../sharepoint/includes/tla2sharptla-xml-md.md)] ます。

- 呼び出し履歴は無効にする (`CallStack="false"`)

- [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]() でカスタムエラーを有効にする `<customErrors mode="On" />`

- コンパイル デバッグは無効にする (`<compilation debug="false">`)

## <a name="f5-debug-and-deployment-process"></a>F5 キーのデバッグと配置のプロセス
 SharePoint プロジェクトをデバッグ モードで実行するとき、SharePoint の配置プロセスによって、次のタスクが実行されます。

1. カスタマイズ可能な配置前コマンドが実行されます。

2. [!INCLUDE[vstecmsbuild](../sharepoint/includes/vstecmsbuild-md.md)] コマンドを使用して、Web ソリューション パッケージ (.wsp) ファイルが作成されます。 この .wsp ファイルには、すべての必要なファイルおよびフィーチャーが含まれます。 詳細については、「 [ソリューションの概要](/previous-versions/office/developer/sharepoint-2010/aa543214(v=office.14))」を参照してください。

3. SharePoint ソリューションがファーム ソリューションである場合は、指定されたサイトの [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] の [!INCLUDE[TLA2#tla_url](../sharepoint/includes/tla2sharptla-url-md.md)] アプリケーション プールがリサイクルされます。 この段階で、[!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] のワーカー プロセスによってロックされたファイルが解放されます。

4. 以前のバージョンのパッケージが既に存在する場合は、.wsp ファイル内の以前のバージョンのフィーチャーおよびファイルが取り消されます。 この段階で、フィーチャーが非アクティブ化され、ソリューション パッケージがアンインストールされた後に、ソリューション パッケージが SharePoint サーバーから削除されます。

5. .wsp ファイル内の最新のバージョンのフィーチャーおよびファイルがインストールされます。 この段階で、SharePoint サーバーにソリューションが追加され、インストールされます。

6. ワークフローの場合は、ワークフロー アセンブリがインストールされます。 その場所は、" *アセンブリの場所* " プロパティを使用して変更できます。

7. スコープがサイトまたは Web の場合は、SharePoint でプロジェクトのフィーチャーがアクティブ化されます。 ファーム スコープおよび Web アプリケーション スコープのフィーチャーはアクティブ化されません。

8. ワークフローの場合、は、 **Sharepoint カスタマイズウィザード** で選択した sharepoint ライブラリ、リスト、またはサイトにワークフローを関連付けます。

   > [!NOTE]
   > この関連付けは、ウィザードで [ **ワークフローを自動的に関連付ける** ] を選択した場合にのみ発生します。

9. カスタマイズ可能な配置後コマンドが実行されます。

10. デバッガーを [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] プロセスにアタッチし [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] ます (*w3wp.exe*)。 プロジェクトの種類で *サンドボックスソリューション* のプロパティを変更でき、その値が **true** に設定されている場合、デバッガーは別のプロセス (*SPUCWorkerProcess.exe*) にアタッチします。 詳細については、「 [サンドボックスソリューションの考慮事項](../sharepoint/sandboxed-solution-considerations.md)」を参照してください。

11. SharePoint ソリューションがファーム ソリューションである場合は、JavaScript デバッガーが開始されます。

12. 適切なライブラリ、リスト、またはサイト ページが Web ブラウザーに表示されます。

    [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 各タスクが完了すると、ステータスメッセージが [出力] ウィンドウに表示されます。 タスクを完了できなかった場合は、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] の [エラー一覧] ウィンドウにエラー メッセージが表示されます。

## <a name="sharepoint-project-features"></a>SharePoint プロジェクトの機能
 フィーチャーは、サイト定義を使用することによってサイトの変更を単純化する、移植性のあるモジュール式の機能単位です。 また、 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] 特定のスコープに対してアクティブ化し、ユーザーが特定の目標やタスクを達成するのに役立つ (WSS) 要素のパッケージでもあります。 テンプレートはフィーチャーとして配置されます。

 デバッグモードでプロジェクトを実行すると、配置プロセスによって、 *%COMMONPROGRAMFILES%\Microsoft Shared\web server extensions\14\TEMPLATE\FEATURES* の *機能* ディレクトリにフォルダーが作成されます。 機能名には、 *プロジェクト名* _Feature *x* の形式 (TestProject_Feature1 など) があります。

 フィーチャーディレクトリ内のソリューションのフォルダーには、 *機能定義* ファイルと *ワークフロー定義* ファイルが含まれています。 フィーチャー定義ファイル (Feature.xml) は、プロジェクトの機能のファイルについて記述します。プロジェクト定義ファイル (*Elements.xml*) には、プロジェクトテンプレートが記述されています。 *Elements.xml* は **ソリューションエクスプローラー** にありますが、ソリューションパッケージの作成時に Feature.xml が生成されます。 これらのファイルの詳細については、「 [SharePoint プロジェクトとプロジェクト項目テンプレート](../sharepoint/sharepoint-project-and-project-item-templates.md)」を参照してください。

## <a name="debug-workflows"></a>デバッグ ワークフロー
 ワークフロー プロジェクトをデバッグすると、その種類に応じたワークフロー テンプレートが [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] によってライブラリまたはリストに追加されます。 このワークフロー テンプレートは手動で開始できるほか、項目を追加または更新することによって開始することもできます。 これで、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] を使用してワークフローをデバッグできます。

> [!NOTE]
> 他のアセンブリへの参照を追加する場合は、それらのアセンブリがグローバルアセンブリキャッシュ () にインストールされていることを確認してください [!INCLUDE[TLA2#tla_gac](../sharepoint/includes/tla2sharptla-gac-md.md)] 。 そうしないと、ワークフロー ソリューションは失敗します。 アセンブリをインストールする方法の詳細については、「 [ドキュメントまたはアイテムでワークフローを手動で開始](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963)する」を参照してください。

 ただし、配置プロセスでは、ワークフローは開始されません。 SharePoint Web サイトからワークフローを開始する必要があります。 Microsoft Office Word 2010 などのクライアント アプリケーションや別個のサーバー側のコードを使用して、ワークフローを開始することもできます。 **SharePoint カスタマイズウィザード** で指定されたいずれかの方法を使用します。

 たとえば、ワークフローの手動での開始を許可した場合は、ライブラリまたはリスト内のアイテムから、ワークフローを直接開始します。 ワークフローを手動で開始する方法の詳細については、「 [ドキュメントアイテムでワークフローを手動で開始](https://support.office.com/article/Manually-start-a-workflow-on-a-document-or-item-5C106E0E-6FF2-4A75-AF99-F01653BC7963)する」を参照してください。

## <a name="debug-feature-event-receivers"></a>フィーチャーイベントレシーバーのデバッグ
 既定では、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] SharePoint アプリケーションを実行すると、そのフィーチャーが SharePoint サーバー上で自動的にアクティブ化されます。 ただし、フィーチャーイベントレシーバーをデバッグするときに問題が発生します。これは、フィーチャーがによってアクティブ化された場合、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] デバッガーとは異なるプロセスで実行されるためです。 つまり、ブレークポイントなどの一部のデバッグ機能が正常に機能しなくなるということです。

 SharePoint で機能の自動アクティブ化を無効にして、機能イベントレシーバーを適切にデバッグできるようにするには、デバッグの前に、プロジェクトの **アクティブな配置構成** プロパティの値を [アクティブ **化なし** ] に設定します。 そのうえで、[!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] で SharePoint アプリケーションのデバッグを開始してから、SharePoint でフィーチャーを手動でアクティブ化します。 この機能をアクティブにするには、SharePoint で [ **サイトの操作** ] メニューを開き、[ **サイトの設定**] を選択します。次に、[ **サイト機能の管理** ] リンクを選択し、機能の横にある [ **アクティブ化** ] ボタンを選択して、通常どおりにデバッグを続行します。

## <a name="enable-enhanced-debugging-information"></a>強化されたデバッグ情報を有効にする
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]プロセス (devenv.exe)、sharepoint [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ホストプロセス (*vssphost4.exe*)、sharepoint、および WCF 層との間の対話が複雑になることがあるため、構築や配置などの際に発生するエラーを診断するのは困難な場合があります。 拡張デバッグ情報を有効にすると、こうしたエラーが解決しやすくなります。 これを行うには、まず Windows レジストリで次のレジストリ キーに移動します。

 **HKEY_CURRENT_USER\Software\Microsoft\VisualStudio\11.0\SharePointTools**

 "EnableDiagnostics" **REG_DWORD** 値がまだ存在しない場合は、手動で作成します。 "EnableDiagnostics" の値を "1" に設定します。

 このキー値を1に設定すると、での実行中にプロジェクトシステムエラーが発生するたびに、スタックトレース情報が **出力** ウィンドウに表示され [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] ます。 強化されたデバッグ情報を無効にするには、EnableDiagnostics を 0 に戻すか、この値を削除します。

 その他の SharePoint レジストリキーの詳細については、「 [Visual Studio での sharepoint ツールの拡張機能のデバッグ](../sharepoint/debugging-extensions-for-the-sharepoint-tools-in-visual-studio.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [SharePoint ソリューションのトラブルシューティング](../sharepoint/troubleshooting-sharepoint-solutions.md)
