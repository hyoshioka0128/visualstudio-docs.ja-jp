---
title: ClickOnce アプリケーションのカスタムインストーラーを作成する
description: カスタムインストーラーを使用して、.exe ファイルに基づいて ClickOnce アプリケーションをサイレントインストールおよび更新する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, custom installer
- installer [ClickOnce], custom
- deploying applications [ClickOnce], custom installer
- InPlaceHostingManager [ClickOnce], custom installer
- custom installer [ClickOnce]
ms.assetid: fb222cc5-8aeb-4b94-8c49-b93e342f5f69
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 08b4adbaa7e7e25041f90628695de729aaff0d0d
ms.sourcegitcommit: 75bfdaab9a8b23a097c1e8538ed1cde404305974
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/07/2020
ms.locfileid: "94349205"
---
# <a name="walkthrough-create-a-custom-installer-for-a-clickonce-application"></a>チュートリアル: ClickOnce アプリケーションのカスタムインストーラーを作成する
*.Exe* ファイルに基づく ClickOnce アプリケーションは、カスタムインストーラーによってサイレントインストールおよび更新できます。 カスタムインストーラーは、インストール時にカスタムのユーザーエクスペリエンスを実装できます。たとえば、セキュリティおよびメンテナンス操作のためのカスタムダイアログボックスがあります。 インストール操作を実行するために、カスタムインストーラーはクラスを使用し <xref:System.Deployment.Application.InPlaceHostingManager> ます。 このチュートリアルでは、ClickOnce アプリケーションをサイレントインストールするカスタムインストーラーを作成する方法について説明します。

## <a name="prerequisites"></a>前提条件

### <a name="to-create-a-custom-clickonce-application-installer"></a>カスタム ClickOnce アプリケーションインストーラーを作成するには

1. ClickOnce アプリケーションで、system.servicemodel および system.string への参照を追加します。

2. アプリケーションに新しいクラスを追加し、任意の名前を指定します。 このチュートリアルでは、名前 `MyInstaller` を使用します。

3. 次の `Imports` ディレクティブまたは `using` ディレクティブを新しいクラスの先頭に追加します。

    ```vb
    Imports System.Deployment.Application
    Imports System.Windows.Forms
    ```

    ```csharp
    using System.Deployment.Application;
    using System.Windows.Forms;
    ```

4. 次のメソッドをクラスに追加します。

     これらのメソッドは、メソッドを呼び出して <xref:System.Deployment.Application.InPlaceHostingManager> 配置マニフェストをダウンロードし、適切なアクセス許可をアサートして、インストールのアクセス許可をユーザーに要求してから、アプリケーションを ClickOnce キャッシュにダウンロードしてインストールします。 カスタムインストーラーでは、ClickOnce アプリケーションが事前に信頼されていることを指定できます。また、メソッド呼び出しに対して信頼の決定を延期することもでき <xref:System.Deployment.Application.InPlaceHostingManager.AssertApplicationRequirements%2A> ます。 このコードは、アプリケーションを事前に信頼します。

    > [!NOTE]
    > 事前信頼によって割り当てられたアクセス許可は、カスタムインストーラーコードのアクセス許可を超えることはできません。

     [!code-vb[System.Deployment.Application.InPlaceHostingManager#1](../deployment/codesnippet/VisualBasic/walkthrough-creating-a-custom-installer-for-a-clickonce-application_1.vb)]
     [!code-csharp[System.Deployment.Application.InPlaceHostingManager#1](../deployment/codesnippet/CSharp/walkthrough-creating-a-custom-installer-for-a-clickonce-application_1.cs)]

5. コードからインストールを試みるには、メソッドを呼び出し `InstallApplication` ます。 たとえば、クラスにという名前を付けた場合は、 `MyInstaller` 次のようにを呼び出すことができ `InstallApplication` ます。

    ```vb
    Dim installer As New MyInstaller()
    installer.InstallApplication("\\myServer\myShare\myApp.application")
    MessageBox.Show("Installer object created.")
    ```

    ```csharp
    MyInstaller installer = new MyInstaller();
    installer.InstallApplication(@"\\myServer\myShare\myApp.application");
    MessageBox.Show("Installer object created.");
    ```

## <a name="next-steps"></a>次のステップ
 ClickOnce アプリケーションでは、更新プロセス中に表示するカスタムユーザーインターフェイスを含む、カスタムの更新ロジックを追加することもできます。 詳細については、「<xref:System.Deployment.Application.UpdateCheckInfo>」を参照してください。 ClickOnce アプリケーションでは、要素を使用して、[スタート] メニューの標準エントリ、ショートカット、および [プログラムの追加と削除] エントリを抑制することもでき `<customUX>` ます。 詳細については、「 [ \<entryPoint> 要素](../deployment/entrypoint-element-clickonce-application.md)」と「」を参照してください <xref:System.Deployment.Application.DownloadApplicationCompletedEventArgs.ShortcutAppId%2A> 。

## <a name="see-also"></a>関連項目
- [ClickOnce アプリケーションマニフェスト](../deployment/clickonce-application-manifest.md)
- [\<entryPoint> element](../deployment/entrypoint-element-clickonce-application.md)
