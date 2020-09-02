---
title: '方法: ClickOnce アプリケーションのカスタムアクセス許可を設定する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, permissions
- permissions, ClickOnce applications
ms.assetid: 660459ca-ef73-44a8-b323-610001f63b93
caps.latest.revision: 19
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 6739f38e91ce998441c4cfa62453d485a5d370e3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697548"
---
# <a name="how-to-set-custom-permissions-for-a-clickonce-application"></a>方法 : ClickOnce アプリケーションのカスタム アクセス許可を設定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

インターネット ゾーンまたはローカル イントラネット ゾーンの既定のアクセス許可を使用する [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを配置できます。 または、アプリケーションに必要な特定のアクセス許可用にカスタム ゾーンを作成することもできます。 そのためには、 **プロジェクト デザイナー** の **[セキュリティ]** ページでセキュリティのアクセス許可をカスタマイズします。  
  
### <a name="to-customize-a-permission"></a>アクセス許可をカスタマイズするには  
  
1. **ソリューション エクスプローラー**でプロジェクトを選択し、 **[プロジェクト]** メニューの **[プロパティ]** をクリックします。  
  
2. **[セキュリティ]** タブをクリックします。  
  
3. **[ClickOnce セキュリティ設定を有効にする]** チェック ボックスをオンにします。  
  
4. **[これは部分的に信頼するアプリケーションです]** オプション ボタンを選択します。  
  
     **[ClickOnce セキュリティのアクセス許可]** セクション内のコントロールが有効になります。  
  
5. **[アプリケーションのインストール元のゾーン]** ドロップダウン リストの **[(カスタム)]** を選択します。  
  
6. **[アクセス許可 XML の編集]** をクリックします。  
  
     XML エディターで app.manifest ファイルが開きます。  
  
7. `</applicationRequestMinimum>` 要素の前に、アプリケーションに必要なアクセス許可の XML コードを追加します。  
  
    > [!NOTE]
    > アクセス許可セットの `ToXml` メソッドを使用して、アプリケーション マニフェスト用の XML コードを生成できます。 たとえば、 <xref:System.Security.Permissions.EnvironmentPermission> アクセス許可セットの XML を生成するには、 <xref:System.Security.Permissions.EnvironmentPermission.ToXml%2A> メソッドを呼び出します。 アクセス許可セット XML の構造の詳細については、「 [NIB: 方法: XML ファイルを使用してアクセス許可セットをインポートする](https://msdn.microsoft.com/dea16b54-c108-408a-ac36-cdc05f746236)」をご覧ください。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)   
 [ClickOnce アプリケーションのコードアクセスセキュリティ](../deployment/code-access-security-for-clickonce-applications.md)   
 [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
