---
title: '方法: サービスのトラブルシューティング |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: troubleshooting
helpviewer_keywords:
- services, troubleshooting
ms.assetid: 001551da-4847-4f59-a0b2-fcd327d7f5ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 588396f3f152222c4e79b03a1d733524a8ff3ca9
ms.sourcegitcommit: 05487d286ed891a04196aacd965870e2ceaadb68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85905723"
---
# <a name="how-to-troubleshoot-services"></a>方法: サービスのトラブルシューティング
サービスを取得しようとすると、いくつかの一般的な問題が発生する可能性があります。

- サービスはに登録されていません [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。

- サービスは、サービスの種類ではなく、インターフェイスの種類によって要求されます。

- サービスを要求している VSPackage が配置されていません。

- 間違ったサービスプロバイダーが使用されています。

  要求されたサービスを取得できない場合、を呼び出すと <xref:Microsoft.VisualStudio.Shell.Package.GetService%2A> null が返されます。 サービスを要求した後、必ず null をテストする必要があります。

```csharp
IVsActivityLog log =
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="to-troubleshoot-a-service"></a>サービスのトラブルシューティングを行うには

1. システムレジストリを調べて、サービスが正しく登録されているかどうかを確認します。 詳細については、「[方法: サービスを提供する](../extensibility/how-to-provide-a-service.md)」を参照してください。

    次の *.reg*ファイルフラグメントは、SVsTextManager サービスを登録する方法を示しています。

   ```
   [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\<version number>\Services\{F5E7E71D-1401-11d1-883B-0000F87579D2}]
   @="{F5E7E720-1401-11d1-883B-0000F87579D2}"
   "Name"="SVsTextManager"
   ```

    上記の例では、バージョン番号は12.0 や14.0 などののバージョンです [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。キー {F5E7E71D-1401-11d1-883B-0000F87579D2} はサービスのサービス識別子 (SID)、SVsTextManager、既定値 {F5E7E720-1401-11d1-883B-0000F87579D2} は、サービスを提供するテキストマネージャー VSPackage のパッケージ GUID です (既定値 {})。

2. GetService を呼び出すときは、インターフェイスの種類ではなくサービスの種類を使用します。 からサービスを要求するときに [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 、 <xref:Microsoft.VisualStudio.Shell.Package> 型から GUID を抽出します。 次の条件が存在する場合、サービスは見つかりません。

   1. インターフェイス型は、サービス型ではなく、GetService に渡されます。

   2. インターフェイスに明示的に割り当てられている GUID はありません。 そのため、必要に応じて、システムによってオブジェクトの既定の GUID が作成されます。

3. サービスを要求している VSPackage が配置されていることを確認してください。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]サイトを構築した後、を呼び出す前に VSPackage し <xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A> ます。

    サービスを必要とする VSPackage コンストラクターにコードがある場合は、それをメソッドに移動し `Initialize` ます。

4. 正しいサービスプロバイダーを使用していることを確認してください。

    すべてのサービスプロバイダーが似ているわけではありません。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]ツールウィンドウに渡すサービスプロバイダーは、VSPackage に渡されるものとは異なります。 ツールウィンドウサービスプロバイダーはを認識し <xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection> ますが、については理解していません <xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable> 。 を呼び出して、 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> ツールウィンドウ内から VSPackage service プロバイダーを取得できます。

    ツールウィンドウがユーザーコントロールまたはその他のコントロールコンテナーをホストしている場合、コンテナーは Windows コンポーネントモデルによって配置され、どのサービスにもアクセスできません [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 。 を呼び出して、 <xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A> コントロールコンテナー内から VSPackage service プロバイダーを取得できます。

## <a name="see-also"></a>関連項目
- [利用可能なサービスの一覧](../extensibility/internals/list-of-available-services.md)
- [サービスを使用して提供する](../extensibility/using-and-providing-services.md)
- [サービスの基本事項](../extensibility/internals/service-essentials.md)
