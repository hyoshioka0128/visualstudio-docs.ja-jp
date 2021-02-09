---
title: セキュリティ/バージョン管理/マニフェストに関する問題 (ClickOnce)
description: Clickonce のセキュリティ、アプリケーションのバージョン管理、およびマニフェストの構文とセマンティクスに関する問題について説明します。これにより、ClickOnce 配置が成功しなくなる可能性があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- versioning, ClickOnce applications
- ClickOnce applications, Windows Vista User Account Control
- ClickOnce applications, versioning issues
- security, ClickOnce applications
- Windows 7, ClickOnce deployments
- ClickOnce applications, manifest issues
- User Account Control, ClickOnce applications
- Windows Vista, ClickOnce deployments
- manifests [ClickOnce]
- ClickOnce applications, security issues
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 55758f67c845cbf753d51ebfb94b87af6cf55cde
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99877630"
---
# <a name="security-versioning-and-manifest-issues-in-clickonce-deployments"></a>ClickOnce 配置でのセキュリティ、バージョン管理、およびマニフェストの問題

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]セキュリティ、アプリケーションのバージョン管理、マニフェストの構文とセマンティクスにはさまざまな問題があり、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] デプロイが成功しない可能性があります。

## <a name="clickonce-and-windows-vista-user-account-control"></a>ClickOnce と Windows Vista のユーザーアカウント制御

では [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] 、現在のユーザーが管理者のアクセス許可を持つアカウントでログインしている場合でも、既定では、アプリケーションは標準ユーザーとして実行されます。 アプリケーションで管理者のアクセス許可が必要なアクションを実行する必要がある場合は、オペレーティングシステムに対して、ユーザーに管理者の資格情報の入力を求めるメッセージが表示されます。 この機能は、ユーザーアカウント制御 (UAC) という名前であり、ユーザーが明示的に承認することなく、オペレーティングシステム全体に影響を与える可能性がある変更をアプリケーションが行うことを防止します。 Windows アプリケーションは、 `requestedExecutionLevel` アプリケーションマニフェストのセクションで属性を指定することによって、このアクセス許可の昇格が必要であることを宣言し `trustInfo` ます。

アプリケーションがセキュリティ昇格攻撃にさらされるリスクのため、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] UAC がクライアントに対して有効になっている場合、アプリケーションはアクセス許可の昇格を要求できません。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]属性をまたはに設定しようとするアプリケーションは、 `requestedExecutionLevel` にインストールされ `requireAdministrator` `highestAvailable` ません [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] 。

場合によっては、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] のインストーラー検出ロジックにより、管理者権限でアプリケーションを実行しようとすることがあり [!INCLUDE[windowsver](../deployment/includes/windowsver_md.md)] ます。 この場合、 `requestedExecutionLevel` アプリケーションマニフェストの属性をに設定でき `asInvoker` ます。 これにより、アプリケーション自体が昇格せずに実行されます。 [!INCLUDE[vs_orcas_long](../debugger/includes/vs_orcas_long_md.md)] は、この属性をすべてのアプリケーションマニフェストに自動的に追加します。

アプリケーションの有効期間全体に対する管理者権限を必要とするアプリケーションを開発している場合は、代わりに Windows インストーラー (MSI) テクノロジを使用してアプリケーションを展開することを検討してください。 詳細については、「 [Windows インストーラーの基礎](../extensibility/internals/windows-installer-basics.md)」を参照してください。

## <a name="online-application-quotas-and-partial-trust-applications"></a>オンラインアプリケーションクォータと部分信頼アプリケーション

アプリケーションがインストールではなくオンラインで実行されている場合は、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] オンラインアプリケーション用に確保されているクォータに収まる必要があります。 また、部分信頼で実行されるネットワークアプリケーション (セキュリティアクセス許可の制限付きセットなど) は、クォータサイズの半分よりも大きくすることはできません。

オンラインアプリケーションクォータを変更する方法の詳細と手順については、「 [ClickOnce キャッシュの概要](../deployment/clickonce-cache-overview.md)」を参照してください。

## <a name="versioning-issues"></a>バージョン管理に関する問題

アセンブリに厳密な名前を割り当て、アプリケーションの更新を反映するようにアセンブリのバージョン番号を増やすと、問題が発生することがあります。 厳密な名前のアセンブリへの参照を使用してコンパイルされたアセンブリ自体を再コンパイルする必要があります。それ以外の場合、アセンブリは古いバージョンを参照しようとします。 アセンブリは、そのバインド要求で古いバージョンの値を使用しているため、この操作を試みます。

たとえば、独自のプロジェクトにバージョン1.0.0.0 の厳密な名前付きアセンブリがあるとします。 アセンブリをコンパイルした後、メインアプリケーションを含むプロジェクトへの参照として追加します。 アセンブリを更新し、そのバージョンを1.0.0.1 にインクリメントして、アプリケーションを再コンパイルせずに展開しようとすると、アプリケーションは実行時にアセンブリを読み込むことができなくなります。

