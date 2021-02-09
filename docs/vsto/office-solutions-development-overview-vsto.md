---
title: Office ソリューションの開発の概要 (VSTO)
description: Word のワードプロセッシング機能や Excel のデータ分析機能など、使い慣れた Microsoft Office ユーザーインターフェイスとツールのカスタマイズを開発する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- primary interop assemblies, Office
- Office development in Visual Studio, about developing solutions
author: John-Hart
ms.author: johnhart
manager: jmartens
ms.workload:
- office
ms.openlocfilehash: 03da1c8052140bbe23ce4d99c12d72baef18898f
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99891957"
---
# <a name="office-solutions-development-overview-vsto"></a>Office ソリューションの開発の概要 (VSTO)
  ソリューションのフロント エンドとして Microsoft Office を使用すると、Word のワープロ機能、Excel のデータの分析機能、および Outlook の電子メール管理機能などの使い慣れた Microsoft Office のユーザー インターフェイスとツールを活用することができます。 Office アプリケーションのカスタマイズおよびビジネス プロセスに必要な特定の機能の追加を行うために、Visual Studio でソリューションを開発することができます。 たとえば、Word を既存のパーツからコントラクトを組み合わせるコントラクト ジェネレーターにすることができます。既存のパーツは編集可能または編集可能でない場合があります。 Excel では、さまざまなプロジェクト用にカスタマイズされた自動予算のワークシートを作成できます。 ユーザーはオフラインで Office ソリューションを取得することもできます。これは、Web ベースのアーキテクチャを使用する場合に、複雑なソリューションをより実用的なものにします。

 ここでは、Visual Studio の Office Developer Tools で使用可能な Visual Studio Tools for Office (VSTO) テンプレートを使用して作成できる、Office ソリューションの種類の概要について説明します。 Office での開発方法に関する一般的な情報については、「 [office デベロッパーセンター](https://developer.microsoft.com/office)」を参照してください。

## <a name="choose-an-office-project-type"></a>Office プロジェクトの種類の選択
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、VSTO ベースの Office 開発のために、次の種類のプロジェクト テンプレートを提供します。

- **ドキュメント レベルのカスタマイズ** は、特定のドキュメントに関連付けられます。

- **VSTO Add-ins** は、アプリケーション自体に関連付けられます。

  これらのプロジェクトの中でソリューションに最適な種類を決定するには、特定のドキュメントを開いたときにのみ実行するコードが必要かどうか、また、アプリケーションの実行時に使用できるコードが必要かどうかについて考えます。 プロジェクトテンプレートの詳細については、「 [Office プロジェクトテンプレートの概要](../vsto/office-project-templates-overview.md)」を参照してください。

  作成できるプロジェクトの種類は、開発用コンピューターにインストールした Office アプリケーションによって異なります。 詳細については、「 [Office アプリケーションおよびプロジェクトの種類別の使用可能な機能](../vsto/features-available-by-office-application-and-project-type.md)」を参照してください。

### <a name="document-level-customizations"></a>ドキュメント レベルのカスタマイズ
 ドキュメント レベルのカスタマイズは、Microsoft Office Word または Microsoft Office Excel 内の単一のドキュメント、ブック、またはテンプレートに関連付けられているアセンブリで構成されます。 このアセンブリは、関連付けられたドキュメントを開いたときに読み込まれます。 作成するカスタマイズの機能は、関連付けられたドキュメントが開いている場合にのみ使用できます。 カスタマイズでは、任意のドキュメントが開いている場合の新しいメニュー項目やリボン タブの表示など、アプリケーション全体に変更を加えることはできません。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、ドキュメント レベルのカスタマイズを作成するのに役立つツールが含まれています。 カスタマイズするドキュメントは、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]のデザイン サーフェイスとしてホストされます。これにより、コントロールをドキュメントにドラッグ アンド ドロップして、ドキュメントをデザインすることができます。 その他の多くの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 機能は、Windows フォーム コントロール、ドラッグ アンド ドロップのデータ バインディング、および統合デバッガーなど、ドキュメント レベルのプロジェクトで利用可能です。

 カスタマイズの詳細については、次のトピックを参照してください。

- [Excel のドキュメントレベルのカスタマイズのプログラミングの概要](../vsto/getting-started-programming-document-level-customizations-for-excel.md)

- [Word のドキュメントレベルのカスタマイズのプログラミングの概要](../vsto/getting-started-programming-document-level-customizations-for-word.md)

- [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)

