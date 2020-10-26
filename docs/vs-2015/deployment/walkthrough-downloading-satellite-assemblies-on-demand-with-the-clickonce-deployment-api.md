---
title: 'チュートリアル: ClickOnce 配置 API を使用して必要に応じてサテライトアセンブリをダウンロードする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, globalization
- localization, Windows Forms
- Windows Forms, localization
- globalization, ClickOnce
- satellite assemblies, ClickOnce
- ClickOnce deployment, on-demand download
- localization, ClickOnce deployment
- ClickOnce deployment, localization
ms.assetid: fdaa553f-a27e-44eb-a4e2-08c122105a87
caps.latest.revision: 13
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: a84de037661992d1ee185bea2a70db74dac5e618
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65686352"
---
# <a name="walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api"></a>チュートリアル : ClickOnce 配置 API を使用して必要に応じてサテライト アセンブリをダウンロードする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

サテライト アセンブリを使用すると、複数のカルチャに対して Windows フォーム アプリケーションを構成できます。 *サテライト アセンブリ* とは、アプリケーションの既定のカルチャ以外のカルチャ用アプリケーション リソースを含むアセンブリのことです。  
  
 「 [ClickOnce アプリケーションのローカライズ](../deployment/localizing-clickonce-applications.md)」で説明したように、同じデプロイ内の複数のカルチャに対して複数のサテライトアセンブリを含めることができ [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 既定では、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] により配置に含まれるすべてのサテライト アセンブリがクライアント コンピューターにダウンロードされます。ただし、多くの場合、1 つのクライアントに必要なサテライト アセンブリは 1 つだけです。  
  
 このチュートリアルでは、サテライト アセンブリをオプションとしてマークする方法、および現在のカルチャ設定にクライアント コンピューターが必要とするアセンブリのみをダウンロードする方法について説明します。 次の手順では、 [!INCLUDE[winsdklong](../includes/winsdklong-md.md)]から入手できるツールを使用します。 このタスクを、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]を使用して実行することもできます。  「 [チュートリアル: デザイナーを使用し、ClickOnce 配置 API で必要に応じてサテライト アセンブリをダウンロードする](https://msdn.microsoft.com/library/ms366788\(v=vs.110\)) 」または「 [チュートリアル: デザイナーを使用し、ClickOnce 配置 API で必要に応じてサテライト アセンブリをダウンロードする](https://msdn.microsoft.com/library/ms366788\(v=vs.120\))」もご覧ください。  
  
> [!NOTE]
> 次のコード例は、テストを目的としているため、プログラム内でカルチャを `ja-JP`に設定しています。 このコードを運用環境用に調整する方法については、このトピックの「次の手順」セクションを参照してください。  
  
## <a name="prerequisites"></a>必須コンポーネント  
 このトピックでは、ローカライズされたリソースを、Visual Studio を使用してアプリケーションに追加する方法を理解していることを想定しています。 手順について詳しくは、「 [チュートリアル: Windows フォームのローカリゼーション](https://msdn.microsoft.com/library/vstudio/y99d1cd3\(v=vs.100\).aspx)」をご覧ください。  
  
### <a name="to-download-satellite-assemblies-on-demand"></a>必要に応じてサテライト アセンブリをダウンロードするには  
  
1. アプリケーションに次のコードを追加して、サテライト アセンブリのオンデマンドでのダウンロードを有効にします。  
  
     [!code-csharp[ClickOnce.SatelliteAssembliesSDK#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesSDK/CS/Program.cs#1)]
     [!code-vb[ClickOnce.SatelliteAssembliesSDK#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesSDK/VB/Form1.vb#1)]  
  
2. [Resgen.exe (リソースファイルジェネレーター)](https://msdn.microsoft.com/library/8ef159de-b660-4bec-9213-c3fbc4d1c6f4)またはを使用して、アプリケーションのサテライトアセンブリを生成し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。  
  
3. MageUI.exe を使用して、アプリケーション マニフェストを生成するか、または既存のアプリケーション マニフェストを開きます。 このツールの詳細については、「 [MageUI.exe (マニフェスト生成および編集ツール、グラフィカルクライアント)](https://msdn.microsoft.com/library/f9e130a6-8117-49c4-839c-c988f641dc14)」を参照してください。  
  
4. **[Files]** タブをクリックします。  
  
5. **省略記号**ボタン ([**...**]) をクリックし、Resgen.exe を使用して生成したサテライトアセンブリを含む、アプリケーションのすべてのアセンブリとファイルを含むディレクトリを選択します。 (サテライトアセンブリは、 *isocode*\ApplicationName.resources.dll の形式で名前が付いています。 *ISOCODE* は RFC 1766 形式の言語識別子です)。  
  
6. **[作成]** をクリックして、配置にファイルを追加します。  
  
7. 各サテライト アセンブリの **[省略可能]** チェック ボックスをオンにします。  
  
8. 各サテライト アセンブリの [グループ] フィールドに ISO 言語識別子を設定します。 たとえば、日本語のサテライト アセンブリであれば、ダウンロード グループ名として「 `ja-JP`から入手できるツールを使用します。 これにより、ユーザーの <xref:System.Threading.Thread.CurrentUICulture%2A> プロパティの設定に応じて該当するサテライト アセンブリをダウンロードする、手順 1 で追加したコードが有効になります。  
  
## <a name="next-steps"></a>次の手順  
 コード例を見ると、 <xref:System.Threading.Thread.CurrentUICulture%2A> が特定の値に設定されています。しかし、運用環境では、クライアント コンピューターに適切な値が既定で設定されるため、この行は削除する必要があります。 たとえば、アプリケーションを日本語のクライアント コンピューターで実行する場合、既定では <xref:System.Threading.Thread.CurrentUICulture%2A> が `ja-JP` になります。 ここでは、アプリケーションの配置前にサテライト アセンブリをテストするという趣旨でプログラムから値を設定しています。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションのローカライズ](../deployment/localizing-clickonce-applications.md)
