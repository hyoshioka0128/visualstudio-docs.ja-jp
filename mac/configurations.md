---
title: ビルド構成について
description: この記事では、Visual Studio for Mac のさまざまなビルド構成について説明します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 09/18/2019
ms.assetid: 78107CFA-9308-4293-A92A-9B552A259E15
ms.openlocfilehash: d1511434a34017a7f0f7da65fe1ea6956d45d497
ms.sourcegitcommit: 2975d722a6d6e45f7887b05e9b526e91cffb0bcf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2020
ms.locfileid: "71128396"
---
# <a name="understanding-build-configurations"></a>ビルド構成について

開発プロセス中、さまざまなビルドに使用できるように、ソリューションとプロジェクトのプロパティからなるさまざまな構成を保存できます。 テンプレートを利用し、Visual Studio for Mac で作成されたプロジェクトには通常、アプリのデバッグとアプリのデプロイをそれぞれサポートする、デバッグ構成とリリース構成が含まれています。 

カスタム構成を作成する場合、「[ビルド構成の作成と編集](/visualstudio/mac/create-and-edit-configurations)」を参照してください。

>[!NOTE]
>このトピックは、Visual Studio for Mac に適用されます。 Windows での Visual Studio については、「[ビルド構成について](/visualstudio/ide/understanding-build-configurations)」を参照してください。

## <a name="solution-configurations"></a>ソリューション構成

ソリューション構成は、ソリューション内のすべてのプロジェクトの構成を指定するために使用されます。 **[ビルド]、[構成]** 、 **[構成マッピング]** タブの順に選択し、開いているソリューションで項目ごとにターゲット構成を割り当てることができます。 次の画像で確認できます。

![構成マッピング オプション](media/projects-and-solutions-image3.png)

構成の詳細については、James Montemagno の [Configuration Manager](https://www.youtube.com/watch?v=tjSdkqYh5Vg) の動画をご覧ください。

## <a name="project-build-configurations"></a>プロジェクトのビルド構成

プロジェクトには複数の構成が与えられる傾向があります。 プロジェクトが対象とする構成とプラット フォームは、プロジェクトのビルド時に使用されるプロパティを指定するために一緒に使用されます。 構成を切り替えることで、ビルド時に異なる出力が可能になります。 たとえば、デバッグ構成を選択すると、デバッグ シンボルが出力されるので、デバッガーは関数名、パラメーター、変数をクラッシュしたアプリケーションのスタック トレースから解決できます。 開発時にはこのような追加情報が役に立ちますが、ファイル サイズが膨大になるため、配布には適していません。

各プラットフォームには、そのビルドに固有の構成があります。 プロジェクトのビルド構成ページには、 **[プロジェクト オプション]** ダイアログで **[ビルド]** セクションに移動することでアクセスできます。 このダイアログを開くには、プロジェクトを右クリックし、 **[オプション]** を選択するか、ソリューション エクスプローラーでプロジェクトをダブルクリックします。

## <a name="run-configuration"></a>実行構成

Visual Studio for Mac では、_実行構成_を設定できます。 実行構成は、下の画像のように、ツール バーのビルド構成選択の隣にあるドロップダウンで提示されます。

![実行構成ドロップダウン](media/projects-and-solutions-image8.png)

実行構成は、一連の実行オプション、名前、さまざまな目的でプロジェクトに定義されるいくつかの構成からなります。 実行構成はプロジェクト レベルで定義されます。デフォルトは実行可能プロジェクトごとに自動的に作成されます。ただし、必要な数だけ追加できます。 プロジェクトの種類によっては、追加の実行構成が自動的に生成されます。 たとえば、watchOS プロジェクトの場合、_グランス構成と通知構成_が生成されることがあります。

構成は他の開発者と共有したり (この場合、構成は .csproj ファイルに保存)、ローカル保存したり (この場合、構成は .user ファイルに保存) することができます。

### <a name="android-run-configurations"></a>Android 実行構成

Android プロジェクトの実行構成では、プロジェクトの実行時またはデバッグ時に起動する特定のアクティビティ、サービス、ブロードキャスト レシーバーを指定できます。 さまざまな起動条件下でコンポーネントをテストするために、インテント エクストラ データを渡し、インテント フラグを設定できます。

`MainLauncher` 以外のアクティビティの場合、物理デバイスでデバッグするために、アクティビティ属性に `Exported=true` を追加しておく必要があります。あるいは、インテント フィルターを定義しておきます。

## <a name="examples-of-data-that-might-be-included-in-run-configurations"></a>実行構成に含まれるデータの例

次の一覧は、実行構成に含まれることがあるデータ例です。

* 通常の .NET プロジェクト
  * 代替スタートアップ アプリ
  * 引数の開始
  * 作業ディレクトリ
  * 環境変数
  * Mono ランタイム オプション (Mono で実行時のみ使用)
* Android プロジェクト
  * エントリ ポイント (アクティビティ、サービス、レシーバー)
  * インテント引数とデータ
* iOS プロジェクト
  * モード (通常、バック グラウンド フェッチ)
* iOS 拡張プロジェクト
  * スタートアップ アプリ: デフォルトまたはカスタム
* WatchKit プロジェクト
  * モード (グランス、通知)
  * 通知ペイロード

## <a name="see-also"></a>参照

- [ビルド構成について (Windows の Visual Studio)](/visualstudio/ide/understanding-build-configurations)
