---
title: Visual Studio 2017 での設計向けの新機能
titleSuffix: ''
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- what's new [Visual Studio], architecture and modeling
- architecture [Visual Studio], modeling
- modeling software [Visual Studio], What's New
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.workload:
- multiple
monikerRange: vs-2017
ms.openlocfilehash: 6f81cc32604abe6d90ac0d263574e97df35c63bd
ms.sourcegitcommit: 95f26af1da51d4c83ae78adcb7372b32364d8a2b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79301495"
---
# <a name="whats-new-for-design-in-visual-studio-2017"></a>Visual Studio 2017 での設計向けの新機能

## <a name="live-dependency-validation"></a>ライブ依存関係の検証

不要な依存関係を削除することは、技術的な負債を管理する上で重要な部分です。 Visual Studio では、依存関係の場所など、問題に関する正確な情報を含む、依存関係のライブ検証が提供されます。 ライブ依存関係の検証では、エラー一覧とエディターの新機能を最大限に活用できます。

![ライブ依存関係の検証が行われる](media/dep-validation-whatsnew-01.png)

オーサリングエクスペリエンスが変更され、依存関係の検証がより見やすく、アクセスしやすくなっています。 用語が「レイヤー図」から「依存図」に変更されました。

**アーキテクチャ**メニューには、依存関係図を直接作成するコマンドが含まれています。

![[アーキテクチャ] メニューのライブ依存関係項目](media/dep-validation-whatsnew-02.png)

レイヤー プロパティの名前と説明は、よりわかりやすいように変更されました。

![ライブ依存関係更新されたプロパティ名](media/dep-validation-whatsnew-03.png)

ダイアグラムを保存するたびに、ソリューション内の現在のコードの解析結果に変更が反映された場合の影響がすぐにわかります。 **[依存関係の検証**] コマンドが完了するまで待つ必要はありません。

詳しくは、[このブログ投稿](https://devblogs.microsoft.com/devops/live-architecture-dependency-validation-in-visual-studio-15-preview-5/)をご覧ください。

## <a name="uml-designers-have-been-removed"></a>UML デザイナが削除されました

UML デザイナーは、Visual Studio から削除されました。

* UML 図が XML ファイルとして表示されるようになりました
* UML モデル エクスプローラーが存在しなくなりました
* プロジェクト参照のモデリングは依存関係の検証に使用されなくなりました
* ソリューション エクスプローラーの [レイヤー参照] ノードが表示されなくなった
* 依存関係 (レイヤー) 図の "検証" ビルド アクションが使用されなくなりました - ビルド タスクが削除されました
* プロジェクト構造はバージョン間のラウンドトリップのために維持されます。
* 依存関係 (レイヤー) ダイアグラムを XML として開き、作成、編集、および保存できます。
* 依存関係 (レイヤー) 図にリンクされた TFS 作業項目は、デザイン サーフェイスでアクセスできません。
* DSL またはレイヤへのバック リンクはサポートされなくなりました
* モデリング SDK での UML 拡張はサポートされなくなりました。

.NET および C++ コードのアーキテクチャの視覚化のサポートは、[コード マップ](map-dependencies-across-your-solutions.md)を通じて利用できます。

UML デザイナーの重要なユーザーであれば、UML のニーズに合った代替ツールを決定しながら、Visual Studio 2015 以前のバージョンを引き続き使用できます。

詳しくは、[このブログ投稿](https://devblogs.microsoft.com/devops/uml-designers-have-been-removed-layer-designer-now-supports-live-architectural-analysis/)をご覧ください。

[!INCLUDE[modeling_sdk_info](includes/modeling_sdk_info.md)]

## <a name="edition-support-for-architecture-and-modeling-tools"></a><a name="VersionSupport" />アーキテクチャとモデリング ツールのエディションサポート

Visual Studio はいくつかのエディションで使用できます。 これらのすべてが、アーキテクチャとモデリング ツールをサポートするわけではありません。 各ツールの利用可能情報を次の表に示します。

|**機能**|**エンタープライズエディション**|**プロフェッショナル版**|**コミュニティ版**|
|-|-|-|-|
|**コード マップ**|はい|コード マップの読み取り、コード マップのフィルター処理、新しいジェネリック ノードの追加、選択項目からの新しい有向グラフの作成のみをサポートします。|-|
|**依存関係図**|はい|依存関係図の読み取りのみをサポートします。|依存関係図の読み取りのみをサポートします。|
|**有向グラフ**(DGML 図)|はい|はい|はい|
|**コードクローン**|はい|-|-|
