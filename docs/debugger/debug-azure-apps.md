---
title: Azure サービスをデバッグする | Microsoft Docs
description: Visual Studio で Azure サービスをデバッグできます。 それを行うさまざまな方法をこの記事に含まれるリンクから確認できます。
ms.custom: SEO-VS-2020
ms.date: 09/14/2018
ms.topic: how-to
helpviewer_keywords:
- debugger
ms.assetid: 3d434de3-ee5f-419d-9a94-ac4ac02d635b
author: mikejo5000
ms.author: mikejo
manager: jmartens
ms.workload:
- azure
ms.openlocfilehash: a77f1291621e84eb2e13075a791e9c6735447137
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99857623"
---
# <a name="debug-azure-services-in-visual-studio"></a>Visual Studio で Azure サービスをデバッグする

Visual Studio を使用して、さまざまなシナリオの Azure サービスをデバッグできます。

以下でホストされている運用環境アプリをデバッグするには:

- Azure App Service。Visual Studio Enterprise を使用する場合。[スナップショット デバッガーを使用したライブ ASP.NET アプリのデバッグ](../debugger/debug-live-azure-applications.md)に関するページを参照してください。

- Azure App Service または Service Fabric。Application Insights を使用する場合。「[.NET アプリでの例外でのデバッグ スナップショット](/azure/application-insights/app-insights-snapshot-debugger)」を参照してください。

- Azure 仮想マシンまたは Azure 仮想マシン スケール セット。「[スナップショット デバッガーを使用して、Azure Virtual Machines と Azure Virtual Machine Scale Sets 上のライブ ASP.NET アプリをデバッグする](../debugger/debug-live-azure-virtual-machines.md)」を参照してください。

- Azure Kubernetes Service。「[スナップショット デバッガーを使用してライブ ASP.NET Azure Kubernetes サービスをデバッグする](../debugger/debug-live-azure-kubernetes.md)」を参照してください。

以下のリモート デバッグを実行するには:

- IIS 上の ASP.NET (Azure App Service または Azure VM)。[Azure 上での ASP.NET のリモート デバッグ](remote-debugging-azure.md)に関するページを参照してください。

- Azure Service Fabric 上の ASP.NET。「[リモートの Service Fabric アプリケーションをデバッグする](/azure/service-fabric/service-fabric-debugging-your-application#debug-a-remote-service-fabric-application)」を参照してください

## <a name="see-also"></a>関連項目

- [Visual Studio でのデバッグ](../debugger/index.yml)
