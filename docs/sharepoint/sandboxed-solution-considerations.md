---
title: サンドボックスソリューションに関する考慮事項 |Microsoft Docs
description: サイトコレクションユーザーが独自のカスタムコードソリューションをアップロードできるようにする、Microsoft SharePoint の機能であるサンドボックスソリューションについて説明します。
ms.custom: SEO-VS-2020
ms.date: 02/02/2017
ms.topic: conceptual
f1_keywords:
- VS.SharePointTools.Project.SandboxedSolutions
- VS.SharePointTools.Security.SandboxedSolutions
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- SharePoint development in Visual Studio, sandboxed solutions
- sandboxed solutions [SharePoint development in Visual Studio]
- SharePoint development in Visual Studio, farm solutions
- farm solutions [SharePoint development in Visual Studio]
author: John-Hart
ms.author: johnhart
manager: jillfra
ms.workload:
- office
ms.openlocfilehash: 17b310a3f992f80b04ad14bb6e038e05b009a4af
ms.sourcegitcommit: 02f14db142dce68d084dcb0a19ca41a16f5bccff
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/23/2020
ms.locfileid: "95970463"
---
# <a name="sandboxed-solution-considerations"></a>サンドボックス ソリューションの考慮事項
  *サンドボックスソリューション* は、Microsoft SharePoint 2010 の機能であり、サイトコレクションユーザーが独自のカスタムコードソリューションをアップロードできるようにします。 一般的なサンドボックスソリューションは、ユーザーが独自の Web パーツをアップロードすることです。

 サンドボックス化された SharePoint アプリケーションは、Web ファームの限られた部分にアクセスできる、セキュリティで保護された監視対象のプロセスで実行されます。 Microsoft SharePoint 2010 では、機能、ソリューションギャラリー、ソリューションの監視、検証フレームワークの組み合わせを使用して、サンドボックスソリューションを有効にします。

## <a name="specify-project-trust-level"></a>プロジェクトの信頼レベルを指定する
 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)]*サンドボックスソリューション* と呼ばれるブール型のプロジェクトプロパティを使用して、サンドボックスソリューションをサポートします。 このプロパティは、プロジェクトでいつでも設定できます。また、 **SharePoint カスタマイズウィザード** でプロジェクトを作成するときに指定することもできます。

> [!NOTE]
> プロジェクトの作成後に *サンドボックスソリューション* プロパティを変更すると、検証エラーが発生する可能性があります。

 *サンドボックスソリューション* プロパティが **false** に設定されている場合、または [**ファームソリューションとして配置**] オプションを選択した場合、このソリューションはファームスコープのソリューションと見なされます。 ただし、 *サンドボックスソリューション* プロパティが **true** に設定されている場合、またはウィザードで [ **サンドボックスソリューションとして展開** する] オプションを選択した場合、このソリューションはファームソリューションとは異なる方法で処理されます。

## <a name="sharepoint-site-hierarchy"></a>SharePoint サイト階層
 サンドボックスソリューションのしくみを理解するには、SharePoint サイトがスコープ内に階層化されていることを把握しておくと役に立ちます。 最上位の要素は Web ファームと呼ばれ、他の要素は下位にあります。

 Web ファーム

 Web アプリケーション A

 サイトコレクション A1

 サイト A1a

 Web アプリケーション B

 サイトコレクション B1

 サイト B1a

 サイト B1b

 サイトコレクション B2

 サイト B2a

 ご覧のように、Web ファームには1つ以上の Web アプリケーションを含めることができ、さらに、サブサイトを持つことができる1つ以上のサイトコレクションを含めることができます。 1つのサイトコレクションに加えられた変更は、そのサイトコレクションにのみ影響し、それ以外は影響を与えません。 ただし、Web ファームレベルで行われた変更は、ファーム上のすべてのサイトコレクションに影響します。

 Windows SharePoint Services (WSS) 3.0 では、ファームレベルにのみソリューションを配置できますが、 [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] ファームレベル (ファームソリューション) またはサイトコレクションレベル (サンドボックスソリューション) のいずれかに配置できます。

## <a name="why-sandboxed-solutions"></a>サンドボックスソリューションの理由
 WSS 3.0 では、ソリューションをファームレベルにのみ配置できます。 これは、Web ファーム全体およびその下で実行される他のすべてのサイトコレクションとアプリケーションに影響を与える可能性のある、有害または安定性のソリューションを展開できることを意味します。 ただし、サンドボックスソリューションを使用すると、特定のサイトコレクションであるファームのサブエリアにソリューションを配置できます。 追加の保護を提供するために、ソリューションのアセンブリはメイン [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] プロセス (*w3wp.exe*) に読み込まれません。 代わりに、別のプロセス (*SPUCWorkerProcess.exe*) に読み込まれます。 このプロセスは監視され、クォータと調整を実装して、CPU サイクルを消費する短いループの実行など、有害なアクティビティを実行するサンドボックスソリューションからファームを保護します。

