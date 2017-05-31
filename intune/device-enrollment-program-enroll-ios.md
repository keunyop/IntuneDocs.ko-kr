---
title: "iOS 장치 등록 - 장치 등록 프로그램"
titleSuffix: Intune Azure preview
description: "Intune Azure preview: DEP(장치 등록 프로그램)를 사용하여 회사 소유 iOS 장치를 등록하는 방법을 알아봅니다."
keywords: 
author: nathbarn
ms.author: nathbarn
manager: angrobe
ms.date: 04/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-intune
ms.technology: 
ms.assetid: 7981a9c0-168e-4c54-9afd-ac51e895042c
ms.reviewer: dagerrit
ms.suite: ems
ms.custom: intune-azure
ms.translationtype: Human Translation
ms.sourcegitcommit: 9ff1adae93fe6873f5551cf58b1a2e89638dee85
ms.openlocfilehash: 5144b9e7c17a3323667b9ca68cb47829d69866c3
ms.contentlocale: ko-kr
ms.lasthandoff: 05/23/2017


---

# <a name="enroll-ios-devices-using-device-enrollment-program"></a>장치 등록 프로그램을 사용하여 iOS 장치 등록

[!INCLUDE[azure_preview](./includes/azure_preview.md)]

이 항목은 IT 관리자가 [Apple DEP(장비 등록 프로그램)](https://deploy.apple.com)를 통해 구매한 회사 소유 iOS 장치를 등록하는 데 도움이 됩니다. Microsoft Intune에서는 DEP를 등록하는 등록 프로필을 "무선으로" 배포할 수 있으므로 관리자는 관리되는 각 장치를 손대지 않아도 됩니다. DEP 프로필에는 등록 중에 장치에 적용할 관리 설정이 포함되어 있습니다. 등록 패키지는 장치에 대한 설정 도우미 옵션을 포함할 수 있습니다.

>[!NOTE]
>DEP 등록은 [장치 등록 관리자](device-enrollment-manager-enroll.md)와 함께 사용할 수 없습니다.
>또한 사용자가 회사 포털 앱을 사용하여 iOS 장치를 등록한 다음 해당 장치의 일련 번호를 가져오고 DEP 프로필을 할당한 경우 장치가 Intune에서 등록 취소됩니다.

**DEP 등록 단계**
1. [Apple DEP 토큰 가져오기](#get-the-apple-dep-certificate)
2. [DEP 프로필 만들기](#create-an-apple-dep-profile)
3. [Intune 서버에 Apple DEP 일련 번호 할당](#assign-apple-dep-serial-numbers-to-your-mdm-server)
4. [DEP 관리 장치 동기화](#synchronize-dep-managed-devices)
5. [장치에 DEP 프로필 할당](#assign-a-dep-profile-to-devices)
6. [사용자에게 장치 배포](#distribute-devices-to-users)

## <a name="get-the-apple-dep-certificate"></a>Apple DEP 인증서 가져오기
회사 소유 iOS 장치를 Apple의 DEP(장비 등록 프로그램)에 등록하려면 먼저 Apple의 DEP 인증서(.p7m) 파일이 필요합니다. Intune에서는 이 토큰을 통해 회사에서 소유한 DEP 참가 장치에 대한 정보를 동기화할 수 있습니다. 또한 Apple에 등록 프로필을 업로드하고 이러한 프로필에 장치를 할당할 수 있습니다.

DEP를 사용하여 회사 소유의 iOS 장치를 관리하려면 조직이 Apple DEP에 가입하고 해당 프로그램을 통해 장치를 받아야 합니다. 해당 프로세스의 세부 정보는 https://deploy.apple.com에서 확인할 수 있습니다. 이 프로그램의 이점 중 하나는 USB 케이블을 사용해서 각 장치를 컴퓨터에 연결하지 않고도 장치를 자동 설치할 수 있다는 것입니다.

> [!NOTE]
> Intune 테넌트가 Intune 클래식 콘솔에서 Azure Portal로 마이그레이션되었고 사용자가 마이그레이션 기간에 Intune 관리 콘솔에서 Apple DEP 토큰을 삭제한 경우 DEP 토큰이 Intune 계정으로 복원되었을 수 있습니다. Azure Portal에서 DEP 토큰을 다시 삭제할 수 있습니다.

**1단계. Apple DEP 토큰을 만드는 데 필요한 Intune 공개 키 인증서를 다운로드합니다.**<br>
1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다. Intune 블레이드에서 **장치 등록** > **Apple DEP 토큰**을 선택합니다.
2. **공개 키 다운로드**를 선택하여 암호화 키(.pem) 파일을 다운로드하고 로컬로 저장합니다. .pem 파일은 Apple 장치 등록 프로그램 포털에서 트러스트 관계 인증서를 요청하는 데 사용됩니다.

**2단계. 적절한 Apple 웹 사이트에서 Apple DEP 토큰을 다운로드합니다.**<br>
[Apple 배포 프로그램을 통해 DEP 토큰 만들기](https://deploy.apple.com)(https://deploy.apple.com)를 선택하고 회사 Apple ID로 로그인합니다. 이 Apple ID를 사용하여 DEP 토큰을 갱신할 수 있습니다.

   1.  Apple의 [장비 등록 프로그램 포털](https://deploy.apple.com)에서 **장비 등록 프로그램** &gt; **서버 관리**로 이동한 후 **MDM 서버 추가**를 선택합니다.
   2.  **MDM 서버 이름**을 입력하고 **다음**을 선택합니다. 서버 이름은 참조용으로 MDM(모바일 장치 관리) 서버를 식별하기 위한 것으로, Microsoft Intune 서버의 이름 또는 URL이 아닙니다.
   3.  **&lt;ServerName&gt; 추가** 대화 상자가 열립니다. **파일 선택...**을 선택하여 .pem 파일을 업로드하고 **다음**을 선택합니다.
   4.  **&lt;ServerName&gt; 추가** 대화 상자에 **내 서버 토큰** 링크가 표시됩니다. 컴퓨터에 서버 토큰(.p7m) 파일을 다운로드한 다음 **완료**를 선택합니다.

**3단계. Apple DEP 토큰을 만드는 데 사용되는 Apple ID를 입력합니다. 이 ID를 사용하여 Apple DEP 토큰을 갱신할 수 있습니다.**

**4단계. 업로드할 Apple DEP 토큰으로 이동합니다. Intune에서 DEP 계정과 자동으로 동기화합니다.**<br>
인증서(.pem) 파일로 이동한 후 **열기**를 선택하고 **업로드**를 선택합니다. Push Certificate가 있으면 Intune에서 등록된 모바일 장치에 정책을 푸시하여 iOS 장치를 등록하고 관리할 수 있습니다.

## <a name="create-an-apple-dep-profile"></a>Apple DEP 프로필 만들기

장치 등록 프로필은 장치 그룹에 적용되는 설정을 정의합니다. 다음 단계는 DEP를 사용하여 등록된 iOS 장치에 대한 장치 등록 프로필을 만드는 방법을 보여 줍니다.

1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.
2. Intune 블레이드에서 **장치 등록**을 선택한 다음 **Apple 등록**을 선택합니다.
3. **APPLE DEP(장치 등록 프로그램) 설정 관리** 아래에서 **DEP 프로필**을 선택합니다.
4. **Apple DEP 프로필** 블레이드에서 **만들기**를 선택합니다.
5. **등록 프로필 만들기** 블레이드에서 프로필에 대한 이름 및 설명을 입력합니다.
6. **사용자 선호도**에서 이 프로필을 가진 장치가 사용자 선호도를 사용하여 등록되는지 사용하지 않고 등록되는지 선택합니다.

 - **사용자 선호도를 사용하여 등록** - 초기 설치 작업을 진행할 때 장치에 사용자 정보를 등록해야 합니다. 그러면 회사 데이터와 메일에 액세스하도록 허용할 수 있습니다. 사용자에게 속하고 앱 설치 같은 서비스에 회사 포털을 사용해야 하는 DEP 관리 장치에 대한 사용자 선호도를 선택합니다. MFA(다단계 인증)는 사용자 선호도가 있는 DEP 장치에 등록하는 동안 작동하지 않습니다. 등록 후 MFA는 이러한 장치에서 예상대로 작동합니다. DEP 장치에서는 처음 로그인할 때 자신의 암호를 변경해야 하는 새 사용자에게 등록 중에 메시지를 표시할 수 없습니다. 또한 암호가 만료된 사용자는 DEP 등록 중에 암호를 다시 설정하라는 메시지가 표시되지 않으며, 다른 장치에서 암호를 다시 설정해야 합니다.

    >[!NOTE]
    >사용자 선호도를 사용하는 DEP에서는 사용자 토큰을 요청하려면 [WS-Trust 1.3 사용자 이름/혼합 끝점](https://technet.microsoft.com/en-us/library/adfs2-help-endpoints)을 사용하도록 설정해야 합니다. [WS-Trust 1.3에 대해 자세히 알아보세요](https://technet.microsoft.com/itpro/powershell/windows/adfs/get-adfsendpoint).

 - **사용자 선호도를 사용하지 않고 등록**: 장치에 사용자 정보를 등록하지 않습니다. 로컬 사용자 데이터에 액세스하지 않고도 작업을 수행하는 장치에 대해 이 정보를 사용합니다. 기간 업무 앱을 설치하는 데 사용하는 회사 포털 앱 등 사용자 정보가 필요한 앱은 작동하지 않습니다.

7. **장치 관리 설정**을 선택하고 다음 프로필 설정을 구성한 후 **저장**을 선택합니다.

    - **감독됨** - 더 많은 관리 옵션을 사용할 수 있으며 기본적으로 활성화 잠금이 해제된 관리 모드입니다. 이 확인란을 비워 두면 관리 기능이 제한됩니다.

    - **등록 잠김** - (관리 모드 = 감독됨이어야 함) 관리 프로필 제거를 허용하는 iOS 설정이 해제됩니다. 이 확인란을 비워 두면 설정 메뉴에서 관리 프로필을 제거할 수 있습니다. 이 항목은 정품 인증을 하는 동안 설정되고 장치를 초기화해야 변경할 수 있습니다.

    - **연결 허용** - iOS 장치를 컴퓨터와 동기화할 수 있는지 여부를 지정합니다. **인증서로 Apple Configurator 허용**을 선택한 경우 **Apple Configurator 인증서** 아래에서 인증서를 선택해야 합니다.

    - **Apple Configurator 인증서** - **연결 허용** 아래에서 **인증서로 Apple Configurator 허용**을 선택한 경우 가져올 Apple Configurator 인증서를 선택합니다.

8. **설정 도우미 설정**을 선택하고 다음 프로필 설정을 구성한 후 **저장**을 선택합니다.

    - **부서 이름** - 정품 인증을 하는 동안 사용자가 **구성 정보**를 탭하면 표시됩니다.

    - **부서 전화** - 정품 인증을 하는 동안 사용자가 도움 필요 단추를 클릭하면 표시됩니다.
    - **설치 도우미 옵션** - 이러한 선택적 설정은 나중에 iOS **설정** 메뉴에서 지정할 수 있습니다.
        - **암호** - 정품 인증을 하는 동안 암호를 묻는 메시지가 표시됩니다. 장치가 보안된 상태가 아니거나 다른 방식으로 액세스가 제어된 상태(즉, 하나의 앱만 사용할 수 있도록 장치를 제한하는 키오스크 모드)가 아니면 항상 암호를 요구합니다.
        - **위치 서비스** - 이를 설정하면 정품 인증을 하는 동안 설치 도우미에서 서비스를 사용할지 묻는 메시지를 표시합니다.
        - **복원** - 이를 설정하면 정품 인증을 하는 동안 설치 도우미에서 iCloud 백업을 사용할지 묻는 메시지를 표시합니다.
        - **Apple ID** - 이 설정을 지정하면 Intune에서 ID 없이 앱을 설치하려고 할 때 iOS가 사용자에게 Apple ID를 묻습니다. Intune을 통해 설치한 앱을 비롯하여 iOS App Store 앱을 다운로드하려면 Apple ID가 필요합니다.
        - **사용 약관** - 이를 설정하면 정품 인증을 하는 동안 설치 도우미가 Apple의 약관에 동의하라는 메시지를 표시합니다.
        - **터치 ID** - 이 옵션을 사용하도록 설정하면 활성화하는 동안 설정 도우미에서 이 서비스를 확인하는 메시지가 표시됩니다.
        - **Apple Pay** - 이 옵션을 사용하도록 설정하면 활성화하는 동안 설정 도우미에서 이 서비스를 확인하는 메시지가 표시됩니다.
        - **확대/축소** - 이 옵션을 사용하도록 설정하면 활성화하는 동안 설정 도우미에서 이 서비스를 확인하는 메시지가 표시됩니다.
        - **Siri** - 이 옵션을 사용하도록 설정하면 활성화하는 동안 설정 도우미에서 이 서비스를 확인하는 메시지가 표시됩니다.
        - **진단 데이터** - 이 옵션을 사용하도록 설정하면 활성화하는 동안 설정 도우미에서 이 서비스를 확인하는 메시지가 표시됩니다.

9. 프로필 설정을 저장하려면 **등록 프로필 만들기** 블레이드에서 **만들기**를 선택합니다.

## <a name="assign-apple-dep-serial-numbers-to-your-mdm-server"></a>MDM 서버에 Apple DEP 일련 번호 할당
Intune에서 이러한 장치를 관리할 수 있도록 Apple DEP 웹 포털에서 Intune MDM 서버에 장치 일련 번호를 할당해야 합니다.

1. [장치 등록 프로그램 포털](https://deploy.apple.com)(https://deploy.apple.com)로 이동한 다음 회사 Apple ID로 로그인합니다.

2. **배포 프로그램** &gt; **장치 등록 프로그램** &gt; **장치 관리**로 이동합니다.

3. **장치 선택**방법을 지정하고, 장치 정보를 제공한 다음, 장치 **일련번호**, **주문 번호**또는 **CSV 파일 업로드**에 따라 세부 정보를 지정합니다.

4. **서버에 할당**을 선택하고 Microsoft Intune에 대해 지정된 &lt;ServerName&gt;을 선택한 다음 **확인**을 선택합니다.

## <a name="synchronize-dep-managed-devices"></a>DEP 관리 장치 동기화
이제 Intune에 DEP 장치 관리 권한이 할당되었으므로 Intune을 DEP 서비스와 동기화하여 Intune 포털에서 관리되는 장치를 확인할 수 있습니다.

1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.

2. Azure Portal의 Intune 블레이드에서 **장치 등록**을 선택한 다음 **Apple 등록**을 선택합니다.

3. **APPLE DEP(장치 등록 프로그램) 설정 관리** 아래에서 **DEP 일련 번호**를 선택합니다.

4. **Apple DEP 일련 번호** 블레이드에서 **동기화**를 선택합니다.

5. **동기화** 블레이드에서 **동기화 요청**을 선택합니다. 진행률 표시줄에 동기화를 다시 요청하기 전에 대기해야 하는 시간이 표시됩니다.

    허용 가능한 DEP 트래픽에 대한 Apple의 약관을 준수하려면 Intune에서는 다음과 같은 제한 사항을 적용합니다.
     -    전체 DEP 동기화는 7일마다 한 번 이상 실행할 수 없습니다. 전체 동기화 중 Intune은 Apple에서 일련 번호가 이전에 동기화되었는지 여부를 Intune에 할당한 모든 일련 번호를 새로 고칩니다. 전체 동기화를 이전 전체 동기화의 7일 이내에 시도하는 경우 Intune은 Intune에 나열되지 않은 일련 번호만 새로 고칩니다.
     -    모든 동기화 요청은 완료하는 데 10분이 주어집니다. 이 시간 동안 또는 요청이 성공될 때까지 **동기화** 단추는 비활성화됩니다.

>[!NOTE]
>**Apple DEP 일련 번호** 블레이드에서 프로필에 DEP 일련 번호를 할당할 수도 있습니다.

## <a name="assign-a-dep-profile-to-devices"></a>장치에 DEP 프로필 할당
Intune에서 관리하는 DEP 장치를 등록하려면 DEP 프로필을 할당해야 합니다.

1. Azure Portal에서 **추가 서비스** > **모니터링 + 관리** > **Intune**을 선택합니다.

2. Azure Portal의 Intune 블레이드에서 **장치 등록** > **Apple 등록**을 선택한 다음 **DEP 프로필**을 선택합니다.

3. **Apple DEP 등록 프로필** 목록에서 장치에 할당할 프로필을 선택한 다음 **장치 할당**을 선택합니다.

4. **할당**을 선택한 다음 이 프로필을 할당할 DEP 장치를 선택합니다. 다음 기준을 사용하여 필터링하면 DEP 사용 가능 장치를 확인할 수 있습니다.
  - **할당되지 않음**
  - **임의**
  - **&lt;DEP 프로필 이름&gt;**

  ![Intune 포털에서 DEP 프로필을 할당하는 데 사용되는 할당 단추의 스크린샷](media/dep-profile-assignment.png)

5. 프로필을 할당할 장치를 선택합니다. 열 위쪽에 있는 확인란을 선택하면 나열된 장치를 1,000개까지 선택할 수 있습니다. 장치를 선택한 후에 **할당**을 클릭합니다. 1,000개보다 많은 장치를 등록하려면 할당 단계를 반복하여 모든 장치에 DEP 프로필을 할당합니다.

## <a name="distribute-devices-to-users"></a>사용자에게 장치 배포

이제 회사 소유 장치를 사용자에게 배포할 수 있습니다. iOS DEP 장치가 켜진 경우 Intune에서 관리되도록 등록됩니다. 장치가 활성화되었으며 사용 중인 경우에는 장치를 초기화할 때까지 프로필을 적용할 수 없습니다.

[Microsoft Intune에 대한 최종 사용자 교육 방법](https://docs.microsoft.com/intune/deploy-use/how-to-educate-your-end-users-about-microsoft-intune)을 참조하세요. 직접 최종 사용자를 [Intune에서 iOS 또는 macOS 장치 사용](https://docs.microsoft.com/intune/deploy-use/how-to-educate-your-end-users-about-microsoft-intune)으로 안내할 수도 있습니다. 

### <a name="how-users-install-and-use-the-company-portal-on-their-devices"></a>사용자가 자신의 장치에서 회사 포털을 설치 및 사용하는 방법

사용자 선호도로 구성한 장치에서 회사 포털 앱을 설치하고 실행하여 앱을 다운로드하고 장치를 관리할 수 있습니다. 사용자는 장치를 받은 후 아래 설명된 추가 단계를 완료하여 설정 도우미를 완료하고 회사 포털 앱을 설치해야 합니다.
