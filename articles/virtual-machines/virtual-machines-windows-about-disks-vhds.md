---
title: Windows VM에 대한 디스크 및 VHD 정보 | Microsoft Docs
description: Azure의 Windows 가상 컴퓨터용 디스크 및 VHD의 기본 사항에 대해 알아봅니다.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management

ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: cynthn

---
# <a name="about-disks-and-vhds-for-azure-virtual-machines"></a>Azure 가상 컴퓨터용 디스크 및 VHD 정보
다른 컴퓨터와 마찬가지로, Azure에서 가상 컴퓨터는 운영 체제, 응용 프로그램 및 데이터를 저장하는 장소로 디스크를 사용합니다. 모든 Azure 가상 컴퓨터는 Windows 운영 체제 디스크와 임시 디스크라는 적어도 2개의 디스크를 갖습니다. 운영 체제 디스크는 이미지에서 만들어지며, 운영 체제 디스크 및 이미지 모두는 Azure 저장소 계정에 저장된 VHD(가상 하드 디스크)입니다. 가상 컴퓨터에도 데이터 디스크가 있을 수 있으며 이러한 디스크도 VHD로 저장됩니다. 이 문서는 [Linux 가상 컴퓨터](virtual-machines-linux-about-disks-vhds.md)에도 적용됩니다.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-both-include.md)]

## <a name="operating-system-disk"></a>운영 체제 디스크
모든 가상 컴퓨터는 하나의 연결된 운영 체제 디스크를 갖습니다. 이 디스크는 SATA 드라이브로 등록되며 기본적으로 C 드라이브로 레이블이 지정됩니다. 이 디스크의 최대 용량은 1023기가바이트(GB)입니다. 

## <a name="temporary-disk"></a>임시 디스크
임시 디스크는 자동으로 만들어집니다. 이 디스크는 일시적으로 D: 드라이브로 레이블이 지정되며 pagefile.sys를 저장하는 데 사용됩니다. 

임시 디스크의 크기는 가상 컴퓨터의 크기에 따라 달라집니다. 자세한 내용은 [Windows 가상 컴퓨터 크기](virtual-machines-windows-sizes.md)를 참조하세요.

> [!WARNING]
> 데이터를 임시 디스크에 저장하지 마세요. 이는 응용 프로그램 및 프로세스에 대한 임시 디스크를 제공하며 페이지 또는 스왑 파일과 같은 데이터 저장에 사용됩니다. 이 디스크를 다른 드라이브 문자로 다시 매핑하려면 [Windows 임시 디스크의 드라이브 문자 변경](virtual-machines-windows-classic-change-drive-letter.md)을 참조하세요.
> 
> 

