---
title: テキストの色付けに使用するフォントと色の情報を取得する |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- text, coloring
- font and color control [Visual Studio SDK], coloring
ms.assetid: d1f985bd-743e-40b7-9458-d9af53647c91
caps.latest.revision: 23
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 8724c31accb26e478c2726dfe791256994fc95ca
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65696856"
---
# <a name="getting-font-and-color-information-for-text-colorization"></a>テキストに色づけするためのフォントと色の情報の取得
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ユーザーインターフェイス (UI) 要素で色分けされたテキストを表示または表示するプロセスは、プロジェクトの種類、テクノロジ、および開発者の設定によって異なります。 [ **フォントおよび色** ] プロパティページには、設定が格納されます。  
  
 色分けされたテキストを表示するほとんどの実装では、 `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults` テキスト表示設定の表示、取得、および格納に関連するインターフェイスが必要です。  
  
> [!NOTE]
> ( **テキスト EditorCategory**をサポートする) コアエディターをカスタマイズする場合は、言語サービスでカラーリングテクノロジを使用することを強くお勧めします。 詳細については、「 [フォントと色の概要](../extensibility/font-and-color-overview.md)」を参照してください。  
  
## <a name="getting-default-font-and-color-information"></a>既定のフォントと色の情報を取得する  
 テキストを表示するウィンドウのすべての**フォントと色**の設定は、1つの**カテゴリ**の**表示項目**で指定する必要があります。 詳細については、「[ [フォントおよび色] ([オプション] ダイアログボックス](../ide/reference/fonts-and-colors-environment-options-dialog-box.md)-[環境])」を参照してください。  
  
 色を色分けするには、VSPackage が現在の **フォントと色** の設定を取得する必要があります。 VSPackage は、必要に応じて次の方法でこれを実現できます。  
  
- フォントと色の永続化メカニズムを使用して、格納されている状態または現在の状態を取得します。 詳細については、「 [格納されているフォントおよび色の設定へのアクセス](../extensibility/accessing-stored-font-and-color-settings.md)」を参照してください。  
  
- フォントおよびカラー <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider> データを提供するサービスのインターフェイスを使用して、のインスタンスを取得し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults> ます。これは、VSPackage がフォントおよびカラープロバイダーでもない場合に使用します。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> インターフェイスを実装します。  
  
  ポーリングによって取得された結果が最新の状態であることを確認するために、インターフェイスを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> インターフェイスの取得メソッドを呼び出す前に更新が必要かどうかを判断すると便利な場合があり <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> ます。  
  
  フォントおよび色の情報を取得した後、表示されるテキストを解析して、色付けが必要な要素を識別し、適切なフォントと色を使用してウィンドウ内のテキストを表示します。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaultsProvider>   
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults>   
 [フォントとテキストの使用](https://msdn.microsoft.com/library/d43640f3-da94-4df2-a29d-a9d021a1c069)   
 [色の操作](https://msdn.microsoft.com/library/d34ff96f-241d-494f-abdd-13811ada8cd3)   
 [GDI (グラフィックスデバイスインターフェイス)](https://msdn.microsoft.com/7e1d4540-bb2e-4257-8eee-eee376acba83)
