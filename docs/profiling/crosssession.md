---
title: CrossSession | Microsoft Docs
description: VSPerfCmd.exe CrossSession オプションを使用して、プロファイラーで任意のコンソール セッションからデータを収集できるようにする方法について学習します。 Start オプションも指定する必要があります。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: reference
ms.assetid: b9fcb9c3-7903-478c-9b7c-dbd94092fcba
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: a52acb80bac511706086c56074eb5bfe450b7674
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99955906"
---
# <a name="crosssession"></a>CrossSession
*VSPerfCmd.exe* **CrossSession** オプションを使用すると、プロファイラーはあらゆるコンソール セッションからデータを収集できます。 **CrossSession** オプションは、**Start** オプションと共に使用する必要があります。

 **CrossSession** の代わりに省略形の **CS** を利用できます。

## <a name="syntax"></a>構文

```cmd
VSPerfCmd.exe /Start:Method /CrossSession [Options]
```

#### <a name="parameters"></a>パラメーター
 なし

## <a name="valid-options"></a>有効なオプション
 別のセッションでプロファイリングを有効にするには、**CrossSession** オプションは **Start** オプションと共に指定する必要があります。 **CrossSession** は、後続の **VSPerfCmd Attach** コマンドと **Detach** コマンドでも指定する必要があります。

 **Start:** `Method`**Start** オプションは、指定したプロファイル方法にプロファイラーを初期化します。

 **Attach:** _PID_[ **,** _PID_] 指定されたプロセスのプロファイリングを開始します。

 **Detach**[**:**_PID_[,_PID_]] 指定されたプロセスのプロファイリングを停止します。

## <a name="example"></a>例
 この例では、別のコンソール セッションで開始されたアプリケーションにアタッチするために **CrossSession** オプションが使用されます。

```cmd
VSPerfCmd.exe /Start:Sample /Output:TestApp.exe.vsp /CrossSession
VSPerfCmd.exe /Attach:12345 /CS
```

## <a name="see-also"></a>関連項目
- [VSPerfCmd](../profiling/vsperfcmd.md)
- [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)
- [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)
- [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)
