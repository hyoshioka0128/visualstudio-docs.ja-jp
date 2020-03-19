---
title: 'DA0030: データベース プロジェクトの階層の相互作用の測定を収集します。 | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.DA0030
- vs.performance.rules.DA0030
- vs.performance.30
ms.assetid: 42b2f69d-0cfa-4854-82c4-589c3d8b4557
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 26b0905882ef8ec2e3fcddc4cf699ecae7dbe7a4
ms.sourcegitcommit: cc841df335d1d22d281871fe41e74238d2fc52a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/18/2020
ms.locfileid: "74777477"
---
# <a name="da0030-gather-tier-interaction-measurements-for-database-projects"></a>DA0030: データベース プロジェクトの階層相互作用の測定値を収集します

|||
|-|-|
|規則 ID|DA0030|
|カテゴリ|プロファイリング ツールの使用|
|プロファイル方法|サンプリング|
|[メッセージ]|多層アプリケーションの相互作用の測定値を収集すると、データベースの使用パターンと重要なデータのアクセス遅延を知ることができます。 階層の相互作用のプロファイル オプションを有効にして、再度アプリケーションのプロファイリングを試みてください。|
|規則の種類|情報|

## <a name="cause"></a>原因
 <xref:System.Data> メソッドの呼び出しがプロファイル データの大きな割合を占めているため、プロファイリングの実行中に階層の相互作用データが収集されませんでした。 プロファイリングを再度実行し、階層の相互作用データを追加することを検討してください。

## <a name="rule-description"></a>規則の説明
 この規則は、System.Data 名前空間 (<xref:System.Data.Linq><xref:System.Data.Linq> を含む) に常駐する関数内で、重要なアクティビティが発生するたびに適用されます。

 多階層アプリケーションは、アプリケーションのプレゼンテーションとデータ レイヤー用に複数層のサービスを使用します。 多くの場合、データ レイヤーは、Microsoft SQL Server などのデータベース管理システムを実行する独立したプロセスです。 データ レイヤーは、個別のコンピューター上でアプリケーションの途中から実行することもできます。 サンプリング プロファイルの場合、アウトプロセスまたはリモートで実行されるサービスや関数の内部まで詳しく確認することはできません。

 プロファイリング ツールで ADO.NET サービスへの非同期呼び出しを使用すると、Microsoft SQL Server のデータ レイヤーとの対話を行う多階層アプリケーションのタイミング情報を収集できます。 その場合、[階層の相互作用のプロファイルを有効にする] オプションを有効にする必要があります。 このオプションは、既定ではオフになっています。

## <a name="how-to-fix-violations"></a>違反の修正方法
 この規則は情報提供用であるため、是正措置は必要ない場合があります。

 Visual Studio IDE から階層の相互作用データをプロファイル データに追加する方法については、「[階層相互作用データを収集する](../profiling/collecting-tier-interaction-data.md)」を参照してください。 コマンド ラインから階層の相互作用データを追加する方法については、「[階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md)」を参照してください。
