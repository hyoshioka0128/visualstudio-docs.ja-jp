---
title: 'DA0003: カーネル サンプルが多数存在します | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: reference
f1_keywords:
- vs.performance.rules.DA0003
- vs.performance.DA0003
- vs.performance.3
- vs.performance.rules.DAManyKernelSamples
ms.assetid: c1f46f77-eb95-42e5-b340-d86bc9de41b4
caps.latest.revision: 16
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: ad9a0671595d4628932ff4f2db41a137e060c4d1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68158709"
---
# <a name="da0003-many-kernel-samples"></a>DA0003:カーネル サンプルが多数存在します
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

ルール Id |DA0003 |  
|Category |プロファイルツール使用法 |  
|プロファイル方法 |サンプリング |  
|Message |カーネルモードのサンプルの割合が高くなっています。 これは I/O アクティビティの量が多いか、コンテキスト切り替えの率が高いことを示す可能性があります。 インストルメンテーション モードで再度、アプリケーションをプロファイリングすることを検討してください。|  
|ルールの種類 |情報 |  
  
## <a name="cause"></a>原因  
 アプリケーションに対して集められた呼び出し履歴の大部分がカーネル モードで実行されています。 別のプロファイリング方法でアプリケーションをプロファイリングすることを検討してください。  
  
## <a name="rule-description"></a>ルールの説明  
 Windows の場合、カーネル モードまたはユーザー モードでコードを実行できます。 (カーネルモードは特権モードとも呼ばれます)。カーネルモードで実行されるのは、デバイスドライバーなどの低レベルのシステムコードだけです。 ユーザー モードのアプリケーションは、I/O 操作の実行、スレッドまたはプロセスの同期プリミティブの待機、またはシステム コールを実行するために、カーネル モードに遷移できます。  
  
 サンプリングは、ほとんどの時間をユーザー モードでの作業に費やすアプリケーションのプロファイリングで最も有効です。 アプリケーションがカーネル モードで実行されたときに集められたサンプルの数は、頻繁に発生する I/O 操作を示すか、コンテキスト切り替えが発生していることを示すことがあります。 これらの操作のいずれも、サンプリング方法では調査できません。 カーネル モードで採取されたサンプルが多すぎると、サンプリング データに、統計的な意味を持つだけ十分な数のユーザー モード サンプルが含まれない場合があります。  
  
## <a name="how-to-fix-violations"></a>違反の修正方法  
 次のいずれかのオプションで再度、アプリケーションをプロファイリングすることを検討してください。  
  
- インストルメンテーション方式を使用してプロファイリングする。  
  
- サンプリング レートを増やし、ユーザー モードで集めるサンプルを増やす。
