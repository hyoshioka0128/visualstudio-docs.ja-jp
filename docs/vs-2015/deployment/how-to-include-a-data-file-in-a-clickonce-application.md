---
title: '方法: ClickOnce アプリケーションにデータファイルを含める |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-deployment
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- ClickOnce deployment, data
- deploying applications [ClickOnce], data files
- data access, ClickOnce applications
ms.assetid: 89ee46ef-bc8c-4ab0-a2ac-1220f9da06fc
caps.latest.revision: 17
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 9120a5b3cb60f6c607ed97ab2df24bb157c72371
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153766"
---
# <a name="how-to-include-a-data-file-in-a-clickonce-application"></a>方法 : ClickOnce アプリケーションにデータ ファイルを含める
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]インストールする各アプリケーションには、対象のコンピューターのローカルディスクにデータディレクトリが割り当てられます。このディレクトリには、アプリケーションが独自のデータを管理できます。 データファイルには、任意の種類のファイル (テキストファイル、XML ファイル、または Microsoft Access データベース (.mdb) ファイルなど) を含めることができます。 次の手順では、任意の種類のデータファイルをアプリケーションに追加する方法について説明し [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] ます。  
  
### <a name="to-include-a-data-file-by-using-mageexe"></a>Mage.exe を使用してデータファイルを含めるには  
  
1. アプリケーションのファイルの残りの部分を使用して、データファイルをアプリケーションディレクトリに追加します。  
  
    通常、アプリケーションディレクトリは、デプロイの現在のバージョンでラベル付けされたディレクトリ (例: v 1.0.0.0) になります。  
  
2. データファイルを一覧表示するようにアプリケーションマニフェストを更新します。  
  
    **mage.exe-u v 1.0.0.0 \ Application .manifest-FromDirectory v 1.0.0.0**  
  
    このタスクを実行すると、アプリケーションマニフェスト内のファイルの一覧が再作成され、ハッシュ署名も自動的に生成されます。  
  
3. 任意のテキストエディターまたは XML エディターでアプリケーションマニフェストを開き、 `file` 最近追加したファイルの要素を見つけます。  
  
    という名前の XML ファイルを追加した場合、 `Data.xml` ファイルは次のコード例のようになります。  
  
   `<file name="Data.xml" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`  
  
4. `type`この要素に属性を追加し、値をに指定し `data` ます。  
  
   `<file name="Data.xml" writeableType="applicationData" hash="23454C18A2DC1D23E5B391FEE299B1F235067C59" hashalg="SHA1" asmv2:size="39500" />`  
  
5. キーペアまたは証明書を使用してアプリケーションマニフェストに再署名し、デプロイマニフェストに再署名します。  
  
    アプリケーションマニフェストのハッシュが変更されているため、配置マニフェストに再署名する必要があります。  
  
    **mage.exe-s アプリケーションマニフェスト-cf cert_file-pwd パスワード**  
  
    **mage.exe-u 配置マニフェスト-appm アプリケーションマニフェスト**  
  
    **mage.exe-s 配置マニフェスト-cf certfile-pwd パスワード**  
  
6. 
  
### <a name="to-include-a-data-file-by-using-mageuiexe"></a>MageUI.exe を使用してデータファイルを含めるには  
  
1. アプリケーションのファイルの残りの部分を使用して、データファイルをアプリケーションディレクトリに追加します。  
  
2. 通常、アプリケーションディレクトリは、デプロイの現在のバージョンでラベル付けされたディレクトリ (例: v 1.0.0.0) になります。  
  
3. [ **ファイル** ] メニューの [ **開く** ] をクリックして、アプリケーションマニフェストを開きます。  
  
4. [ **ファイル** ] タブを選択します。  
  
5. タブの上部にあるテキストボックスに、アプリケーションのファイルが格納されているディレクトリを入力し、[ **設定**] をクリックします。  
  
     データファイルがグリッドに表示されます。  
  
6. データファイルの **ファイルの種類** の値を **データ**に設定します。  
  
7. アプリケーションマニフェストを保存し、ファイルに再署名します。  
  
     MageUI.exe によって、ファイルに再署名するように求められます。  
  
8. 配置マニフェストに再署名する  
  
     アプリケーションマニフェストのハッシュが変更されているため、配置マニフェストに再署名する必要があります。  
  
## <a name="see-also"></a>参照  
 [ClickOnce アプリケーションにおけるローカル データおよびリモート データへのアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)
