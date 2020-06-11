---
title: MSBuild でのビルド ログの取得 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, logging
- logging [MSBuild]
ms.assetid: 6ba9a754-9cc0-4fed-9fc8-4dcd3926a031
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 8210ceeb26c3350822d95f85af7689a37894dba9
ms.sourcegitcommit: d20ce855461c240ac5eee0fcfe373f166b4a04a9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/29/2020
ms.locfileid: "84184056"
---
# <a name="obtain-build-logs-with-msbuild"></a>MSBuild でのビルド ログの取得

MSBuild でスイッチを使用することで、確認するビルド データの量とビルド データを 1 つ以上のファイルに保存するかどうかを指定できます。 カスタム ロガーを指定して、ビルド データを収集することもできます。 このトピックで説明されていない MSBuild コマンド ライン スイッチの詳細については、「[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)」を参照してください。

> [!NOTE]
> Visual Studio IDE を使用してプロジェクトをビルドする場合は、ビルド ログを確認することで、それらのビルドをトラブルシューティングできます。 詳細については、[ビルド ログ ファイルを表示、保存、および構成する](../ide/how-to-view-save-and-configure-build-log-files.md)」をご覧ください。

## <a name="set-the-level-of-detail"></a>詳細レベルを設定する

 詳細レベルを指定せずに MSBuild を使用して、プロジェクトをビルドすると、出力ログに次の情報が表示されます。

- 重要度 - 高として分類されたエラー、警告、メッセージ。

- 一部の状態イベント。

- ビルドの概要。

**-verbosity** ( **-v**) スイッチを使用して、出力ログに表示するデータ量を制御できます。 トラブルシューティングを行う場合は、`detailed` (`d`) または `diagnostic` (`diag`) のいずれかの詳細レベルを使用します。後者は情報が最も多くなります。

**-verbosity** を `detailed` に設定すると、ビルド処理は遅くなることがあります。また、 **-verbosity** を `diagnostic` に設定するとさらに遅くなる可能性があります。

```cmd
msbuild MyProject.proj -t:go -v:diag
```

### <a name="verbosity-settings"></a>詳細度の設定

次の表では、ログの詳細度 (列の値) が、ログに記録されるメッセージの種類 (行の値) に与える影響を示します。

|                                       | 静的 | Minimal | 標準 | 詳細 | 診断 |
|---------------------------------------|:-----:|:-------:|:------:|:--------:|:----------:|
| エラー                                |   ✅   |    ✅    |    ✅   |     ✅    |      ✅     |
| 警告                              |   ✅   |    ✅    |    ✅   |     ✅    |      ✅     |
| 高重要度のメッセージ              |       |    ✅    |    ✅   |     ✅    |      ✅     |
| 通常の重要度のメッセージ           |       |         |    ✅   |     ✅    |      ✅     |
| 低重要度のメッセージ              |       |         |        |     ✅    |      ✅     |
| MSBuild エンジンの追加情報 |       |         |        |          |      ✅     |

## <a name="save-the-build-log-to-a-file"></a>ビルド ログをファイルに保存する

**-fileLogger** (**fl**) スイッチを使用して、ビルド データをファイルに保存することができます。 次の例では、ビルド データを *msbuild.log* という名前のファイルに保存します。

```cmd
msbuild MyProject.proj -t:go -fileLogger
```

 次の例では、ログ ファイルに *MyProjectOutput.log* という名前を付けて、ログ出力の詳細度を `diagnostic` に設定しています。 **-fileLoggerParameters** (`flp`) スイッチを使用して、これら 2 つの設定を指定します。

```cmd
msbuild MyProject.proj -t:go -fl -flp:logfile=MyProjectOutput.log;verbosity=diagnostic
```

 詳細については、「[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)」を参照してください。

## <a name="save-the-log-output-to-multiple-files"></a>ログ出力を複数のファイルに保存する

 次の例では、ログ全体を *msbuild1.log* に、エラーのみを *JustErrors.log* に、警告のみを *JustWarnings.log* に保存します。 例では、3 つのファイルのそれぞれを表すファイル番号を使用します。 ファイル番号は、 **-fl** スイッチと **-flp** スイッチの直後に指定されています (`-fl1` と `-flp1` など)。

 ファイル 2 とファイル 3 の **-fileLoggerParameters** (`flp`) スイッチは、各ファイルの名前と各ファイルに含まれる内容を指定します。 ファイル 1 には名前が指定されていないため、既定の名前である *msbuild1.log* が使用されます。

```cmd
msbuild MyProject.proj -t:go -fl1 -fl2 -fl3 -flp2:logfile=JustErrors.log;errorsonly -flp3:logfile=JustWarnings.log;warningsonly
```

 詳細については、「[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)」を参照してください。

## <a name="save-a-binary-log"></a>バイナリ ログを保存する

**-binaryLogger** (**bl**) スイッチを利用すれば、ログを圧縮されたバイナリ形式で保存できます。 このログには、ビルド プロセスの詳しい説明が含まれ、特定のログ分析ツールで読み取ることができます。

次の例では、バイナリ ログ ファイルが *binarylogfilename* という名前で作成されます。

```cmd
-bl:binarylogfilename.binlog
```

詳細については、「[コマンド ライン リファレンス](../msbuild/msbuild-command-line-reference.md)」を参照してください。

## <a name="use-a-custom-logger"></a>カスタム ロガーを使用する

 <xref:Microsoft.Build.Framework.ILogger> インターフェイスを実装するマネージド型を記述することにより、独自のロガーを作成できます。 たとえば、カスタム ロガーを使用して、ビルド エラーをメールで送信する、データベースにログを記録する、または XML ファイルにログを記録することができます。 詳細については、「[ビルド ロガー](../msbuild/build-loggers.md)」を参照してください。

 MSBuild コマンドラインでは、 **-logger** スイッチを使用してカスタム ロガーを指定します。 また、 **-noconsolelogger** スイッチを使用して、既定のコンソール ロガーを無効にすることもできます。

## <a name="see-also"></a>関連項目

- <xref:Microsoft.Build.Framework.LoggerVerbosity>
- [ビルド ロガー](../msbuild/build-loggers.md)
- [マルチプロセッサ環境でのログ](../msbuild/logging-in-a-multi-processor-environment.md)
- [転送 logger の作成](../msbuild/creating-forwarding-loggers.md)
- [MSBuild の概念](../msbuild/msbuild-concepts.md)
