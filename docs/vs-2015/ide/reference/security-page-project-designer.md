---
title: '[セキュリティ] ページ (プロジェクト デザイナー) | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: reference
f1_keywords:
- vb.ProjectPropertiesSecurity
- vb.XBAPProjectPropertiesSecurity
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Project Designer, Security page
- Security page in Project Designer
ms.assetid: 641d9cd3-fa07-498a-8568-3c169bb4d3d5
caps.latest.revision: 40
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 768b0d43d8e6b52781e3f2dc2029e0b96b3a6548
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72665533"
---
# <a name="security-page-project-designer"></a>[セキュリティ] ページ (プロジェクト デザイナー)
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

**プロジェクト デザイナー**の **[セキュリティ]** ページを使用して、[!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)] 配置によって配置されたアプリケーションのコード アクセス セキュリティの設定を構成できます。 詳細については、「[ClickOnce アプリケーションのコード アクセス セキュリティ](../../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。

 この **[セキュリティ]** ページにアクセスするには、**ソリューション エクスプローラー**でプロジェクト ノードを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。 **プロジェクト デザイナー**が表示されたら、 **[セキュリティ]** タブをクリックします。

## <a name="security-settings"></a>セキュリティ設定
 **ClickOnce のセキュリティ設定を有効にする**デザイン時にセキュリティ設定を有効にするかどうかを指定します。 このオプションがオフの場合は、 **[セキュリティ]** ページの他のオプションもすべて無効になります。

> [!NOTE]
> **発行**ウィザードを使用してアプリケーションを発行するときは、このオプションが自動的に有効になります。

 このオプションをオンにすると、 **[これは完全に信頼するアプリケーションです]** と **[これは部分的に信頼するアプリケーションです]** の 2 つのオプション ボタンの一方を選択できるようになります。

 WPF Web ブラウザー アプリケーション プロジェクトでは、このオプションは既定でオンになります。

 それ以外のすべての種類のプロジェクトでは、このオプションは既定でオフになります。

 **これは完全に信頼するアプリケーションです**このオプションを選択した場合、アプリケーションは、クライアントコンピューターでインストールまたは実行されるときに完全信頼のアクセス許可を要求します。 ファイル システムやレジストリなどのリソースへの無制限のアクセス許可がアプリケーションに与えられるため、完全信頼の使用はできるだけ避けてください。

 WPF Web ブラウザー アプリケーション プロジェクトでは、このオプションは既定で部分信頼に設定されます。

 それ以外のすべての種類のプロジェクトでは、このオプションは既定で完全信頼に設定されます。

 **これは部分的に信頼するアプリケーションです**このオプションを選択した場合、アプリケーションは、クライアントコンピューターでのインストールまたは実行時に、部分信頼のアクセス許可を要求します。 *部分信頼*とは、要求したコード アクセス セキュリティ許可で許可されたアクションのみが実行されることを意味します。 セキュリティ アクセス許可の構成方法の詳細については、「[ClickOnce アプリケーションのコード アクセス セキュリティ](../../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。

 部分信頼セキュリティの設定は、 **[ClickOnce セキュリティのアクセス許可]** 領域のオプションを構成することで指定できます。

## <a name="clickonce-security-permissions"></a>ClickOnce セキュリティのアクセス許可
 **アプリケーションをインストールするゾーン**コードアクセスセキュリティのアクセス許可の既定のセットを指定します。 制限されたアクセス許可セットを使用するには **[インターネット]** または **[ローカル イントラネット]** を選択し、カスタムのアクセス許可セットを設定するには **[(カスタム)]** を選択します。 ゾーンで付与されているよりも多くのアクセス許可がアプリケーションで要求された場合、エンド ユーザーのアクセス許可を追加するために、ClickOnce 信頼プロンプトが表示されます。 セキュリティ アクセス許可の構成方法の詳細については、「[ClickOnce アプリケーションのコード アクセス セキュリティ](../../deployment/code-access-security-for-clickonce-applications.md)」を参照してください。

 WPF Web ブラウザー アプリケーション プロジェクトでは、このオプションは既定で **[インターネット]** に設定されます。

 **アクセス許可 XML の編集**アプリケーションマニフェストテンプレート (app.xaml) を開き、 **(カスタム)** アクセス許可セットのアクセス許可を構成します。

 **詳細設定**[[セキュリティの詳細設定] ダイアログボックス](../../ide/reference/advanced-security-settings-dialog-box.md)を開きます。このダイアログボックスは、アクセス許可が制限されたアプリケーションをデバッグするための設定を構成するために使用します。 これらの設定はデバッグ中にチェックされます。アクセス許可例外は、ゾーンで定義されているよりも多くのアクセス許可をアプリケーションが必要としている可能性があることを示します。

## <a name="see-also"></a>参照
 <xref:System.Security.Permissions.WebBrowserPermission> <xref:System.Security.Permissions.MediaPermission>
 [Clickonce アプリケーションのコードアクセスセキュリティ](../../deployment/code-access-security-for-clickonce-applications.md)[方法: Clickonce のセキュリティ設定を有効](../../deployment/how-to-enable-clickonce-security-settings.md)にする方法[: clickonce アプリケーションのセキュリティゾーンを設定](../../deployment/how-to-set-a-security-zone-for-a-clickonce-application.md)する方法: [Clickonce アプリケーションのカスタムアクセス許可を設定](../../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)する[方法:制限されたアクセス許可で ClickOnce アプリケーションをデバッグする clickonce の](../../deployment/how-to-debug-a-clickonce-application-with-restricted-permissions.md)[セキュリティと配置](../../deployment/clickonce-security-and-deployment.md)[プロジェクトのプロパティ参照](../../ide/reference/project-properties-reference.md)の[[セキュリティの詳細設定] ダイアログボックス](../../ide/reference/advanced-security-settings-dialog-box.md)
