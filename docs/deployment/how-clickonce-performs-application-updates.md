---
title: ClickOnce がアプリケーションの更新を実行する方法 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- VB
- CSharp
- C++
helpviewer_keywords:
- updates, ClickOnce
- ClickOnce deployment, updates
- deploying applications [ClickOnce], application updates
ms.assetid: d54313c2-cf0c-420d-b151-99953a95f0bb
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 9217558c68d47ef8f2bf34b10db16463ee76f857
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62900025"
---
# <a name="how-clickonce-performs-application-updates"></a>ClickOnce がアプリケーションの更新を実行するしくみ
ClickOnce では、アプリケーションの配置マニフェストで指定されたファイルバージョン情報を使用して、アプリケーションのファイルを更新するかどうかを決定します。 更新が開始されると、ClickOnce は *ファイル修正* と呼ばれる手法を使用して、アプリケーションファイルの冗長ダウンロードを回避します。

## <a name="file-patching"></a>ファイルの修正
 アプリケーションを更新する場合、ファイルが変更されていない限り、ClickOnce では、新しいバージョンのアプリケーションのすべてのファイルがダウンロードされるわけではありません。 代わりに、現在のアプリケーションのアプリケーションマニフェストで指定されたファイルのハッシュ署名を、新しいバージョンのマニフェストの署名と比較します。 ファイルの署名が異なる場合は、ClickOnce によって新しいバージョンがダウンロードされます。 署名が一致する場合、ファイルはあるバージョンから次のバージョンに変更されていません。 この場合、ClickOnce は既存のファイルをコピーし、新しいバージョンのアプリケーションで使用します。 この方法では、1つまたは2つのファイルだけが変更された場合でも、ClickOnce によってアプリケーション全体を再度ダウンロードする必要がなくなります。

 ファイルの修正は、およびメソッドを使用して、必要に応じてダウンロードされるアセンブリに対しても機能し <xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroup%2A> <xref:System.Deployment.Application.ApplicationDeployment.DownloadFileGroupAsync%2A> ます。

 Visual Studio を使用してアプリケーションをコンパイルする場合、プロジェクト全体をリビルドするたびに、すべてのファイルに対して新しいハッシュ署名が生成されます。 この場合、一部のアセンブリだけが変更される可能性がありますが、すべてのアセンブリがクライアントにダウンロードされます。

 ファイルの修正は、データとしてマークされ、データディレクトリに格納されているファイルに対しては機能しません。 これらは、ファイルのハッシュ署名に関係なく、常にダウンロードされます。 データディレクトリの詳細については、「 [ClickOnce アプリケーションでローカルデータおよびリモートデータにアクセス](../deployment/accessing-local-and-remote-data-in-clickonce-applications.md)する」を参照してください。

## <a name="see-also"></a>こちらもご覧ください
- [ClickOnce の更新方法の選択](../deployment/choosing-a-clickonce-update-strategy.md)
- [ClickOnce 配置ストラテジの選択](../deployment/choosing-a-clickonce-deployment-strategy.md)