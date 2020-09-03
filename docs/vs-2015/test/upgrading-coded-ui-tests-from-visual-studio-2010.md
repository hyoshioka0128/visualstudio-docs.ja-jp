---
title: コード化された UI テストのアップグレード
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-test
ms.topic: conceptual
ms.assetid: 11232a83-73ea-46bd-bc0c-46f74f6e3a42
caps.latest.revision: 35
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: 3a29e531ca9b2a74e67abf80a0e3017a0f5b0b07
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "74297992"
---
# <a name="upgrading-coded-ui-tests-from-visual-studio-2010"></a>Visual Studio 2010 からのコード化された UI テストのアップグレード
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] SP1 で作成したコード化された UI テストを含むテスト プロジェクトは、Visual Studio 2012 で開いたときに自動的に修復されます。 テスト プロジェクトがソース管理にチェックインされると、プロジェクト ファイルはこの修復のためにチェックアウトされます。 コード化された UI テストを含むこれらのテスト プロジェクトは、一度修復されると、 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] SP1 と [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]の両方で使用できます。

 **必要条件**

- Visual Studio Enterprise

> [!NOTE]
> Visual Studio には、テスト プロジェクトの種類が複数含まれています。 コード化された UI テストを新しく作成する場合は、コード化された UI テスト プロジェクトの種類で作成されます。 詳しくは、「 [旧バージョンの Visual Studio からのテストのアップグレード](https://msdn.microsoft.com/e9c8b7f6-bd72-448e-8edb-d090dcc5cf52)」をご覧ください。

> [!WARNING]
> コード化された UI テストを含む[!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] テスト プロジェクトは、 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] または [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] と [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]の side-by-side 実行で開くときにリビルドする必要があります。

> [!WARNING]
> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] で作成され、単体テストのみを含むテスト プロジェクトを [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]で開くと、コード化された UI テストを追加することはできません。 同様に、 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]で作成された単体テスト プロジェクトにコード化された UI テストを追加することはできません。

## <a name="compatibility-issues-between-visual-studio-2010-and-visual-studio-2012"></a>Visual Studio 2010 と Visual Studio 2012 の間の互換性の問題
 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] と [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]間でコード化された UI テストを移行する際に注意が必要な問題を次の表に示します。

> [!CAUTION]
> ソリューション エクスプローラーに表示されない、コード化された UI テスト プロジェクトでの参照に関する既知の問題があります。 詳細については、 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] のインストール メディアに含まれている ReadMe ファイルを参照してください。

|コード化された UI の機能|問題|解決策|
|----------------------------|-----------|--------------|
|Silverlight UI テストは [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]ではサポートされていません。|**ビルドは失敗します。**<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] Feature Pack 2 を使用していて、Silverlight アプリケーション用にコード化された UI テスト プロジェクトを作成した場合、これらのプロジェクトを [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]で開くことはできません。|これらのプロジェクトは [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] Feature Pack 2 のみで管理することをお勧めします。|
|Firefox UI テストは [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]ではサポートされていません。|**ビルドは成功しますが、テストの実行は失敗します。**<br /><br /> [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] Feature Pack 2 を使用していて、Firefox の Web アプリケーション用にコード化された UI テスト プロジェクトを作成した場合、これらのプロジェクトを [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]で開くことはできません。|これらのプロジェクトは [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] Feature Pack 2 のみで管理することをお勧めします。|
|新しい UI コード テスト API が [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]に追加されました。|**ビルドは失敗します。**<br /><br /> [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]で新しい UI テスト API を使用してコード化された UI テストを作成した場合、これらのプロジェクトを [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]で開くことはできません。|新しい API を使用したプロジェクトは、 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] のみで管理する必要があります。|
|[!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)]では、csproj ファイルの "選択" ステートメント内に参照が追加されました。 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]では、フィードバックのターゲット ファイルを使用して、コード化された UI テスト アセンブリの参照を含めます。|[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]では、 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] (または SP1) で作成された、コード化された UI テストを含まないテスト プロジェクトに、コード化された UI テストを追加できません。<br /><br /> 修復処理は、ターゲット ファイルと選択ステートメントを追加します。 コード化された UI テストがテスト プロジェクト内にない場合、そのプロジェクトは修復済みとしてマークされ、 [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]でコード化された UI テストを追加する際に適切な参照が追加されません。|[!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)] を使用して同じソリューション内に新しいテスト プロジェクトを作成し、その中に新しいコード化された UI テストを追加する必要があります。 または、 [!INCLUDE[vs_dev10_long](../includes/vs-dev10-long-md.md)] SP1 でテスト プロジェクトにコード化された UI テストを追加し、そのプロジェクトを [!INCLUDE[vs_dev11_long](../includes/vs-dev11-long-md.md)]で開くこともできます。|

