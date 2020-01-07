---
title: Office ソリューション開発の概要 (VSTO)
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
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 45b9dba16a0a8ebf6baaf2f1d7660035294fd80d
ms.sourcegitcommit: 94b3a052fb1229c7e7f8804b09c1d403385c7630
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "62977940"
---
# <a name="office-solutions-development-overview-vsto"></a>Office ソリューション開発の概要 (VSTO)
  ソリューションのフロント エンドとして Microsoft Office を使用すると、Word のワープロ機能、Excel のデータの分析機能、および Outlook の電子メール管理機能などの使い慣れた Microsoft Office のユーザー インターフェイスとツールを活用することができます。 Office アプリケーションのカスタマイズおよびビジネス プロセスに必要な特定の機能の追加を行うために、Visual Studio でソリューションを開発することができます。 たとえば、Word を既存のパーツからコントラクトを組み合わせてコントラクト ジェネレーターにすることができます。既存のパーツは編集可能である場合も編集可能でない場合もあります。 Excel では、さまざまなプロジェクト用にカスタマイズされた自動予算のワークシートを作成できます。 ユーザーはオフラインで Office ソリューションを取得することもできます。これは、Web ベースのアーキテクチャを使用する場合に、複雑なソリューションをより実用的なものにします。

 ここでは、Visual Studio の Office Developer Tools で使用可能な Visual Studio Tools for Office (VSTO) テンプレートを使用して作成できる、Office ソリューションの種類の概要について説明します。 Office での開発方法に関する概要については、[Office デベロッパー センター](https://dev.office.com/)を参照してください。

## <a name="choose-an-office-project-type"></a>Office プロジェクトの種類の選択
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] では、VSTO ベースの Office 開発のために、次の種類のプロジェクト テンプレートを提供します。

- **ドキュメント レベルのカスタマイズ** は、特定のドキュメントに関連付けられます。

- **VSTO Add-ins** は、アプリケーション自体に関連付けられます。

  これらのプロジェクトの中でソリューションに最適な種類を決定するには、特定のドキュメントを開いたときにのみ実行するコードが必要かどうか、また、アプリケーションの実行時に使用できるコードが必要かどうかについて考えます。 プロジェクト テンプレートの詳細については、[Office プロジェクト テンプレートの概要](../vsto/office-project-templates-overview.md)を参照してください。

  作成できるプロジェクトの種類は、開発用コンピューターにインストールした Office アプリケーションによって異なります。 詳細については、[Office アプリケーションおよびプロジェクトの種類で使用できる機能](../vsto/features-available-by-office-application-and-project-type.md)を参照してください。

### <a name="document-level-customizations"></a>ドキュメント レベルのカスタマイズ
 ドキュメント レベルのカスタマイズは、Microsoft Office Word または Microsoft Office Excel 内の単一のドキュメント、ブック、またはテンプレートに関連付けられているアセンブリで構成されます。 このアセンブリは、関連付けられたドキュメントを開いたときに読み込まれます。 作成するカスタマイズの機能は、関連付けられたドキュメントが開いている場合にのみ使用できます。 カスタマイズでは、任意のドキュメントが開いている場合の新しいメニュー項目やリボン タブの表示など、アプリケーション全体に変更を加えることはできません。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、ドキュメント レベルのカスタマイズを作成するのに役立つツールが含まれています。 カスタマイズするドキュメントは、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]のデザイン サーフェイスとしてホストされます。これにより、コントロールをドキュメントにドラッグ アンド ドロップして、ドキュメントをデザインすることができます。 その他の多くの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 機能は、Windows フォーム コントロール、ドラッグ アンド ドロップのデータ バインディング、および統合デバッガーなど、ドキュメント レベルのプロジェクトで利用可能です。

 カスタマイズの詳細については、次のトピックを参照してください。

- [Excel をドキュメント レベルでカスタマイズするプログラミングを始める](../vsto/getting-started-programming-document-level-customizations-for-excel.md)

- [Word をドキュメント レベルでカスタマイズするプログラミングを始める](../vsto/getting-started-programming-document-level-customizations-for-word.md)

- [ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)

### <a name="vsto-add-ins"></a>VSTO アドイン
 VSTO アドインは、Microsoft Office アプリケーションに関連付けられているアセンブリで構成されます。 アプリケーションが既に実行されている場合に VSTO アドインを読み込むこともできますが、通常、VSTO アドインは関連付けられたアプリケーションが開始されたときに実行されます。 作成した VSTO アドインの機能は、どのドキュメントが開いているかにかかわらず、アプリケーション自体に対して使用できます。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] には、VSTO アドインの作成に役立つツールが含まれています。アドイン プロジェクトには、VSTO アドインを表す自動的に生成されたクラスが含まれます。 このクラスは、ホスト アプリケーションのオブジェクト モデルへのアクセス、および VSTO アドインの読み込みとシャットダウン時のコードの実行に使用できる、プロパティとイベントを提供します。 その他の多くの [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] 機能は、Windows フォームや統合デバッガーなどの VSTO アドイン プロジェクトで利用可能です。

 VSTO アドインの詳細については、次のトピックを参照してください。

