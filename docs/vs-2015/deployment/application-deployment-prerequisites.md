---
title: アプリケーション配置の前提条件 |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, platform detection
- ClickOnce deployment, prerequisites
- ClickOnce deployment, dependencies
- prerequisites, ClickOnce
- dependencies, ClickOnce
ms.assetid: fc6e047e-ad94-44e8-8ff5-b6d1f4ca7735
caps.latest.revision: 53
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 4945efddb91142ce04f5b117129428ec4a054fc3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842104"
---
# <a name="application-deployment-prerequisites"></a>アプリケーション配置の必要条件
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

アプリケーションが正常にインストールされ、実行されるようにするには、アプリケーションが依存しているすべてのコンポーネントがターゲット コンピューターに既にインストールされていることを最初に確認する必要があります。 たとえば、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用して作成されたほとんどのアプリケーションは、[!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] に依存します。アプリケーションをインストールする前に、共通言語ランタイムの適切なバージョンが、ターゲット コンピューター上に存在している必要があります。  
  
 [ **必須コンポーネント] ダイアログボックス** でこれらの必須コンポーネントを選択し、インストールの一部として .NET Framework およびその他の再頒布可能パッケージをインストールします。 この方法は*ブートストラップ*と呼ばれます。 次に、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] Setup.exe という名前の Windows 実行可能プログラムを生成します。これは *ブートストラップ*とも呼ばれます。 ブートストラップは、アプリケーションが実行される前にこれらの必須コンポーネントをインストールします。 これらの前提条件の選択の詳細については、「[ [必須コンポーネント] ダイアログボックス](../ide/reference/prerequisites-dialog-box.md)」を参照してください。  
  
 各必須コンポーネントはブートストラップ パッケージです。 ブートストラップ パッケージは、必須コンポーネントのインストール方法を記述するマニフェスト ファイルを含むディレクトリおよびファイルのグループです。 アプリケーションの必須コンポーネントが **[必須コンポーネント]** ダイアログ ボックスに表示されない場合は、カスタム ブートストラップ パッケージを作成して Visual Studio に追加できます。 それにより、**[必須コンポーネント]** ダイアログ ボックスで必須コンポーネントを選択できるようになります。 詳細については、「 [ブートストラップパッケージの作成](../deployment/creating-bootstrapper-packages.md)」を参照してください。  
  
 既定では、ブートストラップは ClickOnce の配置で有効です。 ClickOnce の配置に生成されるブートストラップは署名付きです。 ブートストラップは任意のコンポーネントに対して無効にできますが、これは、該当するコンポーネントの正しいバージョンが既にすべてのターゲット コンピューターにインストールされていることを確認した場合のみに限定してください。  
  
## <a name="bootstrapping-and-clickonce-deployment"></a>ブートストラップと ClickOnce 配置  
 アプリケーションをクライアント コンピューターにインストールする前に、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] はクライアントを検査して、アプリケーション マニフェストに一定の必要条件が指定されているかどうかを確認します。 これらには、次のものが含まれます。  
  
- 最低限必要な共通言語ランタイムのバージョン。これはアプリケーション マニフェストにアセンブリ依存関係として指定されます。  
  
- アプリケーションに最低限必要な Windows オペレーティング システムのバージョン。これは、アプリケーション マニフェストに `<osVersionInfo>` 要素を使用して指定されます。 (「 [ \<dependency> 要素](../deployment/dependency-element-clickonce-application.md)」を参照)  
  
