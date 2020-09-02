---
title: 'チュートリアル: デザイナーを使用して、ClickOnce 配置 API で必要に応じてサテライトアセンブリをダウンロードする |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- Windows Forms, globalization
- ClickOnce deployment, globalization
- localization, Windows Forms
- ClickOnce, on-demand download
- Windows Forms, localization
- ClickOnce deployment, localization
- walkthroughs, localization
ms.assetid: 82b85a47-b223-4221-a17c-38a52c3fb6e2
caps.latest.revision: 12
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 559fb1f3613b42bd2c972f61b45736b07e76a318
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62420030"
---
# <a name="walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api-using-the-designer"></a>チュートリアル : デザイナーを使用し、ClickOnce 配置 API で必要に応じてサテライト アセンブリをダウンロードする

[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

サテライト アセンブリを使用すると、複数のカルチャに対して Windows フォーム アプリケーションを構成できます。 *サテライト アセンブリ* とは、アプリケーションの既定のカルチャ以外のカルチャ用アプリケーション リソースを含むアセンブリのことです。

「 [ClickOnce アプリケーションのローカライズ](../deployment/localizing-clickonce-applications.md)」で説明したように、同じデプロイ内の複数のカルチャに対して複数のサテライトアセンブリを含めることができ [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。 既定では、 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] により配置に含まれるすべてのサテライト アセンブリがクライアント コンピューターにダウンロードされます。ただし、多くの場合、1 つのクライアントに必要なサテライト アセンブリは 1 つだけです。

このチュートリアルでは、サテライト アセンブリをオプションとしてマークする方法、および現在のカルチャ設定にクライアント コンピューターが必要とするアセンブリのみをダウンロードする方法について説明します。

> [!NOTE]
> 次のコード例は、テストを目的としているため、プログラム内でカルチャを `ja-JP` に設定しています。 このコードを運用環境用に調整する方法については、このトピックの「次の手順」セクションを参照してください。

### <a name="to-mark-satellite-assemblies-as-optional"></a>サテライト アセンブリをオプションとしてマークするには

1. プロジェクトをビルドします。 これにより、ローカライズの対象としているすべてのカルチャについて、サテライト アセンブリが生成されます。

2. ソリューション エクスプローラーでご利用のプロジェクト名を右クリックし、**[プロパティ]** をクリックします。

3. **[発行]** タブをクリックし、**[アプリケーション ファイル]** をクリックします。

4. **[すべてのファイルを表示]** チェック ボックスをオンにして、サテライト アセンブリを表示します。 既定では、すべてのサテライト アセンブリが配置対象に含められ、このダイアログ ボックスに表示されます。

     サテライトアセンブリは、 *isocode*\ApplicationName.resources.dll の形式で名前を持ちます。 *ISOCODE* は RFC 1766 形式の言語識別子です。

5. 各言語識別子の [**ダウンロードグループ**] ボックスの一覧の [**新規作成...** ] をクリックします。 ダウンロード グループ名の入力を求めるメッセージが表示されたら、言語識別子を入力します。 たとえば、日本語のサテライトアセンブリの場合は、ダウンロードグループ名を指定し `ja-JP` ます。

6. **[アプリケーション ファイル]** ダイアログ ボックスを閉じます。

### <a name="to-download-satellite-assemblies-on-demand-in-c"></a>必要に応じてサテライト アセンブリをダウンロードするには (C\#)

1. Program.cs ファイルを開きます。 このファイルがソリューション エクスプローラーに表示されない場合は、プロジェクトを選択し、**[プロジェクト]** メニューの **[すべてのファイルを表示]** をクリックします。

2. 該当するサテライト アセンブリをダウンロードし、アプリケーションを起動するには、次のコードを使用します。

     [!code-csharp[ClickOnce.SatelliteAssemblies#1](../snippets/csharp/VS_Snippets_Winforms/ClickOnce.SatelliteAssemblies/CS/Program.cs#1)]

### <a name="to-download-satellite-assemblies-on-demand-in-visual-basic"></a>必要に応じてサテライト アセンブリをダウンロードするには (Visual Basic)

1. アプリケーションの **[プロパティ]** ウィンドウで、**[アプリケーション]** タブをクリックします。

2. タブ ページの一番下にある **[アプリケーション イベントの表示]** をクリックします。

3. ApplicationEvents.VB ファイルの先頭に、次の Imports ステートメントを追加します。

     [!code-vb[ClickOnce.SatelliteAssembliesVB#1](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesVB/VB/ApplicationEvents.vb#1)]

4. 次のコードを `MyApplication` クラスに追加します。

     [!code-vb[ClickOnce.SatelliteAssembliesVB#2](../snippets/visualbasic/VS_Snippets_Winforms/ClickOnce.SatelliteAssembliesVB/VB/ApplicationEvents.vb#2)]

## <a name="next-steps"></a>次の手順

コード例を見ると、<xref:System.Threading.Thread.CurrentUICulture%2A> が特定の値に設定されています。しかし、運用環境では、クライアント コンピューターに適切な値が既定で設定されるため、この行は削除する必要があります。 たとえば、アプリケーションを日本語のクライアント コンピューターで実行する場合、既定では <xref:System.Threading.Thread.CurrentUICulture%2A> が `ja-JP` になります。 ここでは、アプリケーションの配置前にサテライト アセンブリをテストするという趣旨でプログラムから設定しています。

## <a name="see-also"></a>参照

- [チュートリアル : ClickOnce 配置 API を使用して必要に応じてサテライト アセンブリをダウンロードする](../deployment/walkthrough-downloading-satellite-assemblies-on-demand-with-the-clickonce-deployment-api.md)
- [ClickOnce アプリケーションのローカライズ](../deployment/localizing-clickonce-applications.md)