### <a name="vsto-add-ins"></a>VSTO アドイン
 VSTO アドインは、Microsoft Office アプリケーションに関連付けられているアセンブリで構成されます。 アプリケーションが既に実行されている場合に VSTO アドインを読み込むこともできますが、通常、VSTO アドインは関連付けられたアプリケーションが開始されたときに実行されます。 作成した VSTO アドインの機能は、どのドキュメントが開いているかにかかわらず、アプリケーション自体に対して使用できます。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、VSTO アドインの作成に役立つツールが用意されています。アドインプロジェクトには、VSTO アドインを表す自動的に生成されたクラスが含まれます。 このクラスは、ホスト アプリケーションのオブジェクト モデルへのアクセス、および VSTO アドインの読み込みとシャット ダウン時のコードの実行に使用できる、プロパティとイベントを提供します。 その他の多くの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 機能は、Windows フォームや統合デバッガーなどの VSTO アドイン プロジェクトで利用可能です。

 VSTO アドインの詳細については、次のトピックを参照してください。

- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)

- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)

## <a name="automate-office-applications-by-using-primary-interop-assemblies"></a>プライマリ相互運用機能アセンブリを使用して Office アプリケーションを自動化する
 アプリケーションのオブジェクト モデルにアクセスするコードを記述して、Office アプリケーションの機能をソリューションにプログラムによって組み込むことができます。 オブジェクト モデルは、さまざまなプロパティとメソッドを介して機能を公開するクラスの配置です。 各 Office アプリケーションのオブジェクト モデルは異なります。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]の Office 開発者ツールを使用して作成されたソリューションから Office アプリケーションのオブジェクト モデルを使用するには、アプリケーションのプライマリ相互運用機能アセンブリ (PIA) を使用する必要があります。 PIA によって、Office アプリケーションの COM ベースのオブジェクト モデルと対話するソリューション内にマネージド コードを作成できるようになります。

 ほとんどの開発タスクを実行するには、開発用コンピューターのグローバル アセンブリ キャッシュに Office PIA をインストールし、登録する必要があります。 詳細については、「 [Office ソリューションを開発するためのコンピューターの構成](../vsto/configuring-a-computer-to-develop-office-solutions.md)」を参照してください。 エンド ユーザーのコンピューターで VSTO Office ソリューションを実行する場合には、Office PIA は必要ありません。 詳細については、「 [Office ソリューションの設計と作成](../vsto/designing-and-creating-office-solutions.md)」を参照してください。

 VSTO Office ソリューションでの PIA の使用に関する詳細については、次のトピックを参照してください。

- [Office ソリューションでコードを記述する](../vsto/writing-code-in-office-solutions.md)

- [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)

## <a name="run-microsoft-vsto-office-solutions-on-end-user-computers"></a>エンドユーザーのコンピューターで Microsoft VSTO Office ソリューションを実行する
 VSTO Office ソリューションを作成する場合、配置要件が開発方法に与える可能性のある影響について考慮します。

### <a name="deployment-options"></a>デプロイ オプション
 ClickOnce または Windows インストーラーを使用して、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]の Office 開発者ツールを使用して作成したソリューションを配置します。 ClickOnce の配置では、インストールできる自己更新ソリューションを作成し、最小限のユーザー操作で実行することができます。 Windows インストーラー (*.msi*) ファイルは、エンドユーザーのコンピューターに簡単に配布することも、Systems Management SERVER (SMS) を使用して配布することもできます。 VSTO Office ソリューションの配置の詳細については、「 [office ソリューションの配置](../vsto/deploying-an-office-solution.md)」を参照してください。

### <a name="install-prerequisites"></a>必須コンポーネントのインストール
 エンド ユーザーが [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]の Office 開発者ツールを使用して作成したソリューションを実行できるようにするには、ユーザーのコンピューターに特定の必須コンポーネントがインストールされている必要があります。 ClickOnce を使用するか、Windows インストーラー ファイルを作成して、ソリューションを配置する場合は、ソリューションと共にこれらの必須コンポーネントをインストールできます。 詳細については、「 [office ソリューションの配置の前提条件](/previous-versions/bb608617(v=vs.110)) 」および「 [方法: office ソリューションを実行するためにエンドユーザーのコンピューターに必須コンポーネントをインストール](/previous-versions/bb608608(v=vs.110))する」を参照してください。

### <a name="security"></a>セキュリティ
 VSTO Office ソリューションのセキュリティは、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] がソリューションのインストールおよび読み込み時に作成する一連のチェックによって強制されます。 これらのチェックには、配置マニフェストの場所が信頼されているかどうか、または配置マニフェストの署名に使用される証明書が信頼されているかどうかの検証が含まれます。 詳細については、「 [Office ソリューションのセキュリティ保護](../vsto/securing-office-solutions.md)」を参照してください。

## <a name="see-also"></a>関連項目
- [Visual Studio で &#40;Office 開発を開始する&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [ドキュメントレベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)
- [Architecture of VSTO Add-Ins](../vsto/architecture-of-vsto-add-ins.md)
- [Excel のドキュメントレベルのカスタマイズのプログラミングの概要](../vsto/getting-started-programming-document-level-customizations-for-excel.md)
- [Word のドキュメントレベルのカスタマイズのプログラミングの概要](../vsto/getting-started-programming-document-level-customizations-for-word.md)
- [VSTO アドインのプログラミングの概要](../vsto/getting-started-programming-vsto-add-ins.md)
