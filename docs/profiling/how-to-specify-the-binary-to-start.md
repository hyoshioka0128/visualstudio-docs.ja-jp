---
title: 開始するバイナリを指定する | Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
f1_keywords:
- vs.performance.property.itemlaunch
helpviewer_keywords:
- profiling tools, launching
- performance tools, launching
- performance sessions, launching
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 8b3aec9448c6493350683dc9f0bec0cc2d60fa82
ms.sourcegitcommit: 062615c058d2ff44751e8d0c704ccfa3c5543469
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90851334"
---
# <a name="how-to-specify-the-binary-to-start"></a>方法: 開始するバイナリを指定する

DLL などのバイナリをプロファイルするには、 **[\<Target> プロパティ ページ]** ダイアログ ボックスに情報を入力する必要があります。 この情報は、DLL プロジェクトの呼び出し元アプリケーションの場所を示します。

1. **パフォーマンス エクスプローラー**で、対象のバイナリを右クリックし、 **[プロパティ]** をクリックします。

2. **[プロパティ ページ]** ダイアログ ボックスで、 **[起動]** プロパティをクリックします。

3. **[プロジェクト プロパティのオーバーライド]** チェック ボックスを選択します。

4. **[起動する実行可能ファイル]** テキスト ボックスで、ファイルの場所を指定します。

5. **[引数]** テキスト ボックスで、アプリケーションを起動するのに必要な引数を指定します。

6. **[作業ディレクトリ]** テキスト ボックスで、ディレクトリの場所を指定します。

7. **[OK]** をクリックします。

## <a name="see-also"></a>関連項目

[パフォーマンス セッションの構成](../profiling/configuring-performance-sessions.md)