- [VSTO アドインのプログラミングを始める](../vsto/getting-started-programming-vsto-add-ins.md)

- [VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)

## <a name="automate-office-applications-by-using-primary-interop-assemblies"></a>プライマリ相互運用機能アセンブリを使用した Office アプリケーションの自動化
 アプリケーションのオブジェクト モデルにアクセスするコードを記述して、Office アプリケーションの機能をソリューションにプログラムによって組み込むことができます。 オブジェクト モデルは、さまざまなプロパティとメソッドを介して機能を公開するクラスの配置です。 各 Office アプリケーションのオブジェクト モデルは異なります。

 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]の Office 開発者ツールを使用して作成されたソリューションから Office アプリケーションのオブジェクト モデルを使用するには、アプリケーションのプライマリ相互運用機能アセンブリ (PIA) を使用する必要があります。 PIA によって、Office アプリケーションの COM ベースのオブジェクト モデルと対話するソリューション内にマネージド コードを作成できるようになります。

 ほとんどの開発タスクを実行するには、開発用コンピューターのグローバル アセンブリ キャッシュに Office PIA をインストールし、登録する必要があります。 詳細については、[Office ソリューションの開発のためのコンピューター構成](../vsto/configuring-a-computer-to-develop-office-solutions.md)を参照してください。 エンド ユーザーのコンピューターで VSTO Office ソリューションを実行する場合には、Office PIA は必要ありません。 詳細については、[Office ソリューションのデザインと作成](../vsto/designing-and-creating-office-solutions.md)を参照してください。

 VSTO Office ソリューションでの PIA の使用に関する詳細については、次のトピックを参照してください。

- [Office ソリューションでのコードの記述](../vsto/writing-code-in-office-solutions.md)

- [Office プライマリ相互運用機能アセンブリ](../vsto/office-primary-interop-assemblies.md)

## <a name="run-microsoft-vsto-office-solutions-on-end-user-computers"></a>エンドユーザーのコンピューターでの Microsoft VSTO Office ソリューションの実行
 VSTO Office ソリューションを作成する場合、配置要件が開発方法に与える可能性のある影響について考慮します。

### <a name="deployment-options"></a>配置オプション
 ClickOnce または Windows インストーラーを使用して、 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]の Office 開発者ツールを使用して作成したソリューションを配置します。 ClickOnce の配置では、インストールできる自己更新ソリューションを作成し、最小限のユーザー操作で実行することができます。 Windows インストーラー (*.msi*) ファイルを簡単にエンドユーザーのコンピューターに配布または Systems Management Server (SMS) を使用して配布します。 VSTO Office ソリューションの配置に関する詳細については、[Office ソリューションを配置](../vsto/deploying-an-office-solution.md)を参照してください。

### <a name="install-prerequisites"></a>必須コンポーネントのインストール
 エンド ユーザーが [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]の Office 開発者ツールを使用して作成したソリューションを実行できるようにするには、ユーザーのコンピューターに特定の必須コンポーネントがインストールされている必要があります。 ClickOnce を使用するか、Windows インストーラー ファイルを作成して、ソリューションを配置する場合は、ソリューションと共にこれらの必須コンポーネントをインストールできます。 詳細については、[Office ソリューションをデプロイする前提条件](https://msdn.microsoft.com/9f672809-43a3-40a1-9057-397ce3b5126e)と[エンド ユーザー コンピューター上で Office ソリューションを実行するための前提条件のインストール方法](https://msdn.microsoft.com/74dd2c52-838f-4abf-b2b4-4d7b0c2a0a98)を参照してください。

### <a name="security"></a>セキュリティ
 VSTO Office ソリューションのセキュリティは、 [!INCLUDE[vsto_runtime](../vsto/includes/vsto-runtime-md.md)] がソリューションのインストールおよび読み込み時に作成する一連のチェックによって強制されます。 これらのチェックには、配置マニフェストの場所が信頼されているかどうか、または配置マニフェストの署名に使用される証明書が信頼されているかどうかの検証が含まれます。 詳細については、[セキュリティで保護された Office ソリューション](../vsto/securing-office-solutions.md)を参照してください。

## <a name="see-also"></a>関連項目
- [はじめに &#40;Visual Studio での Office 開発&#41;](../vsto/getting-started-office-development-in-visual-studio.md)
- [ドキュメント レベルのカスタマイズのアーキテクチャ](../vsto/architecture-of-document-level-customizations.md)
- [VSTO アドインのアーキテクチャ](../vsto/architecture-of-vsto-add-ins.md)
- [Excel をドキュメント レベルでカスタマイズするプログラミングを始める](../vsto/getting-started-programming-document-level-customizations-for-excel.md)
- [Word をドキュメント レベルでカスタマイズするプログラミングを始める](../vsto/getting-started-programming-document-level-customizations-for-word.md)
- [VSTO アドインのプログラミングを始める](../vsto/getting-started-programming-vsto-add-ins.md)
