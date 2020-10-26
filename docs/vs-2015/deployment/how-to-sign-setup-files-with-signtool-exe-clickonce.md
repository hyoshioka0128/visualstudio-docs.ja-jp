---
title: '方法: SignTool.exe を使用してセットアップファイルに署名する (ClickOnce) |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce applications, signtool.exe
- deploying applications [ClickOnce], re-signing setup.exe
- ClickOnce deployment, signtool.exe
- ClickOnce applications, re-signing setup.exe
- ClickOnce deployment, re-signing setup.exe
ms.assetid: 545a4005-d283-4110-9821-c78a9833c250
caps.latest.revision: 10
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 67dc8e858a8ee87ee9e1fef9d99bf24ea4994960
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68202181"
---
# <a name="how-to-sign-setup-files-with-signtoolexe-clickonce"></a>方法: SignTool.exe を使用してセットアップ ファイルに署名する (ClickOnce)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

SignTool.exe を使用して、セットアップ プログラム (setup.exe) に署名できます。 このプロセスによって、改ざんされたファイルがエンド ユーザーのコンピューターにインストールされないようにすることができます。  
  
 既定で、ClickOnce には複数の署名されたマニフェストと、1 つの署名されたセットアップ プログラムがあります。 ただし、後でセットアップ プログラムのパラメーターを変更する場合、セットアップ プログラムに後で署名する必要があります。 セットアップ プログラムの署名後にパラメーターを変更すると、署名が破損します。  
  
 次の手順では、未署名のマニフェストと未署名のセットアップ プログラムを生成します。 次に、ClickOnce の署名を Visual Studio で有効にし、署名されたマニフェストを生成します。 セットアップ プログラムは未署名のままなので、ユーザーは自分の証明書を使用して実行可能ファイルに署名できます。  
  
### <a name="to-generate-an-unsigned-setup-program-and-sign-later"></a>未署名のセットアップ プログラムを生成し、後で署名するには  
  
1. マニフェストに署名する証明書を開発用コンピューターにインストールします。  
  
2. **ソリューションエクスプローラー**でプロジェクトを選択します。  
  
3. **[プロジェクト]** メニューの *ProjectName の * **[プロパティ]** をクリックします。  
  
4. **[署名]** ページの **[ClickOnce マニフェストに署名する]** をオフにします。  
  
5. **[発行]** ページで、**[必須コンポーネント]** をクリックします。  
  
6. すべての必須コンポーネントが選択されていることを確認し、**[OK]** をクリックします。  
  
7. **[発行]** ページで発行設定を確認して、**[今すぐ発行]** をクリックします。  
  
     ソリューションは、未署名のアプリケーション マニフェスト、未署名の配置マニフェスト、バージョン固有のファイル、および未署名のセットアップ プログラムを発行フォルダーに発行します。  
  
8. **[発行]** ページで、**[必須コンポーネント]** をクリックします。  
  
9. **[必須コンポーネント]** ダイアログ ボックスで、**[必須コンポーネントをインストールするセットアップ プログラムを作成する]** をオフにします。  
  
10. **[発行]** ページで発行設定を確認して、**[今すぐ発行]** をクリックします。  
  
     ソリューションは、署名済みのアプリケーション マニフェスト、署名済みの配置マニフェスト、およびバージョン固有のファイルを発行フォルダーに発行します。 未署名のセットアップ プログラムは発行プロセスで上書きされません。  
  
11. 顧客側でコマンド プロンプトを開きます。  
  
12. .exe ファイルを含むディレクトリに移動します。  
  
13. 次のコマンドで .exe ファイルに署名します。  
  
    ```  
    signtool sign /sha1 CertificateHash Setup.exe  
    signtool sign /f CertFileName Setup.exe  
    ```  
  
     たとえば、セットアップ プログラムに署名するには、次のコマンドのいずれかを使用します。  
  
    ```  
    signtool sign /sha1 CCB... Setup.exe  
    signtool sign /f CertFileName Setup.exe  
    ```  
  
## <a name="see-also"></a>参照  
 [方法: アプリケーションマニフェストおよび配置マニフェストに再署名する](../deployment/how-to-re-sign-application-and-deployment-manifests.md)
