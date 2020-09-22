---
title: 'チュートリアル: ClickOnce 配置 API を使用して必要に応じてアセンブリをダウンロードする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- assemblies, downloading [ClickOnce]
- ClickOnce deployment, on-demand download
- on-demand assemblies, ClickOnce
ms.assetid: d20e2789-8621-4806-b5b7-841122da1456
caps.latest.revision: 18
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: af03329a05501427f6d04d6cddbd637c3311b339
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841757"
---
# <a name="walkthrough-downloading-assemblies-on-demand-with-the-clickonce-deployment-api"></a>チュートリアル : ClickOnce 配置 API を使用して必要に応じてアセンブリをダウンロードする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

既定では、アプリケーションに含まれるすべてのアセンブリ [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] は、アプリケーションの初回実行時にダウンロードされます。 ただし、少数のユーザーによって使用されるアプリケーションの一部を使用することもできます。 その場合は、そのような型を作成するときにだけアセンブリをダウンロードすることができます。 以下のチュートリアルでは、アプリケーション内の特定のアセンブリに "オプション" マークを付ける方法、および共通言語ランタイム (CLR) でそのアセンブリが必要なときに <xref:System.Deployment.Application> 名前空間にあるクラスを使用してアセンブリをダウンロードする方法について説明します。  
  
> [!NOTE]
> これを行うには、アプリケーションが完全な信頼で実行する必要があります。  
  
## <a name="prerequisites"></a>前提条件  
 このチュートリアルを完了するには、次のコンポーネントのいずれかが必要です。  
  
- Windows SDK。 Windows SDK は、Microsoft ダウンロードセンターからダウンロードできます。  
  
- 見ることができます。  
  
## <a name="creating-the-projects"></a>プロジェクトの作成  
  
#### <a name="to-create-a-project-that-uses-an-on-demand-assembly"></a>オンデマンドアセンブリを使用するプロジェクトを作成するには  
  
1. Click、Ondemand という名前のディレクトリを作成します。  
  
2. Windows SDK コマンドプロンプトまたは [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] コマンドプロンプトを開きます。  
  
3. Clickondemand のディレクトリに移動します。  
  
4. 次のコマンドを使用して、公開キーと秘密キーのペアを生成します。  
  
    ```  
    sn -k TestKey.snk  
    ```  
  
5. メモ帳などのテキストエディターを使用して、という名前の1つのプロパティを持つという名前のクラスを定義し `DynamicClass` `Message` ます。  
  
     [!code-csharp[ClickOnceLibrary#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnceLibrary/CS/Class1.cs#1)]
     [!code-vb[ClickOnceLibrary#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceLibrary/VB/Class1.vb#1)]  
  
6. `ClickOnceLibrary.cs` `ClickOnceLibrary.vb` 使用する言語に応じて、テキストをまたはという名前のファイルとして保存します。  
  
7. ファイルをアセンブリにコンパイルします。  
  
    ```csharp  
    csc /target:library /keyfile:TestKey.snk ClickOnceLibrary.cs  
    ```  
  
    ```vb  
    vbc /target:library /keyfile:TestKey.snk ClickOnceLibrary.vb  
    ```  
  
8. アセンブリの公開キートークンを取得するには、次のコマンドを使用します。  
  
    ```  
    sn -T ClickOnceLibrary.dll  
    ```  
  
9. テキストエディターを使用して新しいファイルを作成し、次のコードを入力します。 このコードでは、必要に応じて Clicklibrary アセンブリをダウンロードする Windows フォームアプリケーションを作成します。  
  
     [!code-csharp[ClickOnceOnDemandCmdLine#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/CS/Form1.cs#1)]
     [!code-vb[ClickOnceOnDemandCmdLine#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceOnDemandCmdLine/VB/Form1.vb#1)]  
  
10. コードで、への呼び出しを見つけ <xref:System.Reflection.Assembly.LoadFile%2A> ます。  
  
11. は、前の手順で取得した `PublicKeyToken` 値に設定されます。  
  
12. またはのいずれかの形式でファイルを保存し `Form1.cs` `Form1.vb` ます。  
  
13. 次のコマンドを使用して、実行可能ファイルにコンパイルします。  
  
    ```csharp  
    csc /target:exe /reference:ClickOnceLibrary.dll Form1.cs  
    ```  
  
    ```vb  
    vbc /target:exe /reference:ClickOnceLibrary.dll Form1.vb  
    ```  
  
## <a name="marking-assemblies-as-optional"></a>アセンブリをオプションとしてマークする  
  
#### <a name="to-mark-assemblies-as-optional-in-your-clickonce-application-by-using-mageuiexe"></a>MageUI.exe を使用して ClickOnce アプリケーションでアセンブリをオプションとしてマークするには  
  
1. MageUI.exe を使用して、「 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」の説明に従って、アプリケーションマニフェストを作成します。 アプリケーションマニフェストには、次の設定を使用します。  
  
    - アプリケーションマニフェストに名前を指定 `ClickOnceOnDemand` します。  
  
    - [ **ファイル** ] ページの [ClickOnceLibrary.dll] 行で、[ **ファイルの種類** ] 列を **[なし**] に設定します。  
  
    - [ **ファイル** ] ページの [ClickOnceLibrary.dll] 行で、[ `ClickOnceLibrary.dll` **グループ]** 列に「」と入力します。  
  
2. MageUI.exe を使用して、「 [チュートリアル: ClickOnce アプリケーションを手動で配置する](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)」の説明に従って配置マニフェストを作成します。 配置マニフェストには、次の設定を使用します。  
  
    - 配置マニフェストに名前を指定 `ClickOnceOnDemand` します。  
  
## <a name="testing-the-new-assembly"></a>新しいアセンブリをテストする  
  
#### <a name="to-test-your-on-demand-assembly"></a>オンデマンド アセンブリをテストするには  
  
1. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]Web サーバーに配置をアップロードします。  
  
2. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]配置マニフェストの URL を入力して、Web ブラウザーからでデプロイされたアプリケーションを起動します。 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]アプリケーション `ClickOnceOnDemand` を呼び出し、adatum.com のルートディレクトリにアップロードすると、URL は次のようになります。  
  
    ```  
    http://www.adatum.com/ClickOnceOnDemand/ClickOnceOnDemand.application  
    ```  
  
3. メイン フォームが表示されたら、 <xref:System.Windows.Forms.Button>をクリックします。 メッセージ ボックス ウィンドウに "Hello, World!" という文字列が表示されます。  
  
## <a name="see-also"></a>関連項目  
 <xref:System.Deployment.Application.ApplicationDeployment>
