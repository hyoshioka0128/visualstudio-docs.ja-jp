---
title: SharePoint ソリューションパッケージを作成しています |Microsoft Docs
description: パッケージデザイナーを使用して、SharePoint ソリューションの配置パッケージを作成およびカスタマイズします。 パッケージングツール、デザイナーオプション、およびフォルダー構造について説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, packages
- packages [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: bbe458f6ab4de01ffb224ae4e493bf23e3fc6ceb
ms.sourcegitcommit: ad2c820b280b523a7f7aef89742cdb719354748f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2020
ms.locfileid: "94850560"
---
# <a name="create-sharepoint-solution-packages"></a>SharePoint ソリューションパッケージの作成
  配置パッケージを作成したりカスタマイズしたりするには、パッケージ デザイナーを使用します。 たとえば、SharePoint のプロジェクト項目およびフィーチャーの追加、IIS サーバーのリセット、フィーチャーのアクティブ化スコープの設定、フィーチャーの依存関係の特定などを行うことができます。 このデザイナーでは、マニフェスト (個々のパッケージを記述した XML ファイル) を生成することもできます。

## <a name="packaging-tools"></a>パッケージングツール
 パッケージ **デザイナー** を使用して、パッケージをカスタマイズし、マニフェストを生成することができます。 SharePoint のプロジェクト項目の追加、Web サーバーのリセットの構成、および配置用サーバーの種類の設定を行うことができます。 詳細については、「 [方法: パッケージデザイナーを使用して、パッケージに機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)」を参照してください。

 または、 **パッケージングエクスプローラー** を使用して、パッケージファイル (*.Wsp*) の機能と項目を変更することもできます。 詳細については、「 [方法: パッケージングエクスプローラーを使用して、パッケージに機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-packaging-explorer.md)」を参照してください。

 Visual Studio と MSBuild を使用して、SharePoint ソリューションを配置するためのパッケージ (*.wsp*) ファイルを作成できます。 SharePoint の配置に必要なマニフェスト ファイルはこのプロセスで生成されます。 詳細については、「 [方法: MSBuild タスクを使用して SharePoint ソリューションパッケージを作成](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)する」を参照してください。

## <a name="package-designer-options"></a>パッケージデザイナーのオプション
 次の表は、 **パッケージデザイナー** を使用して SharePoint パッケージでカスタマイズできるプロパティを示しています。

|パッケージ デザイナーのプロパティ|既定の設定に関する説明|
|-------------------------------|------------------------------------|
|名前|必須。 パッケージの既定の名前は *ProjectName* に設定されています。|
|[Web サーバーのリセット]|省略可能。 SharePoint サーバーに *.wsp* ファイルがインストールされた後に Web サーバーを再起動する場合に選択します。|
|配置サーバーの種類|省略可能。 パッケージをホストしているサーバーの種類を表します。 設定されていない場合、既定では WebFrontEnd エンドになります。<br /><br /> ApplicationServer: サービスをホストするサーバーを表します。<br /><br /> WebFrontEnd エンド: Web サイトをホストするサーバーについて説明します。|
|[ソリューション内の項目]|パッケージに追加できるすべての SharePoint プロジェクト項目およびフィーチャーを表します。|
|[パッケージ内の項目]|省略可能。 パッケージ内の配置対象の SharePoint プロジェクト項目およびフィーチャーを表します。|

## <a name="configure-the-packaging-process"></a>パッケージ化プロセスを構成する
 Visual Studio で SharePoint ソリューションを開発した後に、プロジェクトをパッケージ化する方法をカスタマイズすることができます。

 次の表は、 *.wsp* ファイルの作成方法をカスタマイズするために使用できる2つの MSBuild ターゲットを示しています。

|Target|説明|
|------------|-----------------|
|BeforeLayout|ファイルが中間ディレクトリにコピーされる直前にタスクを実行するターゲット。 パッケージファイル (*.wsp*) を作成する前に、ファイルを変更することができます。|
|AfterLayout|ファイルが中間ディレクトリにコピーされた直後にタスクを実行するターゲット。|

 詳細については、「 [方法: MSBuild ターゲットを使用して SharePoint ソリューションパッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)」を参照してください。

## <a name="packaging-architecture"></a>パッケージ化アーキテクチャ
 次の手順は、Visual Studio で SharePoint パッケージ (*.wsp*) を作成するときに発生します。

1. パッケージの物理構造と意味構造が正しいことを確認するために、フィーチャーおよびパッケージが検証されます。

2. パッケージ内のフィーチャー、プロジェクト項目、およびパッケージ ファイルが列挙されます。 パッケージおよびフィーチャーのマニフェスト ファイルが変換されて、配置およびアクティブ化に必要な情報がすべて追加されます。 トークンは完全修飾値に置き換えられます。

3. カスタマイズ可能な BeforeLayout MSBuild ターゲットが実行されます。 このステップを作成すると、 *.wsp* ファイルを作成する前に、パッケージにカスタム変更を加えることができます。

4. 列挙されたファイルが中間ディレクトリにコピーされます。

5. カスタマイズ可能な AfterLayout MSBuild ターゲットが実行されます。 このステップを作成すると、 *.wsp* ファイルを作成する前に、パッケージにカスタム変更を加えることができます。

6. 中間ディレクトリ内のファイルは、 *.wsp* ファイルに追加されます。

## <a name="package-folder-structure"></a>パッケージ フォルダーの構造
 SharePoint プロジェクトをパッケージ化すると、 *solutionfolder\bin \\ \<BuildConfiguration>* フォルダーに *.wsp* ファイルが作成されます。 たとえば、ソリューションが *C:\ Visual studio 2013 \ プロジェクト \ listdefinition1* にあり、ビルド構成が [リリース] に設定されている場合、 *.Wsp* ファイルは *C:\ visual studio 2013 \ Projects\ListDefinition1\bin\Release* にあります。

## <a name="see-also"></a>関連項目
- [方法: SharePoint ソリューションパッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package.md)
- [方法: パッケージデザイナーを使用してパッケージに機能と項目を追加および削除する](../sharepoint/how-to-add-and-remove-features-and-items-to-a-package-by-using-the-package-designer.md)
- [方法: MSBuild タスクを使用して SharePoint ソリューションパッケージを作成する](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)
- [方法: MSBuild タスクを使用して SharePoint ソリューションパッケージを作成する](../sharepoint/how-to-create-a-sharepoint-solution-package-by-using-msbuild-tasks.md)
- [方法: MSBuild ターゲットを使用して SharePoint ソリューションパッケージをカスタマイズする](../sharepoint/how-to-customize-a-sharepoint-solution-package-by-using-msbuild-targets.md)
