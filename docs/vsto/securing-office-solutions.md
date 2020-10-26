---
title: セキュリティで保護された Office ソリューション
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Office development in Visual Studio, security
- Office applications [Office development in Visual Studio], security
- security [Office development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 31a17fdf51e838405c93efca79d7994cd40ece5c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62978600"
---
# <a name="secure-office-solutions"></a>セキュリティで保護された Office ソリューション
  Office ソリューションのセキュリティモデルには、、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] 、Microsoft Office のセキュリティセンター、および Internet Explorer の制限付きサイトゾーンという、いくつかのテクノロジが含まれています。 次のセクションでは、さまざまなセキュリティ機能のしくみについて説明します:

- [Office ソリューションへの信頼の付与](#GrantingTrustToSolutions)

- [ドキュメントへの信頼の付与](#GrantingTrustToDocuments)

- [Windows インストーラーを使用するときに信頼を付与する](#GrantingTrustWindowsInstaller)

- [Office ソリューションに関する特定のセキュリティの考慮事項](#Security)

- [開発中のセキュリティ](#SecurityDuringDeployment)

- [Visual Studio Tools for Office Runtime](#VisualStudioToolsForOfficeRuntime)

  [!INCLUDE[appliesto_all](../vsto/includes/appliesto-all-md.md)]

## <a name="grant-trust-to-office-solutions"></a><a name="GrantingTrustToSolutions"></a> Office ソリューションへの信頼の付与
 Office ソリューションへの信頼の付与とは、以下の証拠に基づいて Office ソリューションを信頼するように各エンド ユーザーのセキュリティ ポリシーを変更することを意味します。

- 配置マニフェストへの署名に使用する証明書

- 配置マニフェストの URL

  詳細については、「 [Office ソリューションへの信頼の付与](../vsto/granting-trust-to-office-solutions.md)」を参照してください。

## <a name="grant-trust-to-documents"></a><a name="GrantingTrustToDocuments"></a> ドキュメントへの信頼の付与
 ドキュメント レベルのカスタマイズでは、ドキュメントを信頼できる場所として指定されたディレクトリに置く必要があります。  詳細については、「 [ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)」を参照してください。

## <a name="grant-trust-when-using-windows-installer"></a><a name="GrantingTrustWindowsInstaller"></a> Windows インストーラーを使用するときに信頼を付与する
 Windows インストーラーを使用して Program Files ディレクトリに Office ソリューションをインストールする MSI ファイルを作成できますが、これには管理者権限が必要です。 Program Files ディレクトリの Office ソリューションでは、Visual Studio 2010 Tools for Office runtime では、これらの Office ソリューションは信頼されていると見なされ、ClickOnce 信頼プロンプトは表示されません。

## <a name="specific-security-considerations-for-office-solutions"></a><a name="Security"></a> Office ソリューションに関する特定のセキュリティの考慮事項
 [!INCLUDE[net_v40_short](../sharepoint/includes/net-v40-short-md.md)]、[!INCLUDE[net_v45](../vsto/includes/net-v45-md.md)] および Microsoft Office に用意されているセキュリティ機能は、Office ソリューションのさまざまなセキュリティ上の脅威に対する保護に役立てることができます。 詳細については、「 [Office ソリューションのセキュリティに関する具体的な考慮事項](../vsto/specific-security-considerations-for-office-solutions.md)」を参照してください。

## <a name="security-during-development"></a><a name="SecurityDuringDeployment"></a> 開発中のセキュリティ
 Visual Studio では、開発プロセスを容易にするために、プロジェクトをビルドするたびにソリューションの実行およびデバッグに必要なセキュリティ ポリシーが設定されます。 場合によっては、プロジェクトの開発に追加のセキュリティ手順が必要になります。

### <a name="document-level-solutions"></a>ドキュメントレベルのソリューション
 次の種類のプロジェクトを開発する場合は、Microsoft Office アプリケーションの信頼できる場所の一覧にドキュメントの完全修飾パスを追加する必要があります。

- * \\ \Servername\sharename*などのネットワークファイル共有上にあるドキュメントレベルのソリューション。

- *.Doc*または *.docm*ファイルを使用する Word のドキュメントレベルのソリューション。

  ドキュメントの場所を信頼できる場所の一覧に追加するときにサブディレクトリを含めるか、デバッグ用のフォルダーとビルド用のフォルダーそれ自体を含めます。 詳細については、Microsoft Office オンラインヘルプの記事「 [ファイルの信頼できる場所を作成、削除、または変更](https://support.office.com/article/Create-remove-or-change-a-trusted-location-for-your-files-f5151879-25ea-4998-80a5-4208b3540a62)する」を参照してください。

### <a name="temporary-certificates"></a>一時的な証明書
 Visual Studio では、既存の署名証明書がない場合、一時的な証明書が作成されます。  一時的な証明書は開発時のみ使用し、配置には正式な証明書を購入する必要があります。

 一時的な証明書は、Office プロジェクトを最初にビルドした後に生成されます。 次に **F5**キーを押したときに、プロジェクトは再構築されます。これは、証明書が追加されたときにプロジェクトが変更済みとしてマークされているためです。

 時間の経過と共に多くの一時的な証明書が生成される可能性があるため、一時的な証明書を随時クリアする必要があります。

## <a name="visual-studio-tools-for-office-runtime"></a><a name="VisualStudioToolsForOfficeRuntime"></a> Visual Studio Tools for Office ランタイム
 に [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] は、パブリッシャーの id と、カスタマイズに付与されるアクセス許可を確認する機能があります。 アクセス許可を確認するときには、一連のセキュリティ チェックが実行されます。

### <a name="security-during-customization-loading"></a>カスタマイズの読み込み中のセキュリティ
 ドキュメントレベルのカスタマイズが読み込まれると、は、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] ドキュメントが信頼できる場所の一覧にあるかどうかを常に確認します。 また、ランタイムは、ソリューションがアプリケーション マニフェストに FullTrust を必要としているかどうかをチェックします。 カスタマイズの読み込み中に追加のセキュリティ チェックは行われません。

### <a name="sequence-of-security-checks-during-installation"></a>インストール中の一連のセキュリティチェック
 Office ソリューションをインストールまたは更新するときには、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] が一連のセキュリティ チェックを所定の順序で実行し、信頼の決定を行います。 ソリューションのインストールまたは更新は、ソリューションが信頼されているとランタイムが判断した場合のみ実行されます。

 インストールプロセスを開始するには、セットアッププログラムを実行する方法、配置マニフェストを開く方法、Microsoft Office アプリケーションホストを開く方法、または *VSTOInstaller.exe*を実行する方法の2つの方法があります。

 最初のセキュリティ チェックはドキュメント レベルのソリューションのみが対象となります。 ドキュメント レベルのソリューションのドキュメントは、信頼できる場所に置く必要があります。 ドキュメントがリモートネットワークファイル共有にある場合、または *.doc* または *.docm* ファイル名拡張子を持つ場合は、ドキュメントの場所を信頼できる場所の一覧に追加する必要があります。 詳細については、「 [ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)」を参照してください。

 ![VSTO セキュリティ - Microsoft Office からのインストール](../vsto/media/host-install.png "VSTO セキュリティ - Microsoft Office からのインストール")

 次に、[!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] と ClickOnce によって一連のセキュリティ チェックが実行されます。 これらのチェックに合格するためには、Office ソリューションが FullTrust アクセス許可を要求し、信頼されない発行元の一覧に含まれていない証明書で署名されていて、Internet Explorer の制限付きサイト ゾーン以外の場所にあることが必要です。 証明書が信頼された発行者の一覧に含まれている場合、ソリューションは直ちにインストールされます。 そうでない場合は、いずれかのチェックで不合格とならなければ、最後のチェックに進みます。

 ![ソリューションをインストールするための VSTO セキュリティ](../vsto/media/installing.png "ソリューションをインストールするための VSTO セキュリティ")

 信頼プロンプトが許可されていて、 [!INCLUDE[ndptecclick](../vsto/includes/ndptecclick-md.md)] ソリューションにまだ信頼が付与されていない場合、ランタイムはエンドユーザーが信頼の決定を行うことを許可します。 ユーザーがソリューションに信頼を付与すると、そのユーザーの信頼のリストにエントリが追加されます。 ユーザーの信頼のリストに追加されたソリューションは、完全に信頼されているため、インストールおよび実行が可能です。

 Visual Studio 2010 以降では、Windows インストーラー (MSI) を使用して Office ソリューションを Program Files ディレクトリにインストールすると、信頼のリストがバイパスされます。 詳細については、「 [信頼リストを使用した Office ソリューションの信頼](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)」を参照してください。

 ![VSTO セキュリティ - セットアップ プログラムを使用してインストール](../vsto/media/setup-vstoinstaller.png "VSTO セキュリティ - セットアップ プログラムを使用してインストール")

## <a name="see-also"></a>こちらもご覧ください

- [Office ソリューションへの信頼の付与](../vsto/granting-trust-to-office-solutions.md)
- [ドキュメントへの信頼の付与](../vsto/granting-trust-to-documents.md)
- [信頼リストを使用して Office ソリューションを信頼する](../vsto/trusting-office-solutions-by-using-inclusion-lists.md)
- [方法: 信頼のリストのセキュリティを構成する](../vsto/how-to-configure-inclusion-list-security.md)
- [方法: Office ソリューションに署名する](../vsto/how-to-sign-office-solutions.md)
- [Office ソリューションのセキュリティに関するトラブルシューティング](../vsto/troubleshooting-office-solution-security.md)
- [Office ソリューション用アプリケーションマニフェスト](../vsto/application-manifests-for-office-solutions.md)
- [Office ソリューションの配置マニフェスト](../vsto/deployment-manifests-for-office-solutions.md)
- [ClickOnce リファレンス](../deployment/clickonce-reference.md)
- [Office ソリューションの配置](../vsto/deploying-an-office-solution.md)