Azure에서 임시 디스크를 사용하는 방법에 대한 자세한 내용은 [Microsoft Azure 가상 컴퓨터에서의 임시 드라이브 이해](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="data-disk"></a>데이터 디스크
데이터 디스크는 응용 프로그램 데이터 또는 사용자가 보존해야 하는 기타 데이터를 저장하기 위해 가상 컴퓨터에 연결된 VHD입니다. 데이터 디스크는 SCSI 드라이브로 등록되며 사용자가 선택한 문자로 레이블이 지정됩니다.  각 데이터 디스크의 최대 용량은 1023GB입니다. 가상 컴퓨터의 크기에 따라 사용자가 해당 가상 컴퓨터에 연결할 수 있는 데이터의 디스크의 용량과 디스크를 호스트하기 위해 사용할 수 있는 저장소 유형이 결정됩니다.

> [!NOTE]
> 가상 컴퓨터 용량에 대한 자세한 내용은 [Windows 가상 컴퓨터에 대한 크기](virtual-machines-windows-sizes.md)를 참조하세요.
> 
> 

Azure는 사용자가 이미지에서 가상 컴퓨터를 만들 때 운영 체제 디스크를 만듭니다. 사용자가 데이터 디스크를 포함하는 이미지를 사용하는 경우, Azure는 가상 컴퓨터를 만들 때, 데이터 디스크도 함께 만듭니다. 그렇지 않은 경우, 가상 컴퓨터를 만든 후에 데이터 디스크를 추가하십시오.

사용자는 언제든지 가상 컴퓨터에 디스크를 **연결** 하여 해당 가상 컴퓨터에 데이터 디스크를 추가할 수 있습니다. 사용자는 자신의 저장소 계정 또는 Azure가 사용자 본인을 위해 만든 계정에 업로드하거나 복사한 VHD를 사용할 수 있습니다. 데이터 디스크를 추가하면 VHD 파일과 VM이 연결되며, 해당 VHD에서 “임대"를 설정하여 해당 VHD가 연결되어 있는 동안 저장소에서 파일이 삭제되지 않게 할 수 있습니다.

## <a name="about-vhds"></a>VHD에 대하여
Azure에서 사용되는 VHD는 Azure의 표준 또는 프리미엄 저장소 계정에서 페이지 blob으로 저장되는 .vhd 파일입니다. 페이지 Blob에 대한 자세한 내용은 [블록 Blob 및 페이지 Blob 이해](https://msdn.microsoft.com/library/ee691964.aspx)를 참조하세요. 프리미엄 저장소에 대한 자세한 내용은 [프리미엄 저장소: Azure 가상 컴퓨터 작업을 위한 고성능 저장소](../storage/storage-premium-storage.md)를 참조하세요.

Azure는 고정 디스크 VHD 형식을 지원합니다. 고정 형식은 디스크 오프셋 X가 blob 오프셋 X에 저장되도록 파일 내에 선형적으로 논리적 디스크를 배치합니다. blob 끝의 작은 바닥글에서는 VHD의 속성을 설명합니다. 고정 형식은 대부분의 디스크에서 사용되지 않는 공간 범위가 크기 때문에 공간이 낭비되는 경우가 많습니다. 하지만 Azure에서는 .vhd 파일을 스파스 형식으로 저장하기 때문에 고정 및 동적 디스크의 장점을 동시에 얻을 수 있습니다. 자세한 내용은 [가상 하드 디스크 시작](https://technet.microsoft.com/library/dd979539.aspx)을 참조하세요.

사용자가 디스크 및 이미지를 만들기 위해 원본으로 사용하려는 Azure의 모든 .vhd 파일은 읽기 전용입니다. 사용자가 디스크 및 이미지를 만들 때, Azure는 .vhd 파일의 복사본을 만듭니다. 이러한 복사본들은 읽기 전용이거나 사용자가 VHD를 사용하는 방법에 따라 읽기 또는 쓰기 모두를 할 수 있습니다.

사용자가 이미지에서 가상 컴퓨터를 만들 때, Azure는 원본 .vhd 파일의 복사본인, 가상 머신에 대한 디스크를 만듭니다. 실수로 삭제되지 않도록 보호하기 위해, Azure는 이미지, 운영 체제 디스크 또는 데이터 디스크를 만드는 데 사용되는 모든 원본 .vhd 파일에 임대를 설정합니다.

원본 .vhd 파일을 삭제하기 전에, 디스크 또는 이미지를 삭제하여 임대를 제거해야 합니다. 가상 컴퓨터 및 연결된 모든 디스크를 삭제하여 가상 컴퓨터, 운영 체제 디스크 및 원본 .vhd 파일을 한번에 삭제할 수 있습니다. 그러나 데이터 디스크의 원본인 .vhd 파일을 삭제하려면 설정된 순서대로 몇 가지 단계를 수행해야 합니다. 먼저 가상 컴퓨터에서 디스크를 분리한 다음 디스크를 삭제하고 .vhd 파일을 삭제합니다.

> [!WARNING]
> 저장소에서 원본 .vhd 파일을 삭제하거나, 사용자의 저장소 계정을 삭제한 경우, Microsoft는 해당 데이터를 복구할 수 없습니다.
> 
> 

## <a name="next-steps"></a>다음 단계
* [디스크를 연결](virtual-machines-windows-attach-disk-portal.md) 하여 VM에 다른 저장소를 추가합니다.
* [Windows VM 이미지를 Azure에 업로드](virtual-machines-windows-upload-image.md) 합니다.
* [Windows 임시 디스크의 드라이브 문자 변경](virtual-machines-windows-classic-change-drive-letter.md) 합니다.

<!--HONumber=Oct16_HO2-->


