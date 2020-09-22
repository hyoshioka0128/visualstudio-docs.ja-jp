---
title: Visual Studio SDK のインストール | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: visual-studio-sdk
ms.topic: conceptual
ms.assetid: c730edb6-5099-4c16-85a8-08def09f1455
caps.latest.revision: 4
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 88a6266a3f5910def0bf5041a37f89c2b3d67416
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842332"
---
# <a name="installing-the-visual-studio-sdk"></a>Visual Studio SDK のインストール
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio 2015 以降では、ダウンロードセンターから Visual Studio SDK をインストールしません。 これは、Visual Studio セットアップでオプション機能として含まれています。 VS SDK は、後でインストールすることもできます。  
  
## <a name="installing-the-visual-studio-sdk-as-part-of-a-visual-studio-installation"></a>Visual studio インストールの一部としての Visual Studio SDK のインストール  
 Visual Studio のインストールに VSSDK を含める場合は、カスタムインストールを行う必要があります。  
  
> [!NOTE]
> インストール実行可能ファイルでは、Visual Studio SDK が **Visual Studio Extensibility Tools**と呼ばれます。  
  
1. Visual Studio 2015 のインストールを開始します。 Express を除く任意のエディションの Visual Studio をインストールできます。  
  
2. 最初の画面で、[**既定**] ではなく [**カスタム**] を選択します。 **[次へ]** をクリックします。  
  
3. カスタム機能のツリービューが表示できます。 **共通ツール**を開きます。 **Visual Studio Extensibility Tools**が表示できます。  
  
     ![VSSDKInstall](../extensibility/media/vssdkinstall.png "VSSDKInstall")  
  
4. **Visual Studio Extensibility Tools**を確認し、[**次へ**] をクリックしてインストールを続行します。  
  
## <a name="installing-the-visual-studio-sdk-after-installing-visual-studio"></a>Visual Studio のインストール後に Visual Studio SDK をインストールする  
 Visual Studio のインストールが完了した後に Visual Studio SDK をインストールする場合は、次の手順に従う必要があります。  
  
1. [ **コントロールパネル]、[プログラム]、[プログラムと機能**] の順に開き、 **Visual Studio 2015**を探します。 Visual studio SDK は、Express を除くすべてのエディションの Visual Studio 2015 にインストールできます。  
  
2. [ **Visual Studio 2015**] を右クリックし、[ **変更**] をクリックします。 [インストール] ページが表示されます。  
  
3. 上記の **visual Studio インストールの一部として Visual STUDIO SDK をインストールする場合** と同じ手順に従います。  
  
4. [ **Visual Studio Extensibility Tools** ] リンクをクリックして、VISUAL Studio SDK をインストールします。  
  
## <a name="installing-the-visual-studio-sdk-from-a-solution"></a>ソリューションからの Visual Studio SDK のインストール  
 最初に VSSDK をインストールせずに、機能拡張プロジェクトでソリューションを開くと、ソリューションエクスプローラーの上に強調表示された情報バーが表示されます。 次のようになります。  
  
 ![SolutionExplorerInstall](../extensibility/media/solutionexplorerinstall.png "SolutionExplorerInstall")  
  
## <a name="installing-the-visual-studio-sdk-from-the-command-line"></a>コマンドラインからの Visual Studio SDK のインストール  
 Visual Studio インストーラーで **/InstallSelectableItems** スイッチを使用すると、コマンドラインから vssdk をインストールできます。 インストーラーでのコマンドラインパラメーターの使用の詳細については、「 [Visual Studio 2015 のインストール](../install/install-visual-studio-2015.md)」を参照してください。  
  
 Visual Studio 2015 コミュニティインストーラーを使用して、VSSDK をサイレントモードでインストールする方法を次に示します。  
  
```  
vs_community.exe /s /installSelectableItems VS_SDK_GROUPV1  
```  
  
 インストールされている Visual Studio のバージョンと一致する Visual Studio インストーラーを使用する必要があることにご注意ください。 たとえば、コンピューターに Visual Studio Enterprise がインストールされている場合は、Visual Studio Enterprise インストーラー (vs_enterprise.exe) を実行する必要があります。
