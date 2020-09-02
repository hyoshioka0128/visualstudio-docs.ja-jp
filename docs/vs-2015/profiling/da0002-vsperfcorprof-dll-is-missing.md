---
title: 'DA0002: VSPerfCorProf.dll がありません | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.DA0002
- vs.performance.2
- vs.performance.rules.DAVsPerfCorProfMissing
- vs.performance.rules.DA0002
ms.assetid: 76e614b3-ad7e-4b92-b7be-88dc1329be1d
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5723506415a0ddbf816b896e23e93eaa706bf7e7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158725"
---
# <a name="da0002-vsperfcorprofdll-is-missing"></a>DA0002:VSPerfCorProf.dll がありません
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ルール Id |DA0002 |  
|Category |プロファイルツール使用法 |  
|プロファイル方法 |VSPerfCmd および VSPerfASPNETCmd コマンドラインツールを使用したプロファイリング |  
|Message |VSPerfCLREnv で環境変数を正しく設定しないと、ファイルが収集されたように見えます。 マネージド バイナリのシンボルを解決できません。|  
|ルールの種類 |情報 |  
  
## <a name="cause"></a>原因  
 プロファイラーは、プロファイリング実行中、VSPerfCorProf.dll を見つけることができませんでした。 プロファイラー データを集めるためのコマンドライン ツールが VSPerfCLREnv.cmd ツールで必要な環境変数を初期化することなく使用されたとき、この警告が発生します。 プロファイリング ツールの開始時に別のプロファイラーが実行されていた場合にもこの警告は発生します。  
  
## <a name="rule-description"></a>ルールの説明  
 プロファイラーのプロファイリング実行で .NET Framework バイナリのシンボルを解決するには、特定の環境変数を設定する必要があります。 この警告が示唆することは、プロファイリング データが集められる前に VSPerfCLREnv.cmd ツールが実行されなかったということです。 マネージド バイナリのシンボルを解決できないことがあります。 コマンドラインからのプロファイルツールの使用方法の詳細については、「[コマンドラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)」を参照してください。  
  
## <a name="how-to-fix-violations"></a>違反の修正方法  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイリング ツールのコマンドライン ツールを利用してマネージド アプリケーションをプロファイリングするとき、データの収集を開始する前に [VSPerfCLREnv](../profiling/vsperfclrenv.md) コマンドライン ツールを実行します。