## <a name="visual-studio-2010-sp1-update"></a><a name="UpgradingCodedUIFromVS2010_Update"></a> Visual Studio 2010 SP1 更新プログラム
 Visual Studio 2012 および Windows 8 の互換性をサポートする [!INCLUDE[vs2010](../includes/vs2010-md.md)] SP1 の更新プログラムは [Microsoft ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=34677) で Visual Studio 更新プログラムとしてもダウンロードできます。

 更新プログラムを適用すると、次の [!INCLUDE[vs2010](../includes/vs2010-md.md)] SP1 のコード化された UI テスト ツール機能が Windows 8 向けに改善されます。

- Windows 8 を実行しているコンピューターで、Microsoft .NET Framework 4.5 ベースの Windows Presentation Foundation (WPF) コントロールにコード化された UI テストを実行できます。

- Windows 8 を実行しているコンピューターで、64 ビット (x64) の Internet Explorer 10 にコード化された UI テストを実行できます。

  この更新プログラムには、次の問題の修正プログラムも含まれています。

- **コード カバレッジ:** Visual Studio 2012 で作成されたコード カバレッジ ファイル (.coverage) を [!INCLUDE[vs2010](../includes/vs2010-md.md)] SP1 で開くことができません。

- **取り残されたテスト アーティファクト:** Team Foundation Server (TFS) 2010 の無効なユーザーに割り当てられているテスト アーティファクトがあります。 たとえば、退職したユーザーにまだ割り当てられたままのテスト ケースがあります。 TFS 2010 を TFS 2012 にアップグレードします。 [!INCLUDE[TCMext](../includes/tcmext-md.md)] 2010 を使用して、アップグレードした TFS サーバーに接続します。 [!INCLUDE[TCMext](../includes/tcmext-md.md)] 2010 を使用して、任意の TFS ユーザーにテスト アーティファクトを割り当てることはできません。

- **ロード テスト:** Windows 8 を実行しているコンピューターで、ローカル エリア ネットワーク (LAN) プロファイル以外のネットワークの種類でロード テストを実行すると、ネットワーク エミュレーターのドライバーにより、オペレーティング システムがクラッシュします。 詳細については、「 [サポート技術情報記事 2736182](https://support.microsoft.com/help/2736182/a-gdr-update-for-visual-studio-2010-sp1-is-available-to-add-compatibil)」を参照してください。

## <a name="see-also"></a>参照
 [Visual Studio プロジェクトの移植、移行、およびアップグレード Visual](../porting/porting-migrating-and-upgrading-visual-studio-projects.md) [studio の以前のバージョンからのテストのアップグレード](https://msdn.microsoft.com/e9c8b7f6-bd72-448e-8edb-d090dcc5cf52) [UI オートメーションを使用してコードをテストする](../test/use-ui-automation-to-test-your-code.md)[既存の操作からコード化](https://msdn.microsoft.com/library/56736963-9027-493b-b5c4-2d4e86d1d497)された ui テストを生成するコード[化された ui テストと操作の記録に対してサポートされる構成とプラットフォーム](../test/supported-configurations-and-platforms-for-coded-ui-tests-and-action-recordings.md)を記録する
