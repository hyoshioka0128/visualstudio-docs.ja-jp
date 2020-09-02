---
title: ClickOnce アプリケーションの保護 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows applications, ClickOnce security
- ClickOnce deployment, security
- deploying applications, ClickOnce security
ms.assetid: a05b5f2f-d1f2-471a-8096-8b11f7554265
caps.latest.revision: 47
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 2a2610c1fef92bb77d150dad7972bb991b6ef4a4
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686007"
---
# <a name="securing-clickonce-applications"></a>ClickOnce アプリケーションのセキュリティ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションは、保護されているリソースや操作に対して、コードが持つアクセス権を制限できるようにするための .NET Framework のコード アクセス セキュリティ制約を前提としています。 このため、コード アクセス セキュリティの影響を理解し、それに応じて [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを作成することが重要です。 アプリケーションでは、完全な信頼ゾーンまたは部分信頼ゾーン (インターネット ゾーンとイントラネット ゾーンなど) を使用して、アクセスを制限できます。  
  
 さらに、ClickOnce では、アプリケーションの発行元の信頼性を検証し、アプリケーションおよび配置マニフェストに署名してファイルが改ざんされていないことを証明するときに証明書を使用します。 署名を行うと、マニフェストの生成後にアプリケーション ファイルをより簡単に変更できるようになりますが、署名は省略可能な手順です。 ただし、署名付きマニフェストがないと、アプリケーション インストーラーが man-in-the-middle セキュリティ攻撃で改ざんされないようにすることが難しくなります。 したがって、アプリケーションをセキュリティで保護するために、アプリケーション マニフェストと配置マニフェストに署名することをお勧めします。  
  
## <a name="zones"></a>ゾーン  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] テクノロジを使用して配置されるアプリケーションは、セキュリティ ゾーンで定義されている一連のアクセス許可と操作に制限されます。 セキュリティ ゾーンは Internet Explorer で定義され、アプリケーションの場所に基づいています。 配置場所によって異なる既定のアクセス許可を次の表に示します。  
  
|デプロイの場所|セキュリティ ゾーン|  
|-------------------------|-------------------|  
|Web からの実行|インターネット ゾーン|  
|Web からのインストール|インターネット ゾーン|  
|ネットワーク ファイル共有からのインストール|ローカル イントラネット ゾーン|  
|CD-ROM からのインストール|Full Trust|  
  
 既定のアクセス許可は、アプリケーションの元のバージョンがどこから配置されたかによって異なります。このアプリケーションを更新する際、そのアクセス許可が継承されます。 アプリケーションが Web またはネットワーク上の場所からの更新プログラムをチェックするように構成されていて、新しいバージョンが使用できるようになっている場合には、元のインストールが完全信頼のアクセス許可ではなく、インターネット ゾーンまたはイントラネット ゾーンのアクセス許可を継承する可能性があります。 ユーザーに対する要求が行われないようにするために、システム管理者は、信頼された発行元として特定のアプリケーション発行元を定義する ClickOnce 配置ポリシーを指定できます。 このポリシーが配置されるコンピューター上では、アクセス許可は自動的に付与され、ユーザーへの要求は行われません。 詳細については、「 [信頼されたアプリケーションの配置の概要](../deployment/trusted-application-deployment-overview.md)」を参照してください。 信頼されたアプリケーションの配置を構成するには、コンピューター レベルまたはエンタープライズ レベルに証明書をインストールできます。 詳細については、「 [How to: Add a Trusted Publisher to a Client Computer for ClickOnce Applications](../deployment/how-to-add-a-trusted-publisher-to-a-client-computer-for-clickonce-applications.md)」を参照してください。  
  
