---
title: '方法: アクセス許可が制限された ClickOnce アプリケーションをデバッグする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], ClickOnce applications
- ClickOnce deployment, debugging
- ClickOnce applications, debugging
ms.assetid: 6991ea91-5253-451b-923d-22273a3d38b1
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: d60f88c4d1532a03922f12f21bb9b455ef5d84d8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153799"
---
# <a name="how-to-debug-a-clickonce-application-with-restricted-permissions"></a>方法 : アクセス許可が制限された ClickOnce アプリケーションをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

通常、開発用コンピューターは完全信頼アクセス許可で実行するので、ClickOnce アプリケーションのデバッグ時には、エンド ユーザーが制限されたアクセス許可でアプリケーションを実行したときと同じセキュリティ例外は発生しません。  
  
 これらの例外をキャッチするには、開発者はエンドユーザーと同じアクセス許可を使用してアプリケーションをデバッグする必要があります。 制限されたアクセス許可でのデバッグは、 **プロジェクト デザイナー** の **セキュリティ**ページで有効にすることができます。  
  
 さらに、Web サービスを呼び出すアプリケーションを開発するときは、通常、これらの Web サービスは開発用コンピューターに存在します。 配置後には、エンド ユーザーはこれらの Web サービスに異なる URL からアクセスします。 デバッグ中にエンド ユーザー エクスペリエンスをエミュレートするには、URL を指定すると、デバッガーはその URL から呼び出されているかのように Web サービスを扱います。  
  
### <a name="to-enable-debugging-with-restricted-permissions"></a>制限されたアクセス許可でのデバッグを有効にするには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **プロジェクト デザイナー**で、 **[セキュリティ]** タブをクリックします。  
  
3. **[ClickOnce セキュリティ設定を有効にする]** チェック ボックスをオンにし、 **[これは部分的に信頼するアプリケーションです]** オプション ボタンをクリックします。  
  
4. **[詳細設定]** をクリックします。  
  
5. **[選択されたアクセス許可セットでこのアプリケーションをデバッグする]** チェック ボックスをオンにし、 **[OK]** をクリックします。  
  
     アプリケーションのデバッグ時に、アクセス許可セットに含まれないアクセス許可にアクセスしようとすると、セキュリティ例外が発生します。  
  
### <a name="to-specify-a-url-for-debugging"></a>デバッグ用の URL を指定するには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **プロジェクト デザイナー**で、 **[セキュリティ]** タブをクリックします。  
  
3. **[ClickOnce セキュリティ設定を有効にする]** チェック ボックスをオンにし、 **[これは部分的に信頼するアプリケーションです]** オプション ボタンをクリックします。  
  
4. **[詳細設定]** をクリックします。  
  
5. **[選択されたアクセス許可セットでこのアプリケーションをデバッグする]** チェック ボックスをオンにし、 **[OK]** をクリックします。  
  
6. **[このアプリケーションが次の URL からダウンロードされたと仮定してデバッグする]** テキスト ボックスに、URL またはネットワーク パスを入力します。  
  
## <a name="see-also"></a>参照  
 [方法: ClickOnce アプリケーションのカスタムアクセス許可を設定する](../deployment/how-to-set-custom-permissions-for-a-clickonce-application.md)   
 [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)   
 [ClickOnce アプリケーションのコードアクセスセキュリティ](../deployment/code-access-security-for-clickonce-applications.md)   
 [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
