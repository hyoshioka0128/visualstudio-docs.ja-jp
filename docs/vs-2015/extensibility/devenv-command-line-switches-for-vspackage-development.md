---
title: VSPackage Development の Devenv コマンドラインスイッチ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- /setup command line switch
- /resetskippkgs command line switch
- /noVSIP command line switch
- /rootsuffix command line switch
- command-line switches
- registry, Visual Studio SDK
- command line, switches
- Visual Studio SDK, command-line switches
ms.assetid: d65d2c04-dd84-42b0-b956-555b11f5a645
caps.latest.revision: 17
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 97ce429a7140d7b95393c2dcb8b34491b3adfefa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68185278"
---
# <a name="devenv-command-line-switches-for-vspackage-development"></a>VSPackage 開発の Devenv コマンド ライン スイッチ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 開発者が Visual Studio 統合開発環境 (IDE: integrated development environment) を起動するファイル devenv.exe を実行するときに、コマンドラインからタスクを自動化できるようにします。  
  
 タスクには次のものがあります。  
  
- IDE の外部からデザイン済みの構成でアプリケーションを配置する。  
  
- 事前設定されたビルド設定またはデバッグ構成を使用してプロジェクトを自動的にビルドします。  
  
- Ide を特定の構成で読み込みます。すべて IDE の外部からです。 また、起動時に IDE をカスタマイズすることもできます。  
  
## <a name="guidelines-for-switches"></a>スイッチのガイドライン  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ドキュメントでは、ユーザーレベルの devenv コマンドラインスイッチについて説明します。 詳細については、「 [Devenv コマンドラインスイッチ](../ide/reference/devenv-command-line-switches.md)」を参照してください。 Devenv では、VSPackage の開発、配置、およびデバッグに役立つその他のコマンドラインスイッチもサポートされています。  
  
|コマンドラインスイッチ|説明|  
|--------------------------|-----------------|  
|/safemode|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]セーフモードで起動し、既定の IDE とサービスのみを読み込みます。 /セーフスイッチは、の起動時にすべてのサードパーティ Vspackage が読み込まれないようにして [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 、安定した実行を保証します。<br /><br /> このスイッチは引数を取りません。|  
|/resetskippkgs|問題のある Vspackage の読み込みを避ける必要があるユーザーによって追加されたスキップ読み込みオプションをすべてクリアしてから、を開始 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] します。 SkipLoading タグが存在すると、VSPackage の読み込みが無効になります。 タグをクリアすると、VSPackage の読み込みが再度有効になります。<br /><br /> このスイッチは引数を取りません。|  
|/rootsuffix|[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]別の場所を使用して開始します。 次のコマンドは、インストーラーによって作成されたショートカットによって実行され [!INCLUDE[vsipsdk](../includes/vsipsdk-md.md)] ます。<br /><br /> devenv/rootsuffix exp<br /><br /> この場合、exp は、10.0 ではなく 10.0 Exp など、特定のサフィックスを持つ場所を識別します。 実験用インスタンスを使用すると、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] コードの記述に使用しているのインスタンスとは別に VSPackage をデバッグできます。<br /><br /> このスイッチは、VSRegEx.exe を使用して作成した場所を識別する任意の文字列を受け取ることができます。 詳細については、 [実験用インスタンス](../extensibility/the-experimental-instance.md)を参照してください。|  
|/スプラッシュ|スプラッシュスクリーンを通常どおりに表示し、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] メイン IDE を表示する前にメッセージボックスを表示します。 このメッセージボックスを使用すると、スプラッシュスクリーンを調べて、VSPackage 製品アイコンがあるかどうかを確認できます。<br /><br /> このスイッチは引数を取りません。|  
  
## <a name="see-also"></a>参照  
 [コマンドラインスイッチの追加](../extensibility/adding-command-line-switches.md)   
 [Devenv コマンドラインスイッチ](../ide/reference/devenv-command-line-switches.md)
