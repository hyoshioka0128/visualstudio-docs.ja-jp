---
title: Windows サービスのデバッグを準備する | Microsoft Docs
ms.custom: seodec18
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- debugging [Visual Studio], Windows services
- Windows Service applications, debugging
ms.assetid: ac0a99f7-ec3d-4a20-b17f-698a817fdcc2
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 3161f6d2c328e8e33dd82ed206aa8aa20e654cc9
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72738085"
---
# <a name="debugging-preparation-windows-services"></a>デバッグの準備:Windows サービス
Windows サービスは、Microsoft Windows のバックグラウンドで実行されるプログラムです。 Windows サービスには、Telnet サービスや、コンピューターに表示される時計を更新する Windows タイム サービスなどがあります。 Windows サービスは [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] 内から実行できないため、サービス コントロール マネージャーのコンテキストで実行する必要があります。 詳細については、「[Windows サービスの作成](/dotnet/framework/windows-services/how-to-create-windows-services)」、「[Windows サービス アプリケーションのデバッグ](/dotnet/framework/windows-services/how-to-debug-windows-service-applications)」、および「[Windows サービス アプリケーション](/dotnet/framework/windows-services/index)」を参照してください。

## <a name="see-also"></a>関連項目
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
- [C#、F#、および Visual Basic のプロジェクト](../debugger/debugging-preparation-csharp-f-hash-and-visual-basic-project-types.md)
- [C# デバッグ構成のプロジェクト設定](../debugger/project-settings-for-csharp-debug-configurations.md)
- [Visual Basic デバッグ構成のプロジェクト設定](../debugger/project-settings-for-a-visual-basic-debug-configuration.md)
- [方法: 方法 : OnStart メソッドをデバッグする](../debugger/how-to-debug-the-onstart-method.md)