## <a name="code-access-security-policies"></a>コード アクセス セキュリティ ポリシー  
 アプリケーションのアクセス許可は、アプリケーションマニフェストの[ \<trustInfo> 要素](../deployment/trustinfo-element-clickonce-application.md)要素の設定によって決まります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] は、プロジェクトの [ **セキュリティ** ] プロパティページの設定に基づいて、この情報を自動的に生成します。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションには、アプリケーションが要求するアクセス許可だけが与えられます。 たとえば、ファイルへのアクセスに完全信頼のアクセス許可が必要な場合、アプリケーションがファイルへのアクセス許可を要求すると、完全信頼ではなくファイルへのアクセス許可だけが与えられます。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを開発するときは、アプリケーションに必要な特定のアクセス許可のみを要求する必要があります。 ほとんどの場合は、インターネット ゾーンまたはローカル イントラネット ゾーンを使用して、アプリケーションを部分信頼に制限できます。 詳細については、「 [How to: Set a Security Zone for a ClickOnce Application](../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)」を参照してください。 アプリケーションにカスタムのアクセス許可が必要な場合、カスタム ゾーンを作成できます。 詳細については、「 [How to: Set Custom Permissions for a ClickOnce Application](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)」を参照してください。  
  
 アプリケーションの配置元ゾーンに与えられた既定のアクセス許可セットに含まれないアクセス許可を追加した場合、エンド ユーザーに対して、インストール時または更新時にアクセス許可の付与を求めるプロンプトが表示されます。 ユーザーに対する要求が行われないようにするために、システム管理者は、信頼された発行元として特定のアプリケーション発行元を定義する ClickOnce 配置ポリシーを指定できます。 このポリシーが配置されるコンピューター上では、アクセス許可は自動的に付与され、ユーザーへの要求は行われません。  
  
 開発者は、開発するアプリケーションが適切なアクセス許可で実行されることを確認する必要があります。 実行時にアプリケーションでゾーン以外のアクセス許可が必要な場合、セキュリティの例外が表示されることがあります。 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] によって、対象のセキュリティ ゾーンでアプリケーションをデバッグできます。 また、セキュリティで保護されたアプリケーションの開発に役立ちます。 詳細については、「 [How to: Debug a ClickOnce Application with Restricted Permissions](../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)」を参照してください。  
  
 コード アクセス セキュリティと ClickOnce の詳細については、「 [Code Access Security for ClickOnce Applications](../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。  
  
## <a name="code-signing-certificates"></a>証明書のコード署名  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] による配置を使用するアプリケーションを発行するには、アプリケーション マニフェストと配置マニフェストに公開キーと秘密キーのペアを使用して署名できます。 マニフェストに署名するツールは、 **プロジェクト デザイナー** の **[署名]** ページで使用できます。 詳細については、「 [Signing Page, Project Designer](../ide/reference/signing-page-project-designer.md)」を参照してください。 別の方法として、発行ウィザードを使用して、発行プロセスの最中にキー ファイルでマニフェストに署名することもできます。  
  
 マニフェストの署名後、Authenticode 署名に基づいた発行元情報は、インストール時に [アクセス許可] ダイアログ ボックスに表示され、アプリケーションが信頼された発行元から発行されていることをユーザーに示します。  
  
 ClickOnce と証明書の詳細については、「 [ClickOnce and Authenticode](../deployment/clickonce-and-authenticode.md)」を参照してください。  
  
## <a name="aspnet-form-based-authentication"></a>ASP.NET フォーム ベースの認証  
 各ユーザーがアクセスできる配置を制御する場合は、Web サーバーに配置される [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションに対する匿名アクセスを許可しないでください。 代わりに Windows 認証を使用して、インストールした配置に対するユーザーのアクセスをユーザーの ID に基づいて許可します。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] は永続的なクッキーを使用するため、ASP.NET フォーム ベースの認証はサポートしません。このクッキーは Internet Explorer のキャッシュに存在し、ハックされる可能性があるため、セキュリティ上のリスクがあります。 このため、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを配置する場合、Windows 認証以外の認証シナリオはサポートされません。  
  
## <a name="passing-arguments"></a>引数の受け渡し  
 引数を [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションに渡す必要がある場合、セキュリティ上の考慮事項が増えます。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] を使用すると、Web に配置されたアプリケーションにクエリ文字列を指定できます。 クエリ文字列は、アプリケーションを起動するための URL の末尾に一連の名前と値のペアが付加された形式になっています。  
  
 `http://servername.adatum.com/WindowsApp1.application?username=joeuser`  
  
 既定では、クエリ文字列の引数が無効になります。 これらを有効にするには、アプリケーションの配置マニフェストで `trustUrlParameters` 属性を設定する必要があります。 この値は、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] および MageUI.exe から設定できます。 クエリ文字列の受け渡しを有効にする方法の詳細な手順については、「 [方法: オンライン ClickOnce アプリケーションでクエリ文字列情報を取得](../deployment/how-to-retrieve-query-string-information-in-an-online-clickonce-application.md)する」を参照してください。  
  
 クエリ文字列を通じて取得された引数は、必ず安全であることを確認してからデータベースまたはコマンド ラインに渡してください。 安全でない引数とは、悪意のあるユーザーがアプリケーションを操作して任意のコマンドを実行できるようにするデータベースまたはコマンド ライン エスケープ文字が含まれた引数のことです。  
  
> [!NOTE]
> クエリ文字列引数は、起動時に [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションに引数を渡す唯一の手段です。 コマンド ラインから [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションに引数を渡すことはできません。  
  
## <a name="deploying-obfuscated-assemblies"></a>難読化されたアセンブリの配置  
 Dotfuscator を使用してアプリケーションを難読化し、他のユーザーがコードをリバース エンジニアリングできないようにできます。 ただし、アセンブリの難読化は Visual Studio IDE または ClickOnce 配置プロセスに統合されていません。 このため、難読化は、配置プロセスの外部でビルド後のステップなどを使用して実行する必要があります。 プロジェクトをビルドした後に、Visual Studio の外部で次の手順を手動で実行します。  
  
1. Dotfuscator を使用して難読化を実行します。  
  
2. Mage.exe または MageUI.exe を使用して、ClickOnce マニフェストを生成し、それらに署名します。 詳細については、次を参照してください。 [Mage.exe (マニフェスト生成および編集ツール)](https://msdn.microsoft.com/library/77dfe576-2962-407e-af13-82255df725a1)と[MageUI.exe (マニフェスト生成および編集ツールのグラフィカル クライアント)](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)します。  
  
3. 配置元の場所 (Web サーバー、UNC 共有、または CD-ROM) から手動でファイルを発行 (コピー) します。  
  
## <a name="see-also"></a>参照  
 [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)   
 [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)