## <a name="site-collection-solution-gallery"></a>サイトコレクションソリューションギャラリー
 [!INCLUDE[sharepointShort](../sharepoint/includes/sharepointshort-md.md)] 2010には、"サイトコレクションソリューションギャラリー" と呼ばれる機能があります。 この機能にアクセスするには、SharePoint 2010 サーバーの全体管理ページを開くか、[**サイトの操作**] メニューを開き、[サイトの **設定**] をクリックしてから、Sharepoint サイトの [**ギャラリー** ] の下にある [**ソリューション**] リンクを選択します。 ソリューションギャラリーは、サイトコレクションの管理者がサイトコレクション内のソリューションを管理できるようにするソリューションのリポジトリです。

 ソリューションギャラリーは、SharePoint サイトのルート Web に格納されているドキュメントライブラリです。 ソリューションギャラリーによって、サイトテンプレートが置き換えられ、ソリューションパッケージがサポートされます。 SharePoint ソリューションパッケージ (*.wsp*) ファイルがアップロードされると、サンドボックスソリューションとして処理されます。

## <a name="sandboxed-solution-limitations"></a>サンドボックスソリューションの制限事項
 サンドボックスソリューションが配置されている場合は、使用できる SharePoint 機能の配列が制限されているため、セキュリティ上の脆弱性を減らすことができます。 これらの制限事項には、次のようなものがあります。

- サンドボックスソリューションには、使用できる配置可能なソリューション要素のサブセットが制限されています。 サイト定義やワークフローなど、脆弱である可能性のある SharePoint プロジェクトテンプレートは使用できません。

- SharePoint では、メイン ** [!INCLUDE[TLA2#tla_iis5](../sharepoint/includes/tla2sharptla-iis5-md.md)] アプリケーションプール (*w3wp.exe*) プロセスとは別のプロセス (SPUCWorkerProcess.exe) で、サンドボックス化されたソリューションコードを実行します。

- マップされたフォルダーをプロジェクトに追加することはできません。

- アセンブリ内の型は、 [!INCLUDE[moss_14_long](../sharepoint/includes/moss-14-long-md.md)] サンドボックスソリューションでは使用できません。 また、アセンブリ Microsoft SharePoint 内の型のみを [!INCLUDE[wss_14_long](../sharepoint/includes/wss-14-long-md.md)] サンドボックスソリューションで使用できます。

  Sharepoint ソリューションをサンドボックスソリューションとして指定しても、SharePoint サーバーには影響しないことに注意してください。sharepoint プロジェクトを SharePoint に配置する方法 [!INCLUDE[vsprvs](../sharepoint/includes/vsprvs-md.md)] とバインド先のアセンブリを指定するだけです。 生成された *.wsp* ファイルには影響しません。また、 *.wsp* ファイルには、 *サンドボックスソリューション* プロパティに直接関連付けられたデータがありません。

## <a name="capabilities-and-elements-in-sandboxed-solutions"></a>サンドボックスソリューションの機能と要素
 サンドボックスソリューションは、次の機能と要素をサポートします。

- コンテンツの種類/フィールド

- カスタム アクション

- 宣言型のワークフロー

- イベント レシーバー

- 機能のコールアウト

- List Definitions

- インスタンスの一覧表示

- モジュール/ファイル

- ナビゲーション

- *Onet.xml*

- SPItemEventReceiver

- SPListEventReceiver

- SPWebEventReceiver

- から派生するすべての Web パーツのサポート `System.Web.UI.WebControls.WebParts.WebPart`

- Web パーツ

- WebTemplate 機能要素 ( *Webtemp.xml* ではなく)

- Visual Web パーツ

  サンドボックスソリューションは、次の機能と要素をサポートしていません。

- アプリケーション ページ

- カスタムアクショングループ

- ファームスコープの機能

- `HideCustomAction` 要素

- Web アプリケーションスコープの機能

- ワークフローとコード

## <a name="see-also"></a>関連項目
- [サンドボックスソリューションとファームソリューションの違い](../sharepoint/differences-between-sandboxed-and-farm-solutions.md)
- [SharePoint ソリューションの開発](../sharepoint/developing-sharepoint-solutions.md)
