---
title: '方法: アクティビティログを使用する |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- VSPackages, debugging
- VSPackages, troubleshooting
ms.assetid: bb3d3322-0e5e-4dd5-b93a-24d5fbcd2ffd
caps.latest.revision: 30
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: d450e02d23159f186fd85bf1b687a2fb2c18e82a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842100"
---
# <a name="how-to-use-the-activity-log"></a>方法: アクティビティ ログを使用する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Vspackage は、アクティビティログにメッセージを書き込むことができます。 この機能は、小売環境で Vspackage をデバッグする場合に特に便利です。  
  
> [!TIP]
> アクティビティログは常にオンになっています。 Visual Studio では、最後の100エントリと、一般的な構成情報を持つ最初の10個のエントリのローリングバッファーが保持されます。  
  
### <a name="to-write-an-entry-to-the-activity-log"></a>アクティビティログにエントリを書き込むには  
  
1. このコード <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> は、VSPackage コンストラクターを除く、メソッドまたは他の任意のメソッドに挿入します。  
  
    ```csharp  
    IVsActivityLog log = GetService(typeof(SVsActivityLog)) as IVsActivityLog;  
    if (log == null) return;  
  
    int hr = log.LogEntry((UInt32)__ACTIVITYLOG_ENTRYTYPE.ALE_INFORMATION,  
        this.ToString(),  
        string.Format(CultureInfo.CurrentCulture,  
        "Called for: {0}", this.ToString()));  
    ```  
  
     このコードは、 <xref:Microsoft.VisualStudio.Shell.Interop.SVsActivityLog> サービスを取得し、それをインターフェイスにキャストし <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog> ます。 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog.LogEntry%2A> 現在のカルチャコンテキストを使用して、情報エントリをアクティビティログに書き込みます。  
  
2. VSPackage が読み込まれると (通常はコマンドが呼び出されたとき、またはウィンドウが開かれたときに)、テキストがアクティビティログに書き込まれます。  
  
### <a name="to-examine-the-activity-log"></a>アクティビティログを確認するには  
  
1. Visual Studio data: *% AppData%* \Microsoft\VisualStudio\14.0\ActivityLog.XML. のサブフォルダーでアクティビティログを探します。  
  
2. 任意のテキストエディターを使用して、アクティビティログを開きます。 一般的なエントリは次のとおりです。  
  
    ```  
    Called for: Company.MyApp.MyAppPackage ...  
    ```  
  
## <a name="robust-programming"></a>信頼性の高いプログラミング  
 アクティビティログはサービスであるため、アクティビティログは VSPackage コンストラクターでは使用できません。  
  
 書き込みの直前にアクティビティログを取得する必要があります。 将来使用するために、アクティビティログをキャッシュまたは保存しないでください。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsActivityLog>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__ACTIVITYLOG_ENTRYTYPE>   
 [Vspackage のトラブルシューティング](../extensibility/troubleshooting-vspackages.md)   
 [VSPackages](../extensibility/internals/vspackages.md)
