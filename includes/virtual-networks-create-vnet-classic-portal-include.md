## <a name="how-to-create-a-vnet-in-the-azure-portal"></a>Azure 포털에서 VNet을 만드는 방법
위의 시나리오에 따라 VNet을 만들려면 다음 단계를 수행합니다.

1. 브라우저에서 http://manage.windowsazure.com으로 이동하고, 필요한 경우 Azure 계정으로 로그인합니다.
2. 아래 그림과 같이 **새로 만들기** > **NETWORK SERVICES** > **VIRTUAL NETWORK** > **사용자 지정 만들기**를 차례로 클릭합니다.
   
    ![포털에서 VNet 만들기](./media/virtual-networks-create-vnet-classic-portal-include/vnet-create-portal-figure1.gif)
3. **Virtual Network 세부 정보** 페이지에서 VNet의 **이름**을 입력하고 해당 **위치**를 선택한 후 페이지 오른쪽 아래 구석에 있는 화살표를 클릭하여 2단계로 이동합니다. 아래 그림에서는 이 시나리오에 대한 설정을 보여 줍니다.
   
    ![가상 네트워크 세부 정보 페이지](./media/virtual-networks-create-vnet-classic-portal-include/vnet-create-portal-figure2.png)
4. **DNS 서버 및 VPN 연결** 페이지에서 사용할 최대 9개의 DNS 서버에 대한 이름 및 IP 주소를 지정합니다. DNS 서버를 지정하지 않으면 VNet은 Azure에서 제공하는 내부 이름 확인 방법을 사용합니다. 이 시나리오에서는 DNS 서버를 구성하지 않을 예정입니다.
5. VNet에 대해 지점 및 사이트 간 VPN 액세스를 제공하려는 경우 **지점 및 사이트 간 VPN 구성** 확인란을 선택합니다. 지점 및 사이트 간 VPN을 구성하지 않은 경우 생성 후에 언제든지 VNet에 추가할 수 있습니다. 이 시나리오에서는 지점 및 사이트 간 VPN을 구성하지 않을 예정입니다.
6. VNet과 다른 VNet 또는 온-프레미스 네트워크 간에 사이트 간 VPN 연결을 제공하려는 경우 **사이트 간 VPN 구성** 확인란을 사용하도록 설정하고 **ExpressRoute**를 사용할지를 지정하거나 연결할 네트워크의 이름을 지정합니다. 사이트 간 VPN을 구성하지 않은 경우 생성 후에 언제든지 VNet에 추가할 수 있습니다. 이 시나리오에서는 사이트 간 VPN을 구성하지 않을 예정입니다.
7. 페이지의 오른쪽 아래 구석에 있는 화살표를 클릭하여 3단계로 이동합니다. 아래 그림에서는 이 시나리오에 대한 설정을 보여 줍니다.
   
    ![DNS 서버 및 VPN 연결 페이지](./media/virtual-networks-create-vnet-classic-portal-include/vnet-create-portal-figure3.png)
8. **Virtual Network 주소 공간** 페이지의 **시작 IP**에서 *10.0.0.0*을 클릭하여 VNet 주소 공간을 변경하고 사용할 시작 주소 공간을 입력합니다. 이 시나리오에서는 *192.168.0.0*을 입력합니다. 
9. **CIDR(주소 개수)** 에서 서브넷 마스크의 비트 수를 선택합니다. 이 시나리오에서는 *16(65536)*을 선택합니다.
10. **서브넷**에서 *Subnet-1* 을 클릭하고 필요한 경우 서브넷의 이름을 바꿉니다. 이 시나리오에서는 *FrontEnd*로 이름을 바꿉니다.
    
    > [!NOTE]
    > 서브넷의 이름 텍스트 상자 바깥쪽을 클릭하면 서브넷 이름을 다시 편집할 수 없게 됩니다. 이 문제를 해결하려면 오른쪽에 있는 X 단추를 클릭하여 서브넷을 제거한 다음 아래의 13단계에서 설명한 대로 새 서브넷을 추가해야 합니다.
    > 
    > 
11. 첫 번째 서브넷에 대한 **시작 IP** 에서 서브넷의 시작 IP 주소를 지정합니다. 이 시나리오에서는 *192.168.1.0*을 입력합니다.
12. **CIDR(주소 개수)** 에서 첫 번째 서브넷의 서브넷 마스크에 대한 비트 수를 선택합니다. 이 시나리오에서는 *24(256)*을 선택합니다.
13. 필요한 경우 **서브넷 추가** 를 클릭하여 새 서브넷을 추가합니다. 이 시나리오에서는 아래 그림과 같이 서브넷을 추가하고 10 ~ 12단계를 반복하여 VNet을 구성합니다.
    
    ![가상 네트워크 주소 공간 페이지](./media/virtual-networks-create-vnet-classic-portal-include/vnet-create-portal-figure4.png)
14. 페이지의 오른쪽 아래 구석에 있는 확인 표시 단추를 클릭하여 VNet을 만듭니다. 아래 그림과 같이 잠시 후에 사용 가능한 VNet 목록에 해당 Vnet이 표시됩니다.
    
    ![새 가상 네트워크](./media/virtual-networks-create-vnet-classic-portal-include/vnet-create-portal-figure5.png)



<!--HONumber=Nov16_HO3-->


