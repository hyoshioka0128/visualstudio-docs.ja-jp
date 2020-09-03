---
title: レイヤー図の拡張機能のトラブルシューティング |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-modeling
ms.topic: troubleshooting
helpviewer_keywords:
- layer diagrams, extension errors
- layer diagrams, troubleshooting extensions
ms.assetid: 1fda4f8a-38b8-482b-87b8-eade1a4e5662
caps.latest.revision: 27
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: dd4560673259373b68b370e73a43de424fb7bdb7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "72658478"
---
# <a name="troubleshoot-extensions-for-layer-diagrams"></a>レイヤー図の拡張機能のトラブルシューティング
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このトピックでは、レイヤー モデル拡張機能を作成するときに発生する可能性のある問題について説明します。

#### <a name="when-i-press-f5-to-debug-my-extension-my-commands-gesture-handlers-validation-extensions-or-custom-properties-do-not-appear-on-layer-diagrams-in-the-experimental-instance-of-vsprvs"></a>F5 キーを押して拡張機能をデバッグするとき、コマンド、ジェスチャ ハンドラー、検証拡張機能、またはカスタム プロパティが、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスのレイヤー図に表示されない

1. の実験用インスタンスで拡張機能ソリューションを開き、[ [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **ビルド** ] メニューの [ **ソリューションのリビルド**] をクリックします。

2. **F5**キーまたは CTRL キーを押し**ながら f5**キーを押して、の実験用インスタンスを開始し [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] ます。 レイヤー図を開き、拡張機能をテストします。

   必要に応じて、次の手順に進みます。

#### <a name="an-old-version-of-my-extension-runs"></a>拡張機能の古いバージョンが実行る

1. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の実験用インスタンスが実行していないことを確認します。

2. 次のフォルダーを削除します:%LocalAppData%\Microsoft\VisualStudio \\ [バージョン]、componentmodelcache

   > [!NOTE]
   > % LocalAppData% は通常、 *DriveName*: \ Users \\ *UserName*\appdata\local です。

   必要に応じて、次の手順に進みます。

#### <a name="an-old-version-of-my-validation-results-appears-or-my-validation-method-is-not-called"></a>古いバージョンの検証結果が表示される、または検証メソッドが呼び出されない

1. の実験用インスタンスで、 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] [ **ビルド** ] メニューの [ **ソリューションのクリーン**] をクリックします。 これにより、前に行った検証分析のキャッシュされている結果がクリアされます。

2. モデルのレイヤーがコード要素と関連付けられていること、および少なくとも 1 つの依存関係リンクがモデルに存在することを確認します。 検証する項目がない場合、検証は呼び出されません。

3. 検証メソッドは別のプロセスで実行するので、標準のブレークポイントは検証メソッドでは機能しない場合があります。 メソッドをステップ実行する場合は、`System.Diagnostics.Debugger.Launch()` の呼び出しを挿入する必要があります。

4. レイヤー検証プロジェクトの **source.extension.vsixmanifest** で、 **MEF コンポーネント** 項目と **カスタム拡張機能の種類** の両方の項目を [ **コンテンツ**] の下に追加したことを確認します。

## <a name="see-also"></a>参照
 [レイヤー図を拡張する](../modeling/extend-layer-diagrams.md)
