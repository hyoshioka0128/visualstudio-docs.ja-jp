---
title: '[サービスの詳細設定] ダイアログ ボックス'
description: '[サービスの詳細設定] 機能を使用して、クライアント アプリケーション サービスの詳細設定を構成する方法について説明します。'
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesAdvancedServices
helpviewer_keywords:
- Advanced Settings for Services dialog box
ms.assetid: 6dde4a2d-85e1-4275-aa55-24b84111be91
author: TerryGLee
ms.author: tglee
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 59ad28dd6890effbac00282a0e9bc388b4191139
ms.sourcegitcommit: 935e4d9a20928b733e573b6801a6eaff0d0b1b14
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/25/2020
ms.locfileid: "95871315"
---
# <a name="advanced-settings-for-services-dialog-box"></a>[サービスの詳細設定] ダイアログ ボックス
クライアント アプリケーション サービスにより、Windows フォーム アプリケーションおよび Windows Presentation Foundation (WPF) アプリケーションから [!INCLUDE[ajax_current_short](../../ide/reference/includes/ajax_current_short_md.md)] ログイン サービス、ロール サービス、プロファイル サービスに簡単にアクセスできます。 **プロジェクト デザイナー** の **[サービス]** ページを使用して、クライアント アプリケーション サービスを構成することができます。 **[サービス]** ページの詳細については、「[Services Page, Project Designer](../../ide/reference/services-page-project-designer.md)」([サービス] ページ (プロジェクト デザイナー)) を参照してください。

**プロジェクト デザイナー** の **[サービスの詳細設定]** ダイアログ ボックスの **[サービス]** ページを使用して、クライアント アプリケーション サービスの詳細設定を構成します。 これらの設定を使用すると、既定のアプリケーション サービスの動作の一部をオーバーライドして、あまり一般的ではないシナリオに対応することができます。 詳細については、「[クライアント アプリケーション サービス](/dotnet/framework/common-client-technologies/client-application-services)」を参照してください。

**[サービスの詳細設定]** ダイアログ ボックスにアクセスするには、**ソリューション エクスプローラー** でプロジェクト ノードを選択し、**[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **プロジェクト デザイナー** が表示されたら、**[サービス]** タブをクリックし、**[詳細設定]** ボタンをクリックします。 クライアント アプリケーション サービスを有効にするまで、このボタンは無効です。

## <a name="task-list"></a>タスク一覧

- [方法 : クライアント アプリケーション サービスを構成する](/dotnet/framework/common-client-technologies/how-to-configure-client-application-services)

## <a name="uielement-list"></a>UIElement の一覧

 **オフラインでログインできるようにパスワードのハッシュをローカルに保存する** 暗号化された形式のユーザー パスワードをローカルにキャッシュして、アプリケーションがオフライン モードのときでもユーザーがログインできるようにするかどうかを指定します。 既定では、このオプションはオンになっています。

 **サーバー クッキーの期限が切れた場合は常に再度ログオンすることをユーザーに要求する** アプリケーションがロールまたはプロファイル サービスにアクセスし、サーバー認証の Cookie が期限切れになっているときに、以前に認証済みのユーザーを自動的に再認証するかどうかを指定します。 Cookie の期限切れ後はアプリケーション サービスへのアクセスを拒否し、明示的に再認証を必須にするには、このオプションをオンにします。 このオプションは、公共の場所に配置されたアプリケーションで、使用後にアプリケーションを実行中のままにしているユーザーが無期限に認証されないようにするのに便利です。 既定では、このオプションはオフになっています。

 **ロール サービスのキャッシュのタイムアウト** クライアント ロール プロバイダーが、ロール サービスにアクセスせずにキャッシュ済みのロール値を使用する時間を指定します。 この時間間隔は、ロールが頻繁に更新される場合は小さい値に設定し、ロールが頻繁に更新されない場合はより大きい値に設定します。 既定値は 1 日です。

<xref:System.Web.Security.RolePrincipal.IsInRole%2A> メソッドを呼び出すと、ロール プロバイダーがキャッシュされたロール値またはロール サービスにアクセスします。 プログラムによってキャッシュを消去し、強制的にこのメソッドがリモート サービスにアクセスするようにするには、<xref:System.Web.ClientServices.Providers.ClientRoleProvider.ResetCache%2A> メソッドを呼び出します。

 **カスタム接続文字列を使用** クライアント サービス プロバイダーがローカル キャッシュにカスタムのデータ ストアを使用するかどうかを指定します。 既定では、サービス プロバイダーはキャッシュのローカル ファイル システムを使用します。 このオプションをオンにすると、テキスト ボックスには既定の接続文字列が自動的に入力されます。 自動生成される既定の接続文字列のままにして、SQL Server Compact Edition データベースを使用するか、既存の SQL Server データベースに対する接続文字列を指定することができます。 詳細については、「 [How to: Configure Client Application Services](/dotnet/framework/common-client-technologies/how-to-configure-client-application-services)」を参照してください。 既定では、このオプションはオフになっています。

## <a name="see-also"></a>関連項目

- [クライアント アプリケーション サービス](/dotnet/framework/common-client-technologies/client-application-services)
- [[サービス] ページ (プロジェクト デザイナー)](../../ide/reference/services-page-project-designer.md)
- [方法 : クライアント アプリケーション サービスを構成する](/dotnet/framework/common-client-technologies/how-to-configure-client-application-services)
