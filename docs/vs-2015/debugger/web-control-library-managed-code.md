---
title: Web コントロールライブラリ (マネージコード) |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging DLLs
- debugging [Visual Studio], Web control libraries
ms.assetid: 2413883f-9e88-406d-b874-0ed743b75d40
caps.latest.revision: 29
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 031f894eb2e117a213f4f9fbbf08ac57a1512d61
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65688176"
---
# <a name="web-control-library-managed-code"></a>Web コントロール ライブラリ (マネージド コード)
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Web コントロール ライブラリ プロジェクト テンプレートは DLL を作成します。 クラス ライブラリは DLL であるため、直接実行することはできません。 コントロールを埋め込む [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ページを作成する必要があります。 詳細については、「 [Web コントロールライブラリのテンプレート](https://msdn.microsoft.com/00666b07-71d2-4ace-a13c-cc130a3ce372)」を参照してください。  
  
### <a name="to-debug-a-web-control-library-method-1"></a>Web コントロール ライブラリをデバッグするには (方法 1)  
  
1. 既存の Web コントロール ライブラリ プロジェクトを開くか、新しいプロジェクトを作成します。  
  
2. コントロールを埋め込む [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] ページを作成します。  
  
3. [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] テスト ハーネスをホストしている Web サイトで、`/Code` という名前のサブディレクトリを作成します。  
  
4. コントロールのソース コードを `/Code` サブディレクトリにコピーします。  
  
5. `/Code` サブディレクトリでソース コードを開き、ブレークポイントを設定します。  
  
6. テスト ハーネスを指す URL を使用してブラウザー ウィンドウを開きます。 コントロール内のブレークポイントにヒットすると、デバッグを開始できます。  
  
### <a name="to-debug-a-web-control-library-method-2"></a>Web コントロールライブラリをデバッグするには (メソッド 2)  
  
1. ホスト アプリケーション プロジェクトと Web コントロール プロジェクトを同じソリューションで作成します。  
  
2. **ソリューションエクスプローラー**で、ホストアプリケーションを右クリックし、[**参照の追加**] を選択します。  
  
3. Web コントロール プロジェクトへの参照を追加します。  
  
## <a name="see-also"></a>参照  
 [ASP.NET Web アプリケーション](../debugger/debugging-preparation-aspnet-web-applications.md)
