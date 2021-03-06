---
title: Microsoft Intune에서 비즈니스용 Windows 업데이트 구성 - Azure | Microsoft Docs
description: Windows 10 디바이스에서 Microsoft Intune을 사용하여 비즈니스용 Windows 업데이트 설정에서 업데이트 링을 만들고, 준수를 검토하고, 업데이트를 일시 중지하기 위해 프로필에서 소프트웨어 업데이트 설정을 업데이트합니다.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/12/2019
ms.topic: conceptual
ms.prod: ''
ms.service: microsoft-intune
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: coryfe
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 05fd362ff6f068669b85b9b78cb1dfd7d3c8011f
ms.sourcegitcommit: 25e6aa3bfce58ce8d9f8c054bc338cc3dff4a78b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57397272"
---
# <a name="manage-software-updates-in-intune"></a>Intune에서 소프트웨어 업데이트 관리

[!INCLUDE [azure_portal](./includes/azure_portal.md)]

Intune을 사용하여 Windows as a Service가 Windows 10 디바이스를 업데이트하는 방법과 시기를 지정하는 업데이트 링을 정의합니다. 업데이트 링은 디바이스 그룹에 정책을 할당하는 정책입니다. 업데이트 링을 사용하여 비즈니스 요구 사항을 반영하는 업데이트 전략을 만들 수 있습니다. 자세한 내용은 [비즈니스용 Windows 업데이트를 사용하여 업데이트 관리](https://technet.microsoft.com/itpro/windows/manage/waas-manage-updates-wufb)를 참조하세요.

Windows 10에서는 새로운 기능 업데이트 및 품질 업데이트에 모든 이전 업데이트의 내용이 포함됩니다. 최신 업데이트를 설치하면 Windows 10 디바이스가 최신 상태가 됩니다. 이전 버전의 Windows와 달리, 이제는 일부 업데이트가 아니라 전체 업데이트를 설치해야 합니다.


비즈니스용 Windows 업데이트를 사용하여 업데이트 관리 환경을 간소화할 수 있습니다. 디바이스 그룹에 대해 개별 업데이트를 승인할 필요가 없습니다. 업데이트 출시 전략을 구성하여 환경에서 위험을 관리할 수 있습니다. Intune에서는 디바이스에서 [업데이트 설정을 구성](windows-update-settings.md)하는 기능 및 업데이트 설치를 지연하는 기능을 제공합니다. Intune에서는 업데이트를 저장하지 않고 업데이트 정책 할당만 저장합니다. 디바이스에서 Windows 업데이트에 직접 액세스하여 업데이트합니다. Windows 10 업데이트가 설치될 때 구성되는 이 설정 모음을 ‘Windows 10 업데이트 링’이라고 합니다.

Windows 10 업데이트 링은 [범위 태그](scope-tags.md)를 지원합니다. 업데이트 링과 함께 범위 태그를 사용하여 사용할 구성 세트를 필터링 및 관리할 수 있습니다.

## <a name="prerequisites"></a>전제 조건  

Intune에서 Windows 10 디바이스의 Windows 업데이트를 사용하려면 다음 필수 구성 요소를 충족해야 합니다.  

- Windows 10 PC는 Windows Anniversary 업데이트 이상(버전 1607 이상)이 포함된 Windows 10 Pro 이상을 실행해야 합니다.
- Windows 업데이트는 다음 Windows 10 버전을 지원합니다.
  - Windows 10
  - Windows 10 Team(Surface Hub 디바이스용)
  - Windows Holographic for Business  

    Windows Holographic for Business는 다음을 포함한 Windows 업데이트의 설정 하위 집합을 지원합니다.
    - **자동 업데이트 동작**
    - **Microsoft 제품 업데이트**
    - **서비스 채널** **반기 채널** 및 **반기 채널(대상 지정)** 옵션 지원  

    자세한 내용은 [Windows Holographic 관리](windows-holographic-for-business.md)를 참조하세요.  
  
  Windows 10 Mobile을 실행하는 디바이스는 지원되지 않습니다.

- Windows 디바이스에서 **피드백 및 진단** > **진단 및 사용 현황 데이터**를 **기본**, **고급** 또는 **전체**로 설정해야 합니다.  

  이 설정을 수동으로 구성하거나 Windows 10 이상에 대한 Intune 디바이스 제한 프로필을 사용할 수 있습니다. 디바이스 제한 프로필을 사용하려면 **일반** > **진단 데이터 전송** 설정을 **기본** 이상으로 구성합니다. 디바이스 프로필에 대한 자세한 내용은 [디바이스 제한 설정 구성](device-restrictions-configure.md)을 참조하세요.  

- Azure 클래식 포털을 사용하는 경우 [설정을 Azure Portal로 마이그레이션](#migrate-update-settings-to-the-azure-portal)합니다.  

## <a name="create-and-assign-update-rings"></a>업데이트 링 만들기 및 할당

1. [Azure 포털](https://portal.azure.com)에 로그인합니다.
2. **모든 서비스**를 선택하고 **Intune**에서 필터링한 다음, **Microsoft Intune**을 선택합니다.
3. **소프트웨어 업데이트** > **Windows 10 업데이트 링** > **만들기**를 선택합니다.
4. 이름, 설명(선택 사항)을 입력한 다음, **구성**을 선택합니다.
5. **설정**에서 비즈니스 요구 사항에 대한 설정을 구성합니다. 사용할 수 있는 설정에 대한 자세한 내용은 [Windows 업데이트 설정](windows-update-settings.md)을 참조하세요.  
6. 작업을 완료하면 **확인**을 선택합니다. **업데이트 링 만들기**에서 **만들기**를 선택합니다. 새 업데이트 링이 업데이트 링 목록에 표시됩니다.
7. 링을 할당하려면 업데이트 링 목록에서 링을 선택한 후 \<링 이름> 탭에서 **할당**을 선택합니다.
8. **포함** 및 **제외** 탭을 사용하여 이 링이 할당되는 그룹을 정의한 후 **저장**을 선택하여 할당을 완료합니다.

## <a name="manage-your-windows-10-update-rings"></a>Windows 10 업데이트 링 관리
포털에서 Windows 10 업데이트 링을 선택하여 해당 **개요** 창을 열 수 있습니다. 이 창에서 링 할당 상태를 보고 링을 관리하는 추가 작업을 수행할 수 있습니다. 
### <a name="to-view-an-updates-rings-overview-pane"></a>업데이트 링 [개요] 창을 보려면: 
1. Azure Portal에 로그인합니다.
2. **Intune** > **소프트웨어 업데이트** > **Windows 10 업데이트 링**으로 이동합니다.
3. 보거나 관리할 업데이트 링을 선택합니다.  

할당 상태를 보는 것 외에 [개요] 창 위쪽에서 다음 작업을 선택하여 업데이트 링을 관리할 수 있습니다.  
- [삭제](#delete)  
- [일시 중지](#pause)  
- [다시 시작](#resume)  
- [연장](#extend)  
- [제거](#uninstall)  

![사용 가능한 작업](./media/windows-update-for-business-configure/overview-actions.png)

### <a name="delete"></a>삭제  
**삭제**를 선택하여 선택된 Windows 10 업데이트 링의 설정을 적용을 중지합니다. 링을 삭제하면 Intune에서 해당 구성이 제거되어 Intune이 해당 설정을 더 이상 적용 및 실행하지 않습니다.  

Intune에서 링을 삭제해도 업데이트 링이 할당된 디바이스의 설정은 수정되지 않습니다.  대신, 디바이스에서는 현재 설정을 유지합니다. 이렇게 되는 이유는 디바이스는 이전에 적용된 설정의 기록 레코드를 유지하지 않으며 디바이스가 활성화되어 있는 추가 업데이트 링에서 설정을 수신할 수 있기 때문입니다.  

#### <a name="to-delete-a-ring"></a>링을 삭제하려면  
1. 업데이트 링의 개요 페이지를 보는 동안 **삭제**를 선택합니다.  
2. **확인**을 선택합니다.  

### <a name="pause"></a>일시 중지  
**일시 중지**를 선택하여 링을 일시 중지하는 시점부터 최대 35일 동안 할당된 디바이스가 기능 업데이트나 품질 업데이트를 수신하지 않도록 합니다. 최대 일수가 경과하고 나면 일시 중지 기능은 자동으로 만료되고 디바이스가 Windows 업데이트에서 적용되는 업데이트를 검색합니다. 이 검색 이후 다시 업데이트를 일시 중지할 수 있습니다. 일시 중지된 업데이트 링을 다시 시작한 후 해당 링을 다시 일시 중지하면 일시 중지 기간이 35일로 다시 설정됩니다.  

 #### <a name="to-pause-a-ring"></a>링을 일시 중지하려면  
1. 업데이트 링의 개요 페이지를 보는 동안 **일시 중지**를 선택합니다.  
2. **기능** 또는 **품질**을 선택하여 해당 형식의 업데이트를 일시 중지한 후 **확인**을 선택합니다.  
3. 한 업데이트 형식을 일시 중지한 후 다시 [일시 중지]를 선택하여 다른 업데이트 형식을 일시 중지할 수 있습니다.  

업데이트 형식이 일시 중지되면 해당 링의 [개요] 창에는 해당 업데이트 형식이 다시 시작되기 전에 남은 기간(일)이 표시됩니다.

> [!IMPORTANT]  
> 일시 중지 명령을 실행한 후 디바이스는 다음에 서비스에 체크 인할 때 이 명령을 수신합니다. 체크 인 이전에 예약된 업데이트가 설치될 수도 있습니다. 또한 일시 중지 명령을 실행할 때 대상 디바이스가 꺼져 있었던 경우 디바이스를 켜면 디바이스가 Intune을 사용해 체크 인하기 전에 예약된 업데이트를 다운로드 및 설치할 수도 있습니다.

### <a name="resume"></a>다시 시작  
업데이트 링이 일시 중지된 동안 **다시 시작**을 선택하여 해당 링의 기능 및 품질 업데이트를 활성 작업으로 복원할 수 있습니다. 업데이트 링을 다시 시작한 후 해당 링을 다시 일시 중지할 수 있습니다.  

#### <a name="to-resume-a-ring"></a>링을 다시 시작하려면  
1. 일시 중지된 업데이트 링의 개요 페이지를 보는 동안 **다시 시작**을 선택합니다.  
2. 사용 가능한 옵션을 선택하여 **기능** 또는 **품질** 업데이트를 다시 시작한 후 **확인**을 선택합니다.  
3. 한 업데이트 형식을 다시 시작한 후 다시 [다시 시작]을 선택하여 다른 업데이트 형식을 다시 시작할 수 있습니다.  

### <a name="extend"></a>Extend  
업데이트 링이 일시 중지된 동안 **연장**을 선택하여 해당 업데이트 링의 기능 및 품질 업데이트에 대한 일시 중지 기간을 35일로 다시 설정할 수 있습니다.  

#### <a name="to-extend-the-pause-period-for-a-ring"></a>링의 일시 중지 기간을 연장하려면  
1. 일시 중지된 업데이트 링의 개요 페이지를 보는 동안 **연장**을 선택합니다. 
2. 사용 가능한 옵션을 선택하여 **기능** 또는 **품질** 업데이트를 다시 시작한 후 **확인**을 선택합니다.  
3. 한 업데이트 형식의 일시 중지를 연장한 후 다시 [연장]을 선택하여 다른 업데이트 형식을 연장할 수 있습니다.  

### <a name="uninstall"></a>제거  
Intune 관리자는 **제거**를 사용하여 활성 또는 일시 중지된 업데이트 링의 최신 ‘기능’ 업데이트 또는 ‘품질’ 업데이트를 제거(롤백)할 수 있습니다. 하나의 형식을 제거한 후 다른 형식을 제거할 수 있습니다. Intune에서는 사용자가 업데이트를 제거하는 기능을 지원하거나 관리하지 않습니다.  

성공적으로 제거하려면:  
- 디바이스에서 Windows 10 2018년 4월 업데이트(버전 1803) 이상을 실행해야 합니다.  

디바이스에 최신 업데이트를 설치해야 합니다. 업데이트는 누적되므로 최신 업데이트를 설치하는 디바이스에는 가장 최근 기능 및 품질 업데이트가 포함됩니다. 예를 들어 Windows 10 머신에서 주요 문제가 발견되어 지난 업데이트를 롤백하려는 경우 이 옵션을 사용할 수 있습니다.  

제거를 사용하는 경우 다음을 고려합니다.  
- 기능 또는 품질 업데이트의 제거는 디바이스가 켜져 있는 서비스 채널에서만 사용할 수 있습니다.  

- 기능 또는 품질 업데이트에 대해 제거를 사용하면 Windows 10 머신에서 이전 업데이트를 복원하는 정책이 트리거됩니다.  

- Windows 10 디바이스에서 품질 업데이트가 성공적으로 롤백된 후 최종 사용자는 **Windows 설정** > **업데이트** > **업데이트 기록**에 나열된 업데이트를 계속 볼 수 있습니다.  

- 특히 기능 업데이트의 경우 기능 업데이트를 제거할 수 있는 시간은 업데이트 링의 업데이트 설정 **기능 업데이트 제거 기간 설정(2~60일)** 에 구성된 대로 2~60일로 제한됩니다. 기능 업데이트가 구성된 제거 기간보다 더 오래 설치된 후에는 디바이스에 설치된 기능 업데이트를 롤백할 수 없습니다.  

  예를 들어 기능 업데이트 제거 기간이 20일인 업데이트 링을 고려합니다. 25일 후에 최신 기능 업데이트를 롤백하고 [제거] 옵션을 사용하기로 결정합니다.  최소 20일 전에 기능 업데이트를 설치한 디바이스는 유지 관리의 일부로 필요한 비트를 제거했으므로 기능 업데이트를 제거할 수 없습니다. 그러나 최대 19일 전에 기능 업데이트만 설치한 디바이스는, 제거 기간 20일을 초과하기 전에 제거 명령을 수신하도록 성공적으로 체크 인한 경우, 업데이트를 제거할 수 있습니다.  

Windows 업데이트 정책에 대한 자세한 내용은 Windows 클라이언트 관리 설명서에서 [Update CSP](https://docs.microsoft.com/windows/client-management/mdm/update-csp)를 참조하세요.  

#### <a name="to-uninstall-the-latest-windows-10-update"></a>최신 Windows 10 업데이트를 제거하려면  
1. 일시 중지된 업데이트 링의 개요 페이지를 보는 동안 **제거**를 선택합니다.  
2. 사용 가능한 옵션을 선택하여 **기능** 또는 **품질** 업데이트를 제거한 후 **확인**을 선택합니다.  
3. 한 업데이트 형식의 제거를 트리거한 후 다시 [제거]를 선택하여 나머지 업데이트 형식을 제거할 수 있습니다.  

## <a name="migrate-update-settings-to-the-azure-portal"></a>업데이트 설정을 Azure Portal로 마이그레이션  
Azure 클래식 포털에는 디바이스 구성 프로필에 제한된 개수의 다른 Windows 10 업데이트 설정도 있습니다. Azure Portal로 마이그레이션할 때 이러한 설정이 구성되어 있는 경우 다음을 수행하는 것이 좋습니다.  

1. 필요한 설정을 사용하여 Azure Portal에서 Windows 10 업데이트 링을 만듭니다. **시험판 기능 허용** 설정은 더 이상 최신 Windows 10 빌드에 적용할 수 없기 때문에 Azure Portal에서 지원되지 않습니다. 업데이트 링을 만들 때 나머지 3개 설정뿐만 아니라 다른 Windows 10 업데이트 설정도 구성할 수 있습니다.  

   > [!NOTE]  
   > 클래식 포털에서 만든 Windows 10 업데이트 설정은 마이그레이션 후 Azure Portal에서 표시되지 않습니다. 하지만 이러한 설정이 적용됩니다. 이러한 설정을 마이그레이션하고 Azure Portal에서 마이그레이션된 정책을 편집하는 경우 정책에서 해당 설정이 제거됩니다.  

2. 클래식 포털에서 업데이트 설정을 삭제합니다. Azure Portal로 마이그레이션하고 동일한 설정을 업데이트 링에 추가한 후에는 잠재적인 정책 충돌을 방지하기 위해 클래식 포털에서 설정을 삭제해야 합니다. 예를 들어 동일한 설정을 서로 다른 값으로 구성한 경우 충돌이 발생합니다. 클래식 포털에서 구성된 설정이 Azure Portal에 표시되지 않기 때문에 쉽게 알 수 없습니다.  

## <a name="next-steps"></a>다음 단계
[Intune에서 지원하는 Windows 업데이트 설정](windows-update-settings.md)  

[업데이트에 대한 Intune 준수 보고서](windows-update-compliance-reports.md)