このエラーは、マニフェストを手動で編集している場合にのみ発生します [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 Visual Studio を使用して配置を生成した場合、このエラーは発生しません。

## <a name="specify-individual-net-framework-assemblies-in-the-manifest"></a>マニフェスト内の個々の .NET Framework アセンブリを指定する

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]以前のバージョンの .NET Framework アセンブリを参照するように配置を手動で編集した場合、アプリケーションの読み込みは失敗します。 たとえば、マニフェストに指定されているバージョンより前のバージョンの .NET Framework の System.Net アセンブリへの参照を追加した場合、エラーが発生します。 一般に、アプリケーションの実行対象となる .NET Framework のバージョンがアプリケーションマニフェストの依存関係として指定されているため、個々の .NET Framework アセンブリへの参照を指定することは避けてください。

## <a name="manifest-parsing-issues"></a>マニフェスト解析の問題

によって使用されるマニフェストファイル [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] は xml ファイルであり、適切な形式で有効である必要があります。 xml 構文規則に従う必要があり、関連する xml スキーマで定義されている要素と属性のみを使用する必要があります。

マニフェストファイルで問題が発生する原因としては、単一引用符や二重引用符などの特殊文字を含むアプリケーションの名前を選択することが挙げられます。 アプリケーションの名前は id の一部です [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 。 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] では、特殊文字を含む id は現在解析されません。 アプリケーションのアクティブ化に失敗した場合は、名前にアルファベットと数字のみを使用していることを確認し、もう一度展開してみてください。

配置マニフェストまたはアプリケーションマニフェストを手動で編集した場合は、意図せず破損している可能性があります。 マニフェストが破損していると、正しいインストールができなくなり [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] ます。 実行時にこのようなエラーをデバッグするには、[ **ClickOnce エラー** ] ダイアログボックスの [**詳細**] をクリックし、ログのエラーメッセージを参照します。 ログには、次のいずれかのメッセージが表示されます。

- 構文エラーの説明、およびエラーが発生した行番号と文字位置。

- マニフェストのスキーマの違反に使用される要素または属性の名前。 マニフェストに手動で XML を追加した場合は、追加したマニフェストをマニフェストスキーマと比較する必要があります。 詳細については、「 [clickonce 配置マニフェスト](../deployment/clickonce-deployment-manifest.md) 」と「 [clickonce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)」を参照してください。

- ID が競合しています。 配置マニフェストとアプリケーションマニフェストの依存関係の参照は、属性と属性の両方で一意である必要があり `name` `publicKeyToken` ます。 両方の属性がマニフェスト内の2つの要素間で一致する場合、マニフェストの解析は成功しません。

## <a name="precautions-when-manually-changing-manifests-or-applications"></a>手動でマニフェストまたはアプリケーションを変更する際の注意事項

アプリケーションマニフェストを更新するときは、アプリケーションマニフェストと配置マニフェストの両方に再署名する必要があります。 配置マニフェストには、そのファイルのハッシュとそのデジタル署名を含むアプリケーションマニフェストへの参照が含まれています。

### <a name="precautions-with-deployment-provider-usage"></a>配置プロバイダーの使用に関する注意事項

[!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)]配置マニフェストには、 `deploymentProvider` アプリケーションをインストールしてサービスを実行する場所の完全パスを指すプロパティがあります。

```xml
<deploymentProvider codebase="http://myserver/myapp.application" />
```

このパスは、がアプリケーションを作成するときに設定され [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 、インストールされているアプリケーションでは必須です。 このパスは、インストーラーによってアプリケーションがインストールされる標準の場所を指し、 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] 更新プログラムを検索します。 **Xcopy** コマンドを使用してアプリケーションを別の場所にコピーしても、プロパティを変更していない場合 [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] `deploymentProvider` で [!INCLUDE[ndptecclick](../deployment/includes/ndptecclick_md.md)] も、はアプリケーションをダウンロードしようとしたときに元の場所を参照します。

アプリケーションを移動またはコピーする場合は、 `deploymentProvider` クライアントが実際に新しい場所からインストールされるように、パスも更新する必要があります。 アプリケーションがインストールされている場合は、このパスを更新することはほとんど問題になります。 常に元の URL を使用して起動されるオンラインアプリケーションの場合、の設定 `deploymentProvider` は省略可能です。 が設定されている場合は受け入れられます。それ以外の場合は、アプリケーションを起動するために使用される URL が、 `deploymentProvider` アプリケーションファイルをダウンロードするためのベース url として使用されます。

> [!NOTE]
> マニフェストを更新するたびに、再度署名する必要もあります。

## <a name="see-also"></a>関連項目

[ClickOnce 配置](../deployment/troubleshooting-clickonce-deployments.md) 
 のトラブルシューティング[ClickOnce アプリケーション](../deployment/securing-clickonce-applications.md) 
 のセキュリティ保護[ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)