- グローバル アセンブリ キャッシュ (GAC) にプレインストールされる必要があるすべてのアセンブリの最小バージョン。これは、アセンブリ マニフェストでアセンブリ依存関係の宣言によって指定されます。  
  
  [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 不足している前提条件を検出し、ブートストラップを使用して必須コンポーネントをインストールすることができます。 詳細については、「 [方法: ClickOnce アプリケーションを使用して必須コンポーネントをインストール](../deployment/how-to-install-prerequisites-with-a-clickonce-application.md)する」を参照してください。  
  
> [!NOTE]
> [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] や MageUI.exe などのツールによって生成されたマニフェスト内の値を変更するには、アプリケーション マニフェストをテキスト エディターで編集した後に、アプリケーション マニフェストと配置マニフェストの両方に再署名する必要があります。 詳細については、「 [How to: Re-sign Application and Deployment Manifests](../deployment/how-to-re-sign-application-and-deployment-manifests.md)」を参照してください。  
  
 Visual Studio と ClickOnce を使用してアプリケーションを配置する場合、既定で選択されるブートストラップ パッケージは、ソリューション内の .NET Framework のバージョンによって異なります。 ただし、対象の .NET Framework のバージョンを変更する場合は、**[必須コンポーネント]** ダイアログ ボックスのオプションを手動で更新する必要があります。  
  
|対象の .NET Framework|選択されるブートストラップ パッケージ|  
|---------------------------|------------------------------------|  
|.NET Framework 4 Client Profile|.NET Framework 4 Client Profile<br /><br /> Windows インストーラー 3.1|  
|.NET Framework 4|.NET Framework 4<br /><br /> Windows インストーラー 3.1|  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 配置では、[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] 発行ウィザードで作成された Publish.htm ページが、アプリケーションのみをインストールするリンクまたはアプリケーションとブートストラップ コンポーネントの両方をインストールするリンクのいずれかを指します。  
  
 ClickOnce 発行ウィザードまたは Visual Studio の [発行] ページを使用してブートストラップを生成する場合、Setup.exe は自動的に署名されます。 ただし、顧客の証明書を使用してブートストラップに署名する場合は、後でファイルに署名できます。  
  
## <a name="bootstrapping-and-msbuild"></a>ブートストラップと MSBuild  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] を使用せず、アプリケーションをコマンド ラインでコンパイルする場合は、Microsoft Build Engine (MSBuild) タスクを使用して [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ブートストラップ アプリケーションを作成できます。 詳細については、「 [Generatebootstrapper タスク](../msbuild/generatebootstrapper-task.md)」を参照してください。  
  
 ブートストラップの代わりに、Microsoft SMS (Systems Management Server) などの電子ソフトウェア配布システムを使用して、コンポーネントを事前に配置することもできます。  
  
## <a name="bootstrapper-setupexe-command-line-arguments"></a>ブートストラップ (Setup.exe) のコマンド ライン引数  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] によって作成される Setup.exe と MSBuild タスクは、次の小さなコマンド ライン引数セットをサポートします。 ブートストラップ アプリケーションに提供されるこれ以外のすべての引数は、アプリケーション インストーラーに渡されます。  
  
 ブートストラップ オプションを変更する場合は、未署名のブートストラップを変更し、後でブートストラップ ファイルに署名する必要があります。  
  
|コマンド ライン引数|Description|  
|---------------------------|-----------------|  
|**-?、-h、-help**|[ヘルプ] ダイアログ ボックスを表示します。|  
|**-url、-componentsurl**|このセットアップ用に保存されている URL とコンポーネントの URL を表示します。|  
|**-url =**`location`|Setup.exe が [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] アプリケーションを検索する URL を設定します。|  
|**-componentsurl=** `location`|Setup.exe が [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] などの依存関係を検索する URL を設定します。 |  
|**-homesite=** `true` **&#124;** `false`|`true`の場合、は、ベンダーのサイトの適切な場所から依存関係をダウンロードします。 これにより、 **-の url** 設定がオーバーライドされます。 の場合 `false` 、 **-コンポーネント url**で指定された url から依存関係をダウンロードします。|  
  
## <a name="operating-system-support"></a>オペレーティング システムのサポート  
 Visual Studio ブートストラップは、Windows Server 2008 Server Core ではサポートされていません。また、機能が限定された、メンテナンスの容易なサーバー環境を提供する Windows Server 2008 R2 Server Core でもサポートされていません。 たとえば、Server Core のインストール オプションでは、.NET Framework 3.5 Server Core プロファイルのみがサポートされています。そのため、完全な .NET Framework を必要とする Visual Studio の機能は実行できません。  
  
## <a name="see-also"></a>参照  
 [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)   
 [ClickOnce のセキュリティと配置](../deployment/clickonce-security-and-deployment.md)
