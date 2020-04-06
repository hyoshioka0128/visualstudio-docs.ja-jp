---
title: '方法 : サービスのトラブルシューティング |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- services, troubleshooting
ms.assetid: 001551da-4847-4f59-a0b2-fcd327d7f5ca
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 49560acdf57f5dad2c57f2a8e4649f194d6d8298
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80710749"
---
# <a name="how-to-troubleshoot-services"></a>方法: サービスのトラブルシューティングを行う
サービスを取得するときに発生する可能性のある一般的な問題がいくつかあります。

- サービスは に[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]登録されていません。

- サービスは、サービスの種類ではなく、インターフェイスの種類によって要求されます。

- サービスを要求する VSPackage がサイト化されていません。

- 間違ったサービス プロバイダが使用されています。

  要求されたサービスを取得できない場合、呼び出<xref:Microsoft.VisualStudio.Shell.Package.GetService%2A>しは null を返します。 サービスを要求した後は、常に null をテストする必要があります。

```csharp
IVsActivityLog log =
    GetService(typeof(SVsActivityLog)) as IVsActivityLog;
if (log == null) return;
```

## <a name="to-troubleshoot-a-service"></a>サービスのトラブルシューティングを行うには

1. システム レジストリを調べて、サービスが正しく登録されているかどうかを確認します。 詳細については、「[方法 : サービスを提供する](../extensibility/how-to-provide-a-service.md)」を参照してください。

    次の *.reg*ファイルの一部は、SVsTextManager サービスの登録方法を示しています。

   ```
   [HKEY_LOCAL_MACHINE\Software\Microsoft\VisualStudio\<version number>\Services\{F5E7E71D-1401-11d1-883B-0000F87579D2}]
   @="{F5E7E720-1401-11d1-883B-0000F87579D2}"
   "Name"="SVsTextManager"
   ```

    上記の例では、バージョン番号は[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]12.0 または 14.0 などの バージョンであり、{F5E7E71D-1401-11d1-883B-0000F87579D} はサービスのサービス識別子 (SID) です。 SVsTextManager と既定値 {F5E7E720-1401-11d1-883B-0000F87579D} は、サービスを提供するテキスト マネージャー VSPackage のパッケージ GUID です。

2. GetService を呼び出すときは、インターフェイスの種類ではなく、サービスの種類を使用します。 から[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]サービスを要求する場合<xref:Microsoft.VisualStudio.Shell.Package>、GUID を型から抽出します。 次の条件が存在する場合、サービスは見つかりません。

   1. インターフェイスの型は、サービスの種類ではなく GetService に渡されます。

   2. インターフェイスに明示的に割り当てられた GUID はありません。 したがって、システムは、必要に応じて、オブジェクトの既定の GUID を作成します。

3. サービスを要求する VSPackage がサイト化されていることを確認します。 [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]を構築した後、呼び出す<xref:Microsoft.VisualStudio.Shell.Package.Initialize%2A>前に VSPackage をサイトします。

    VSPackage コンストラクターにサービスを必要とするコードがある場合は、そのコードをメソッド`Initialize`に移動します。

4. 正しいサービス プロバイダーを使用していることを確認します。

    すべてのサービス プロバイダーが同じではありません。 ツール ウィンドウに[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]渡すサービス プロバイダーは、VSPackage に渡すものとは異なります。 ツール ウィンドウ サービス プロバイダ<xref:Microsoft.VisualStudio.Shell.Interop.STrackSelection>は について知っていますが<xref:Microsoft.VisualStudio.Shell.Interop.SVsRunningDocumentTable>、についてはわかりません。 ツール ウィンドウ<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>内から VSPackage サービス プロバイダーを取得する呼び出しできます。

    ツール ウィンドウがユーザー コントロールまたはその他のコントロール コンテナーをホストしている場合、コンテナーは Windows コンポーネント モデルによって配置され、どのサービス[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)]にもアクセスできません。 コントロール コンテナー<xref:Microsoft.VisualStudio.Shell.Package.GetGlobalService%2A>内から VSPackage サービス プロバイダーを取得する呼び出しできます。

## <a name="see-also"></a>関連項目
- [利用可能なサービスの一覧](../extensibility/internals/list-of-available-services.md)
- [サービスの使用と提供](../extensibility/using-and-providing-services.md)
- [サービスの必需品](../extensibility/internals/service-essentials.md)
