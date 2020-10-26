---
title: '方法: オンライン ClickOnce アプリケーションでクエリ文字列情報を取得する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, query strings
- query strings, retrieving information
ms.assetid: 48ce098a-a075-481b-a5f5-c8ba11f63120
caps.latest.revision: 21
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 588ff95f90c6d85526dfe931e8f0b8ab439d9b94
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65697583"
---
# <a name="how-to-retrieve-query-string-information-in-an-online-clickonce-application"></a>方法 : オンライン ClickOnce アプリケーションでクエリ文字列を取得する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

*クエリ文字列* とは、URL のうちの疑問符 (?) で始まる部分であり、 *name=value*の形式で任意の情報を記述します。 たとえば、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] でホストされている `WindowsApp1` という `servername`アプリケーションがあり、このアプリケーションを起動するときに、 `username` という変数に値を渡すとします。 URL は次のようになります。  
  
 `http://servername/WindowsApp1.application?username=joeuser`  
  
 以下の 2 つの手順では、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを使用してクエリ文字列の内容を取得する方法を説明します。  
  
> [!NOTE]
> クエリ文字列で情報を渡すことができるのは、ファイル共有やローカル ファイル システムではなく HTTP を使用してアプリケーションが起動しているときだけです。  
  
 まず、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションで短いコードを使用して、アプリケーションの起動時にクエリ文字列の値を読み取る方法について説明します。  
  
 次に、MageUI.exe を使用して、クエリ文字列パラメーターを受け入れることができるように [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを構成する方法について説明します。 これは、アプリケーションを発行するたびに実行する必要があります。  
  
> [!NOTE]
> この機能を有効にする前に、この後の「セキュリティ」を参照してください。  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]Mage.exe または MageUI.exe を使用した配置の作成方法については、「[チュートリアル: ClickOnce アプリケーションを手動で配置](../deployment/walkthrough-manually-deploying-a-clickonce-application.md)する」を参照してください。  
  
> [!NOTE]
> .NET Framework 3.5 SP1 以降では、オフラインの [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションにコマンド ライン引数を渡すことができます。 このアプリケーションに引数を提供する場合は、.APPREF-MS 拡張子を持つショートカット ファイルにパラメーターを渡すことができます。  
  
### <a name="to-obtain-query-string-information-from-a-clickonce-application"></a>ClickOnce アプリケーションでクエリ文字列を取得するには  
  
1. プロジェクト内に次のコードを記述します。 このコードが機能するためには、System.Web への参照を設定し、System.Web、System.Collections.Specialized、および System.Deployment.Application に対して `using` ステートメントまたは `Imports` ステートメントを追加する必要があります。  
  
     [!code-csharp[ClickOnceQueryString#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnceQueryString/CS/Form1.cs#1)]
     [!code-vb[ClickOnceQueryString#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnceQueryString/VB/Form1.vb#1)]  
  
2. 定義済みの関数を呼び出して、名前でインデックス化された、クエリ文字列パラメーターの <xref:System.Collections.DictionaryBase.Dictionary%2A> を取得します。  
  
### <a name="to-enable-query-string-passing-in-a-clickonce-application-with-mageuiexe"></a>MageUI.exe を使用して ClickOnce アプリケーションでクエリ文字列の受け渡しを有効にする方法  
  
1. .NET Framework のコマンド プロンプトを開き、次のように入力します。  
  
    ```  
    MageUI  
    ```  
  
2. **[ファイル]** メニューの **[開く]** をクリックし、対象の [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションの配置マニフェストを開きます。配置マニフェスト ファイルの拡張子は `.application` です。  
  
3. 左側のナビゲーション ウィンドウにある **[配置オプション]** パネルをクリックし、 **[URL パラメーターをアプリケーションに渡すことを許可する]** チェック ボックスをオンにします。  
  
4. **[ファイル]** メニューの **[保存]** をクリックします。  
  
> [!NOTE]
> または、 [!INCLUDE[vs_current_short](../includes/vs-current-short-md.md)]でクエリ文字列を渡すことができるようにすることもできます。 **[URL パラメーターをアプリケーションに渡すことを許可する]** チェック ボックスをオンにします。このチェック ボックスは、 **[プロジェクトのプロパティ]** を開いて **[発行]** タブをクリックし、 **[オプション]** ボタンをクリックして **[マニフェスト]** を選択すると表示されます。  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 クエリ文字列パラメーターを使用する場合は、アプリケーションがどのようにインストールされ、アクティブ化されるかを十分に考慮する必要があります。 アプリケーションが、Web またはネットワーク共有からユーザーのコンピューターにインストールされるように構成されている場合は、ユーザーが一度だけ URL を通じてアプリケーションをアクティブにすることが予想されます。 その後ユーザーは、ほとんどの場合、 **[スタート]** メニューのショートカットを使用してアプリケーションをアクティブにします。 その結果、アプリケーションはその有効期間中に一度だけクエリ文字列引数を受け取ることが保証されます。 これらの引数を後から使用できるようにユーザーのコンピューターに格納する場合は、それらが安全かつ確実に格納されるようにする必要があります。  
  
 アプリケーションがオンラインでのみ使用される場合は、常に URL を通じてそのアプリケーションがアクティブ化されます。 ただしその場合でも、クエリ文字列パラメーターが失われたり壊れたりしても正しく機能するようにアプリケーションを作成する必要があります。  
  
## <a name="net-framework-security"></a>.NET Framework のセキュリティ  
 悪意のある文字の入力を使用前に削除する予定である場合にのみ、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションに URL パラメーターを渡すことができるようにしてください。 たとえば、引用符、スラッシュ、またはセミコロンが埋め込まれた文字列を、フィルターしないままデータベースに対する SQL クエリに使用すると、任意のデータ操作が行われる可能性があります。 クエリ文字列のセキュリティの詳細については、「 [Script Exploits Overview](https://msdn.microsoft.com/library/772c7312-211a-4eb3-8d6e-eec0aa1dcc07)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションのセキュリティ保護](../deployment/securing-clickonce-applications.md)
