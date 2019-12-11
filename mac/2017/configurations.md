---
title: ビルド構成について
description: この記事では、Visual Studio for Mac のさまざまなビルド構成について説明します。
author: heiligerdankgesang
ms.author: dominicn
ms.date: 04/14/2017
ms.assetid: 78107CFA-9308-4293-A92A-9B552A259E15
ms.openlocfilehash: 0bd35d415a60ea64c479b19cb506c58c2c346cc0
ms.sourcegitcommit: 370cc7fd2e11ede6d8215c8d81963a8307614550
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/10/2019
ms.locfileid: "74983595"
---
# <a name="understanding-build-configurations"></a>ビルド構成について

## <a name="project-build-configurations"></a>プロジェクトのビルド構成

多くの場合、プロジェクトには複数の構成があり、ビルド時に構成を切り替えてさまざまな出力を実行できます。 たとえば、デバッグ構成を選択すると、デバッグ シンボルが出力されるので、デバッガーは関数名、パラメーター、変数をクラッシュしたアプリケーションのスタック トレースから解決できます。 開発時にはこのような追加情報が役に立ちますが、ファイル サイズが膨大になるため、配布には適していません。

各プラットフォームには、そのビルドに固有の構成があります。

## <a name="solution-configurations"></a>ソリューション構成

プロジェクト構成のように、ソリューション構成も、プロジェクト全体に対してカスタム構成を作成するために使用されます。 次の画像のように、 **[ビルド]、[構成]** 、 **[構成マッピング]** タブの順に選択し、各ソリューション項目のターゲット構成を割り当てることができます。

![構成マッピング オプション](media/projects-and-solutions-image3.png)

構成の詳細については、James Montemagno の [Configuration Manager](https://www.youtube.com/watch?v=tjSdkqYh5Vg) の動画をご覧ください。

## <a name="run-configuration"></a>構成の実行

以前のバージョンの Xamarin Studio では、**スタートアップ プロジェクト**としてプロジェクトを設定するオプションを選択できました。これは、グローバルの実行/デバッグ コマンドの利用時に実行/デバッグされるプロジェクトです。 これは、プロジェクト パッドでプロジェクト名に対して太字で示されていました。

Visual Studio for Mac では、スタートアップ プロジェクトを設定する代わりに、_実行構成_を設定できます。 実行構成は、下の画像のように、ツール バーのビルド構成選択の隣にあるドロップダウンで提示されます。

![実行構成ドロップダウン](media/projects-and-solutions-image8.png)

実行構成は、一連の実行オプション、名前、さまざまな目的でプロジェクトに定義されるいくつかの構成からなります。 実行構成はプロジェクト レベルで定義されます。デフォルトは実行可能プロジェクトごとに自動的に作成されます。ただし、必要な数だけ追加できます。 プロジェクトの種類によっては、追加の実行構成が自動的に生成されます。 たとえば、watchOS プロジェクトの場合、_グランス構成と通知構成_が生成されることがあります。

構成は他の開発者と共有したり (この場合、構成は .csproj ファイルに保存)、ローカル保存したり (この場合、構成は .user ファイルに保存) することができます。

### <a name="android-run-configurations"></a>Android 実行構成

Android プロジェクトの実行構成では、プロジェクトの実行時またはデバッグ時に起動するアクティビティ、サービス、ブロードキャスト レシーバーを指定できます。 さまざまな起動条件下でコンポーネントをテストできるように、インテント エクストラ データを渡し、インテント フラグを設定できます。

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

## <a name="see-also"></a>関連項目

- [ビルド構成について (Windows の Visual Studio)](/visualstudio/ide/understanding-build-configurations)
