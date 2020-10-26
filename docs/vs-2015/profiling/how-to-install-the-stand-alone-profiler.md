---
title: '方法: スタンドアロンのプロファイラーをインストールする | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- performance tools, installing stand-alone profiler
- profiling tools, stand-alone profiler
ms.assetid: cae81c95-83cd-4ab6-8a98-84ef977a2f6d
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 026162a2c8334c7163f9c7853d2de30e58e5939a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "77476783"
---
# <a name="how-to-install-the-stand-alone-profiler"></a>方法 : スタンドアロンのプロファイラーをインストールする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] では、[!INCLUDE[vsprvs](../includes/vsprvs-md.md)] IDE をインストールしなくても実行できるコマンドライン ベースのスタンドアロン プロファイラーを利用できます。 このような状況は、コンピューターに開発環境がインストールされていないときに発生します。 たとえば、本稼働中の Web サーバーには開発環境をインストールするべきではありません。  
  
> [!NOTE]
> スタンドアロン プロファイラーを利用し、ASP.NET Web サイトのパフォーマンス データを集めるときは、[VSPerfCmd](../profiling/vsperfcmd.md) ツールよりも [VSPerfASPNetCmd](../profiling/vsperfaspnetcmd.md) ライン ツールをお勧めします。  
  
### <a name="to-install-the-stand-alone-profiler"></a>スタンドアロンのプロファイラーをインストールするには  
  
1. \Standalone Profiler パスが含まれるディレクトリの [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] インストール メディアでスタンドアロン プロファイル インストーラー (vs_profiler.exe) を見つけて実行します。  
  
2. vsintr.exe と msdis150.dll のパスをシステム パスに追加します。  
  
    > [!NOTE]
    > [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] の既定のインストールでは、vsinstr.exe と msdis150.dll は \Program Files\Visual Studio 10\Team Tools\Performance Tools にあります。  
  
3. コマンド プロンプトで、「**VSInstr**」と入力します。  
  
    > [!NOTE]
    > vsinstr.exe の利用状況情報が表示された場合、すべてが正しく設定されています。 vsinstr.exe またはその依存関係の 1 つが見つからないというエラーが表示された場合、手順 2 のとおりにパスが正しく設定されていることを確認してください。  
  
4. **_NT_SYMBOL_PATH**変数をに設定して、シンボルサーバーを設定します。`symsrv*symsrv.dll*c:\localcache*https://msdl.microsoft.com/download/symbols`  
  
5. システム環境変数を利用してシンボル サーバーを設定したら、新しいコマンド プロンプトでコマンドライン プロファイラー ツールを実行します。 実行後、新しい環境変数が適用されます。 [コマンド プロンプト] ウィンドウで、次のコマンド ラインを入力します。  
  
     **start %COMSPEC%**  
  
    > [!NOTE]
    > シンボルサーバーパッケージを設定する方法の詳細については、「 [方法: Windows シンボル情報を参照](../profiling/how-to-reference-windows-symbol-information.md)する」を参照してください。  
  
6. [VSPerfReport](../profiling/vsperfreport.md) ツールを利用し、シンボルをシリアル化してプロファイリング データ ファイル (.vsp) を生成します。 **VSPerfReport /summary:all /packsymbols** スイッチを使用します。 データ ファイルにシンボルが挿入されていない場合、_NT_SYMBOL_PATH 環境変数が設定されていることを確認します。  
  
## <a name="see-also"></a>参照  
 [コマンドラインからのプロファイリング](../profiling/using-the-profiling-tools-from-the-command-line.md)   
 [チュートリアル: サンプリングを使用したコマンドラインプロファイリング](../profiling/walkthrough-command-line-profiling-using-sampling.md)   
 [チュートリアル: インストルメンテーションを使用したコマンドラインプロファイリング](../profiling/walkthrough-command-line-profiling-using-instrumentation.md)   
 [方法: Windows シンボル情報を参照する](../profiling/how-to-reference-windows-symbol-information.md)   
 [VSPerfReport](../profiling/vsperfreport.md)
