---
title: MSBuild でのビルド ログの取得 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: msbuild
ms.topic: conceptual
helpviewer_keywords:
- MSBuild, logging
- logging [MSBuild]
ms.assetid: 6ba9a754-9cc0-4fed-9fc8-4dcd3926a031
caps.latest.revision: 30
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: c88288a7bed453ca14e9c14fd43706b97be04044
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841509"
---
# <a name="obtaining-build-logs-with-msbuild"></a>MSBuild でのビルド ログの取得
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

MSBuild でスイッチを使用することで、確認するビルド データの量とビルド データを 1 つ以上のファイルに保存するかどうかを指定できます。 カスタム ロガーを指定して、ビルド データを収集することもできます。 このトピックで説明されていない MSBuild コマンドラインスイッチの詳細については、「 [コマンドラインリファレンス](../msbuild/msbuild-command-line-reference.md)」を参照してください。  
  
> [!NOTE]
> Visual Studio IDE を使用してプロジェクトをビルドする場合は、ビルド ログを確認することで、それらのビルドをトラブルシューティングできます。 詳細については、[ビルド ログ ファイルを表示、保存、および構成する](../ide/how-to-view-save-and-configure-build-log-files.md)」を参照してください。  
  
## <a name="setting-the-level-of-detail"></a>詳細レベルを設定する  
 詳細レベルを指定せずに MSBuild を使用して、プロジェクトをビルドすると、出力ログに次の情報が表示されます。  
  
- 重要度 - 高として分類されたエラー、警告、メッセージ。  
  
- 一部の状態イベント。  
  
- ビルドの概要。  
  
  **/Verbosity** (**/v**) スイッチを使用すると、出力ログに表示されるデータ量を制御できます。 トラブルシューティングを行う場合は、`detailed` (`d`) または `diagnostic` (`diag`) のいずれかの詳細レベルを使用します。後者は情報が最も多くなります。  
  
  **/Verbosity**をに設定し、 `detailed` **/verbosity**をに設定すると、ビルドプロセスが遅くなることがあり `diagnostic` ます。  
  
```  
msbuild MyProject.proj /t:go /v:diag  
```  
  
## <a name="saving-the-build-log-to-a-file"></a>ビルド ログをファイルに保存する  
 **/FileLogger** (**fl**) スイッチを使用して、ビルドデータをファイルに保存できます。 次の例では、ビルド データを `msbuild.log` という名前のファイルに保存します。  
  
```  
msbuild MyProject.proj /t:go /fileLogger  
```  
  
 次の例では、ログ ファイルに `MyProjectOutput.log` という名前を付けて、ログ出力の詳細度を `diagnostic` に設定しています。 これらの2つの設定は、 **/filelogparameters** () スイッチを使用して指定し `flp` ます。  
  
```  
msbuild MyProject.proj /t:go /fl /flp:logfile=MyProjectOutput.log;verbosity=diagnostic  
```  
  
 詳細については、「 [コマンドラインリファレンス](../msbuild/msbuild-command-line-reference.md)」を参照してください。  
  
## <a name="saving-the-log-output-to-multiple-files"></a>ログ出力を複数のファイルに保存する  
 次の例では、ログ全体を `msbuild1.log` に、エラーのみを `JustErrors.log` に、警告のみを `JustWarnings.log` に保存します。 例では、3 つのファイルのそれぞれを表すファイル番号を使用します。 ファイル番号は、/ **fl** スイッチと **/flp** スイッチの直後に指定されます (たとえば、 `/fl1` や `/flp1` )。  
  
 ファイル **/filelogparameters** `flp` 2 とファイル3の/filelogparameters () スイッチは、各ファイルの名前を指定し、各ファイルに含める内容を指定します。 ファイル 1 には名前が指定されていないため、既定の名前である `msbuild1.log` が使用されます。  
  
```  
msbuild MyProject.proj /t:go /fl1 /fl2 /fl3 /flp2:logfile=JustErrors.log;errorsonly /flp3:logfile=JustWarnings.log;warningsonly  
  
```  
  
 詳細については、「 [コマンドラインリファレンス](../msbuild/msbuild-command-line-reference.md)」を参照してください。  
  
## <a name="using-a-custom-logger"></a>カスタム ロガーを使用する  
 <xref:Microsoft.Build.Framework.ILogger> インターフェイスを実装するマネージド型を記述することにより、独自のロガーを作成できます。 たとえば、カスタム ロガーを使用して、ビルド エラーをメールで送信する、データベースにログを記録する、または XML ファイルにログを記録することができます。 詳細については、「 [ビルドロガー](../msbuild/build-loggers.md)」を参照してください。  
  
 MSBuild コマンドラインで、 **/ロガー** スイッチを使用してカスタムロガーを指定します。 **/Noconsolelogger**スイッチを使用して、既定のコンソールロガーを無効にすることもできます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.Build.Framework.LoggerVerbosity>   
 [ビルドロガー](../msbuild/build-loggers.md)   
 [マルチプロセッサ環境でのログ記録](../msbuild/logging-in-a-multi-processor-environment.md)   
 [転送 Logger の作成](../msbuild/creating-forwarding-loggers.md)   
 [MSBuild の概念](../msbuild/msbuild-concepts.md)
