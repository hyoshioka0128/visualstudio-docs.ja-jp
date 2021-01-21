---
title: IDE 内からのビルドの開始 | Microsoft Docs
description: Microsoft.VisualStudio.Shell.Interop.IVsBuildManagerAccessor を使用して、カスタム プロジェクト システムのビルドを開始する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- build
ms.assetid: 936317aa-63b7-4eb0-b9db-b260a0306196
author: ghogen
ms.author: ghogen
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 5e0447cae810da48bd592371a40f22c40ff45cec
ms.sourcegitcommit: 1a36533f385e50c05f661f440380fda6386ed3c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/30/2020
ms.locfileid: "93048161"
---
# <a name="start-a-build-from-within-the-ide"></a>IDE 内からのビルドの開始

カスタムのプロジェクト システムでは、<xref:Microsoft.VisualStudio.Shell.Interop.IVsBuildManagerAccessor> を使用してビルドを開始する必要があります。 この記事では、この要件の理由とプロシージャの概要について説明します。

## <a name="parallel-builds-and-threads"></a>並行ビルドとスレッド

 Visual Studio では並行ビルドを使用できます。これは共通リソースにアクセスするための仲介を必要とします。 プロジェクト システムではビルドを非同期的に実行できますが、このようなシステムでは、コールバック内からビルド関数を呼び出すことはできません。

 プロジェクト システムで環境変数を変更する場合は、ビルドの NodeAffinity を OutOfProc に設定する必要があります。 この要件は、インプロセス ノードを必要とするためホスト オブジェクトを使用できないことを意味します。

## <a name="use-ivsbuildmanageraccessor"></a>IVSBuildManagerAccessor を使用する

 次のコードは、ビルドを開始するためにプロジェクト システムで使用できるメソッドの概要を示しています。

```csharp

public bool Build(Project project, bool isDesignTimeBuild)
{
    // Get the accessor from the IServiceProvider interface for the
    // project system
    IVsBuildManagerAccessor accessor =
        serviceProvider.GetService(typeof(SVsBuildManagerAccessor)) as
        IVsBuildManagerAccessor;
    bool releaseUIThread = false;
    try
    {
        if(accessor != null)
        {
            // Claim the UI thread under the following conditions:
            // 1. The build must use a resource that uses the UI thread
            // or,
            // 2. The build requires the in-proc node AND waits on the
            // UI thread for the build to complete
            if(NeedsUIThread)
            {
                int result = accessor.ClaimUIThreadForBuild();
                if(result != S_OK)
                {
                     // Not allowed to claim the UI thread right now
                     return false;
                }
                releaseUIThread = true;
             }
             if(isDesignTimeBuild)
             {
// Start the design time build
                  int result = accessor.BeginDesignTimeBuild();
                  if(result != S_OK)
                  {
                      // Not allowed to begin a design-time build at
                      // this time. Try again later.
                      return false;
                  }
             }
         }
         bool buildSucceeded = false;
         // perform project-system specific build set up tasks
         // Create your BuildRequestData
         // This assumes a IHostServices variable (hostServices) set
   // to your host services. If you don't use a project instance
         // (you build from a file for example) then use another
         // constructor.
         BuildRequestData requestData = new
             BuildRequestData(project.CreateProjectInstance(),
             "myTarget", hostServices,
             BuildRequestData.BuildRequestDataFlags.None);
         // Mark your your submission as Pending
         BuildSubmission submission =
              BuildManager.DefaultBuildManager.
              PendBuildRequest(requestData);
         // Register the loggers in BuildLoggers
         if (accessor != null)
         {
               foreach (ILogger logger in BuildLoggers)
               {
                    accessor.RegisterLogger(submission.SubmissionId,
                        logger);
               }
         }
         BuildResult buildResult = submission.Execute();
         return buildResult;
     }
     // Clean up resources
     finally
     {
         if(accessor != null)
         {
             // Unregister the loggers, if necessary.
             accessor.UnregisterLoggers(submission.SubmissionId);
             // Release the UI thread, if used
             if(releaseUIThread)
             {
                  accessor.ReleaseUIThreadForBuild();
             }
             // End the design time build, if used
             if(isDesignTimeBuild)
             {
                  accessor.EndDesignTimeBuild();
             }
         }
     }
}
```
