---
title: "Intune 장치 인벤토리 확인"
titleSuffix: Intune on Azure
description: "Intune으로 관리하는 장치를 확인하는 방법과 해당 하드웨어 및 설치된 앱을 파악하는 방법을 알아봅니다.\""
keywords: 
author: robstackmsft
ms.author: robstack
manager: angrobe
ms.date: 06/25/2017
ms.topic: get-started-article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: e71c6bdb-d75c-404f-8e38-24a663be81c2
ms.suite: ems
ms.custom: intune-azure
ms.openlocfilehash: dae92c117bcf8a4a8ff133ed613f9f77ea0c07c2
ms.sourcegitcommit: 34cfebfc1d8b81032f4d41869d74dda559e677e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2017
---
# <a name="how-to-view-intune-device-inventory"></a>Intune 장치 인벤토리를 확인하는 방법


[!INCLUDE[azure_portal](./includes/azure_portal.md)]

**장치** 워크로드에서 관리하는 장치, 장치의 하드웨어 기능 및 장치에 설치된 앱을 확인할 수 있습니다. 

장치 인벤토리를 확인하려면:

1. Azure 포털에 로그인합니다.
2. **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.
3. **Intune** 블레이드에서 **장치**를 선택합니다.

이제 다음 옵션 중 하나를 선택합니다.

- **개요** - 등록한 장치 및 각 장치에서 실행하는 운영 체제에 대한 정보를 가져옵니다.
- **관리** - **모든 장치**를 선택하면 관리하는 모든 장치 목록이 표시됩니다.
    목록에서 이러한 장치 중 하나를 선택하면 <*장치 이름*> **개요** 블레이드가 열립니다. 여기서 다음 중 하나를 선택할 수 있습니다.
    - **개요** - 이름, 소유자, BYOD 장치인지 여부, 체크 인했는지 여부 등 장치에 대한 일반 정보를 표시합니다.
    ![장치 개요](./media/device-overview.png)
    - **하드웨어** - 사용 가능한 저장소 공간, 모델, 제조업체 등 장치에 대한 자세한 정보를 표시합니다.
    ![관리되는 장치 하드웨어 인벤토리](./media/hardware-inventory.png)
    - **검색된 앱** - Intune에서 찾아서 장치에 설치한 모든 앱 목록을 표시합니다.
    ![검색된 앱 노드](./media/detected-applications.png)
    - **장치 준수** - 장치에 할당된 모든 준수 정책의 준수 상태를 표시합니다.
    - **장치 구성** - 장치에 할당된 모든 장치 구성 정책의 준수 상태를 표시합니다.
- **모니터** **장치 작업**을 선택하면 관리하는 장치에서 수행된 장치 작업 목록 및 현재 상태가 표시됩니다.
- **설치 프로그램** > **TeamViewer 커넥터** -TeamViewer 소프트웨어를 사용하여 장치에서 원격 관리를 구성하도록 허용합니다. 자세한 내용은 [Intune 관리 Android 장치에 대해 원격 지원 제공](/intune/device-profile-android-teamviewer)을 참조하세요.

