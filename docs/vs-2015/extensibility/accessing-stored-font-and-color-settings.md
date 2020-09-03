---
title: 格納されているフォントと色の設定にアクセスする |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- fonts, accessing stored settings
- font and color control [Visual Studio SDK], persistence
- colors, accessing stored settings
ms.assetid: beba7174-e787-45c2-b6ff-a60f67ad4998
caps.latest.revision: 27
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fbb2f118d903eae2124e705f14c7aa7b51bf9c4d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "67821836"
---
# <a name="accessing-stored-font-and-color-settings"></a>格納されたフォントと色の設定へのアクセス
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[vsprvs](../includes/vsprvs-md.md)]統合開発環境 (IDE: integrated development environment) には、フォントおよび色の変更された設定がレジストリに保存されます。 インターフェイスを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> これらの設定にアクセスできます。  
  
## <a name="to-initiate-state-persistence-of-fonts-and-colors"></a>フォントおよび色の状態の永続化を開始するには  
 フォントおよび色の情報は、次のレジストリの場所にカテゴリ別に格納されています: [HKCU\SOFTWARE\Microsoft]、[Visual Studio \\ *\<Visual Studio version>* ]、[色]。ここで、 \\ *\<CategoryGUID>* *\<CategoryGUID>* はカテゴリ GUID です。  
  
 したがって、永続化を開始するには、VSPackage で次のことを行う必要があります。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>グローバルサービスプロバイダーに対してを呼び出すことによって、インターフェイスを取得 `QueryService` します。  
  
     `QueryService` は、のサービス ID 引数 `SID_SVsFontAndColorStorage` とのインターフェイス ID 引数を使用して呼び出す必要があり `IID_IVsFontAndColorStorage` ます。  
  
- <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.OpenCategory%2A>カテゴリの GUID とモードフラグを引数として使用して、永続化するカテゴリを開くには、メソッドを使用します。  
  
  引数で指定されたモードは、 `fFlags` 列挙体の値から構築され <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS> ます。 このモードは、次のことを制御します。  

  - インターフェイスを使用してアクセスできる設定 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 。  

  - すべての設定、またはユーザーが変更したすべての設定またはインターフェイスで取得可能な <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> 。  

  - ユーザー設定に変更を反映する方法。  

  - 使用される色の値の形式。  

## <a name="to-use-state-persistence-of-fonts-and-colors"></a>フォントおよび色の状態の永続化を使用するには  
 フォントと色の保持には次のものが含まれます。  
  
- IDE 設定とレジストリに格納されている設定との同期。  
  
- レジストリの変更情報を伝達しています。  
  
- レジストリに格納されている設定の設定および取得。  
  
  ストレージ設定と IDE 設定の同期は、ほぼ透過的です。 基になる IDE は、 **表示項目** の更新された設定をカテゴリのレジストリエントリに自動的に書き込みます。  
  
  複数の Vspackage が特定のカテゴリを共有する場合、VSPackage は、インターフェイスのメソッドを使用して格納されている <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> レジストリ設定を変更するときに、イベントを生成する必要があります。  
  
  既定では、イベント生成は有効になっていません。 イベントの生成を有効にするには、を使用してカテゴリを開く必要があり <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS> ます。 これにより、IDE は VSPackage が実装する適切なメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorEvents> ます。  
  
> [!NOTE]
> [ **フォントおよび色** ] プロパティページを使用して変更すると、に依存しないイベントが生成さ <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> れます。 インターフェイスを使用すると、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorCacheManager> クラスのメソッドを呼び出す前に、キャッシュされたフォントと色の設定を更新する必要があるかどうかを判断でき <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> ます。  
  
### <a name="storing-and-retrieving-information"></a>情報の格納と取得  
 開いているカテゴリの名前付き表示項目に対してユーザーが変更できる情報を取得または構成するには、Vspackage <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> メソッドとメソッドを呼び出し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.SetItem%2A> ます。  
  
 特定のカテゴリのフォント属性に関する情報は、メソッドとメソッドを使用して取得し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.SetFont%2A> ます。  
  
> [!NOTE]
> この `fFlags` カテゴリが開かれたときにメソッドに渡される引数は、メソッド <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.OpenCategory%2A> とメソッドの動作を定義し <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> ます。 既定では、これらのメソッドは、変更された表示 itemsthat 関する情報のみを返します。 ただし、フラグを使用してカテゴリが開かれている場合、 <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS> 更新された表示項目と変更されていない表示項目は、およびでアクセスでき <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> ます。  
  
 既定では、変更された **表示項目** の情報だけがレジストリに保持されます。 インターフェイスを使用して、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage> フォントおよび色のすべての設定を取得することはできません。  
  
> [!NOTE]
> <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetItem%2A>メソッドとメソッドは、 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage.GetFont%2A> 変更されていない**表示項目**に関する情報を取得するために使用するときに、REGDB_E_KEYMISSING、(0x80040152L) を返します。  
  
 特定の**カテゴリ**のすべての**表示項目**の設定は、インターフェイスのメソッドを使用して取得でき `T:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorDefaults` ます。  
  
## <a name="see-also"></a>参照  
 <xref:Microsoft.VisualStudio.Shell.Interop.IVsFontAndColorStorage>   
 <xref:Microsoft.VisualStudio.Shell.Interop.__FCSTORAGEFLAGS>   
 [カスタム カテゴリと表示項目の実装](../extensibility/implementing-custom-categories-and-display-items.md)
