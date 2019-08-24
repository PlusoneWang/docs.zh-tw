---
title: 將 Windows 容器部署至 Azure Container Service 的時機 (也就是 Kubernetes)
description: 使用 Azure 雲端和 Windows 容器現代化現有的 .NET 應用程式 |將 Windows 容器部署至 Azure Container Service 的時機 (也就是 Kubernetes)
ms.date: 04/30/2018
ms.openlocfilehash: 903082deba635dd0dfc22d0186fbc589f8d05b92
ms.sourcegitcommit: f20dd18dbcf2275513281f5d9ad7ece6a62644b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/30/2019
ms.locfileid: "69577941"
---
# <a name="when-to-deploy-windows-containers-to-azure-container-service-that-is-kubernetes"></a><span data-ttu-id="3e38d-103">將 Windows 容器部署至 Azure Container Service 的時機 (也就是 Kubernetes)</span><span class="sxs-lookup"><span data-stu-id="3e38d-103">When to deploy Windows Containers to Azure Container Service (that is, Kubernetes)</span></span>

<span data-ttu-id="3e38d-104">Azure Container Service 特別針對 Azure, 將熱門開放原始碼工具和技術的設定優化。</span><span class="sxs-lookup"><span data-stu-id="3e38d-104">Azure Container Service optimizes the configuration of popular open-source tools and technologies specifically for Azure.</span></span> <span data-ttu-id="3e38d-105">您會取得一個開放解決方案, 為您的容器和您的應用程式設定提供可攜性。</span><span class="sxs-lookup"><span data-stu-id="3e38d-105">You get an open solution that offers portability both for your containers and for your application configuration.</span></span> <span data-ttu-id="3e38d-106">您可以選取 [大小]、[主機數] 和 [orchestrator 工具]。</span><span class="sxs-lookup"><span data-stu-id="3e38d-106">You select the size, the number of hosts, and the orchestrator tools.</span></span> <span data-ttu-id="3e38d-107">Azure Container Service 會為您處理基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3e38d-107">Azure Container Service handles the infrastructure for you.</span></span>

<span data-ttu-id="3e38d-108">如果您已經在使用開放原始碼協調器 (例如 Kubernetes、Docker Swarm 或 DC/OS), 則不需要變更現有的管理作法, 就能將容器工作負載移至雲端。</span><span class="sxs-lookup"><span data-stu-id="3e38d-108">If you are already working with open-source orchestrators like Kubernetes, Docker Swarm, or DC/OS, you don't need to change your existing management practices to move container workloads to the cloud.</span></span> <span data-ttu-id="3e38d-109">使用您已熟悉的應用程式管理工具, 並透過適用于您所選 orchestrator 的標準 API 端點進行連接。</span><span class="sxs-lookup"><span data-stu-id="3e38d-109">Use the application management tools that you're already familiar with and connect via the standard API endpoints for the orchestrator of your choice.</span></span>

<span data-ttu-id="3e38d-110">如果您使用 Linux Docker 容器, 則所有這些協調器都是成熟的環境, 但可能僅適用于 Windows 容器的預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="3e38d-110">All these orchestrators are mature environments if you are using Linux Docker containers, but might only be in Preview state for Windows Containers.</span></span>

<span data-ttu-id="3e38d-111">例如, 在 Kubernetes 中, 容器的支援是原生 (第一方公民), 因此在 Kubernetes 上使用 Windows 容器也會有效 (在2018年初的 ACS 中為預覽狀態)。</span><span class="sxs-lookup"><span data-stu-id="3e38d-111">For example, in Kubernetes, support for containers is native (first-class citizen), so using Windows Containers on Kubernetes is also effective (in preview in ACS as of early 2018).</span></span>

<span data-ttu-id="3e38d-112">重要注意事項:針對 Kubernetes 發展和「更多 PaaS」版本的 ACS (Azure Container Service) 是 AKS (Azure Kubernetes Service), 不過, Windows 容器在2季2018仍不受支援, 但很快就會受到支援。</span><span class="sxs-lookup"><span data-stu-id="3e38d-112">Important note: The evolved and “more PaaS” version of ACS (Azure Container Service) for Kubernetes is AKS (Azure Kubernetes Service), however, Windows Containers are still not supported as of Q2 2018, but it will be supported soon.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="3e38d-113">[上一頁](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)
>[下一頁](choosing-azure-compute-options-for-container-based-applications.md)</span><span class="sxs-lookup"><span data-stu-id="3e38d-113">[Previous](when-to-deploy-windows-containers-to-azure-container-instances-ACI.md)
[Next](choosing-azure-compute-options-for-container-based-applications.md)</span></span>