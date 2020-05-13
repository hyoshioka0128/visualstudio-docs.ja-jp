---
title: '方法 : エンコーディングを使用してファイルを保存および開く | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-general
ms.topic: conceptual
helpviewer_keywords:
- Unicode, bi-directional language support
- files, encoding
- bi-directional language support, encoded files
- file encoding, bi-directional languages
ms.assetid: cb52b732-b395-4ba1-a3ef-104b3942a12a
caps.latest.revision: 9
author: jillre
ms.author: jillfra
manager: jillfra
ms.openlocfilehash: b9285a72137e4c2f3bdf54ef9f6535dedaa2cd5f
ms.sourcegitcommit: a8e8f4bd5d508da34bbe9f2d4d9fa94da0539de0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/19/2019
ms.locfileid: "72670775"
---
# <a name="how-to-save-and-open-files-with-encoding"></a>方法 : エンコーディングを使用してファイルを保存および開く
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

双方向言語をサポートするために、特定の文字エンコーディングを使用してファイルを保存できます。 また、Visual Studio でファイルが正しく開かれるように、ファイルを開くときにもエンコーディングを指定できます。

### <a name="to-save-a-file-with-encoding"></a>エンコーディングを使用してファイルを保存するには

1. **[ファイル]** メニューの **[名前を付けてファイルを保存]** を選び、 **[保存]** の横のドロップダウン ボタンをクリックします。

     **[保存オプションの詳細設定]** ダイアログ ボックスが表示されます。

2. **[エンコード]** で、ファイルに使うエンコーディングを選択します。

3. 必要に応じて、 **[行の終わり]** で行末文字の書式を選びます。

     このオプションは、異なるオペレーティング システムのユーザーとファイルを交換する場合に便利です。

     特定の方法でエンコードされていることがわかっているファイルを使用する場合は、ファイルを開くときに、そのエンコーディングを使用するように指定できます。 その方法は、ファイルがプロジェクトの一部であるかどうかによって異なります。

### <a name="to-open-an-encoded-file-that-is-part-of-a-project"></a>プロジェクトの一部であるエンコードされたファイルを開くには

1. **ソリューション エクスプローラー**でファイルを右クリックし、 **[ファイルを開くアプリケーションの選択]** を選びます。

2. **[ファイルを開くアプリケーションの選択]** ダイアログ ボックスで、ファイルを開くエディターを選びます。

     フォーム エディターなど、多くの Visual Studio エディターは、エンコーディングを自動検出し、ファイルを適切に開きます。 エンコーディングを選択できるエディターの場合は、 **[エンコード]** ダイアログ ボックスが表示されます。

3. **[エンコード]** ダイアログ ボックスで、エディターで使うエンコーディングを選びます。

### <a name="to-open-an-encoded-file-that-is-not-part-of-a-project"></a>プロジェクトの一部ではないエンコードされたファイルを開くには

1. **[ファイル]** メニューの **[開く]** をポイントし、 **[ファイル]** または **[Web のファイル]** を選んで、開くファイルを選びます。

2. **[開く]** ボタンの横のドロップダウン ボタンをクリックし、 **[ファイルを開くアプリケーションの選択]** を選びます。

3. 前の手順の 2. と 3. を実行します。

## <a name="see-also"></a>参照
 [エンコードと Windows フォームグローバリゼーション](https://msdn.microsoft.com/library/22e8965d-a712-42b3-8167-3ee346bd70f9)[アプリケーションのグローバライズとローカライズ](../ide/globalizing-and-localizing-applications.md)
