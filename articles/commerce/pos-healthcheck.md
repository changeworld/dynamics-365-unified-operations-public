---
title: Health check for POS peripherals and services
description: This article describes the health check operation in Microsoft Dynamics 365 Commerce point of sale (POS).
author: ritakimani
ms.date: 02/27/2025
ms.topic: how-to
ms.custom: 
  - bap-template
ms.reviewer: v-chrgriffin
ms.assetid: e23e944c-15de-459d-bcc5-ea03615ebf4c
ms.search.region: Global
ms.author: ritakimani
ms.search.validFrom: 2019-03-31

---

# Health check for POS peripherals and services

[!include [banner](includes/banner.md)]

This article describes the health check operation in Microsoft Dynamics 365 Commerce point of sale (POS).

Retail stores can be complex environments where many applications and devices are used. As operations grow, it can become difficult to ensure that operations always run smoothly. For example, dependencies on peripherals that can break or accidentally become unplugged can disrupt operations. Troubleshooting issues that are related to devices and services can be costly for larger merchants and equally frustrating for smaller operations.

Dynamics 365 Commerce includes a health check operation that can help prevent some of this cost and frustration. The health check operation can help retailers detect issues before they occur by providing a method for testing devices directly from the POS outside of normal operations, and two tests for network-related issues.

## Key terms

| Term | Description |
|---|---|
| Peripheral | Any device that the POS application uses to facilitate transactions and other operations in the store. Examples include cash drawers, bar code scanners, and payment terminals. |
| Service | In this article, a service is an ancillary application that the POS application depends on to perform transactions and daily operations. Examples include apps that help with tax or shipping calculations. |

## Health check operation

The health check operation is operation 717 on the **POS Operations** page in Commerce Headquarters. It can be used while the POS is in nondrawer mode. However, a hardware station must be active.

POS users can access the health check operation in two ways:

- By selecting the **Health check** button on the **Settings** page.
- By adding a tile to your screen layout button grid and associating the health check operation with that tile. 

### Peripheral health checks

By default, the health check operation only tests devices that are configured in the hardware profile for the hardware station that is currently active for a register. If a register uses multiple hardware stations over the course of a day, to do health checks for all of them, it must connect to one hardware station at a time. There's no store-level health check. However, it's possible that this type of check can be done through Commerce Server extensibility.

#### Out-of-box health checks

| Type | Connection | Details |
|---|---|---|
| Printer | OPOS | This check tests basic object linking and embedding for POS (OPOS) functions. Here are some examples:<ul><li>Open: **Open** &gt; **ClaimDevice** &gt; **DeviceEnabled=True**</li><li>Close: **DeviceEnabled=False** &gt; **ReleaseDevice** &gt; **Close**</li></ul> |
| Line display | OPOS | This check tests basic OPOS functions. Here are some examples:<ul><li>Open: **Open** &gt; **ClaimDevice** &gt; **DeviceEnabled=True**</li><li>Close: **DeviceEnabled=False** &gt; **ReleaseDevice** &gt; **Close**</li></ul> |
| Dual display | Windows | This check ensures that the operating system detects a second Windows display. | 
| MSR | OPOS | This check tests basic OPOS functions. Here are some examples:<ul><li>Open: **Open** &gt; **ClaimDevice** &gt; **DeviceEnabled=True**</li><li>Close: **DeviceEnabled=False** &gt; **ReleaseDevice** &gt; **Close**</li></ul> |
| Drawer | OPOS | This check tests basic OPOS functions. Here are some examples:<ul><li>Open: **Open** &gt; **ClaimDevice** &gt; **DeviceEnabled=True**</li><li>Close: **DeviceEnabled=False** &gt; **ReleaseDevice** &gt; **Close**</li></ul> | 
| Scanner | OPOS | This check tests basic OPOS functions. Here are some examples:<ul><li>Open: **Open** &gt; **ClaimDevice** &gt; **DeviceEnabled=True**</li><li>Close: **DeviceEnabled=False** &gt; **ReleaseDevice** &gt; **Close**</li></ul> | 
| Scale | OPOS | This check tests basic OPOS functions. Here are some examples:<ul><li>Open: **Open** &gt; **ClaimDevice** &gt; **DeviceEnabled=True**</li><li>Close: **DeviceEnabled=False** &gt; **ReleaseDevice** &gt; **Close**</li></ul> |
| PIN pad | OPOS | This check tests basic OPOS functions. Here are some examples:<ul><li>Open: **Open** &gt; **ClaimDevice** &gt; **DeviceEnabled=True**</li><li>Close: **DeviceEnabled=False** &gt; **ReleaseDevice** &gt; **Close**</li></ul> |
| Payment terminal | Payments SDK | This check tests basic payment terminal functions provided by the Payments SDK. <ul><li>Lock</li><li>BeginTransaction</li><li>EndTransaction</li><li>ReleaseDevice</li><li>Close</li></ul> |

#### Use peripheral health checks in the POS

When the health check operation is initiated in the POS, a pane on the right lists the configured devices and shows the status of each device. To do a health check for a single device, select the device, and then select **Test selected**. To do a health check for all devices, select **Test all**. The **Test all** function tests all the devices, one at a time, and updates the status of each device in the **Status** column.

The **Last check** column shows when the health check was last done for each device.

If a device passes the health check (that is, if no errors are encountered), the device's status is shown as **OK**. If the health check fails, the status indicates that there was an error. In this case, the **Details** pane provides details related to the error, or instructs the user to contact the system administrator.

Some devices, such as the OPOS keylock, don't have out-of-box health check tests. If no health check test is detected for a device that is used, the status is **Not supported**.

### Network health checks

The two out-of-box network health checks listed below are always included in the health check list regardless of the peripherals configured for the terminal. The Retail Server connectivity and network latency health checks can be run individually or together. 

| Name                       | Details                                                      |
| -------------------------- | ------------------------------------------------------------ |
| Retail Server connectivity | The Retail Server connectivity health check verifies that the terminal can communicate with Retail Server and the channel database, and verifies that real-time service calls can be made to Commerce headquarters. |
| Network latency            | The network latency health check tests the network latency between the terminal and Retail Server. The test returns the average latency for 10 calls to Retail Server in a five-second period. |

#### Network latency health check

Network latency health check results are categorized as shown in the following table.

| Latency range       | Meaning                                                      |
| ------------------- | ------------------------------------------------------------ |
| 0–50 ms             | **Good** – Your network latency is low and not likely to be the source of any performance related issues. |
| 50–100 ms           | **Acceptable** – Your network latency is in the acceptable range, but may be degrading performance for network-intensive operations such as offline sync. |
| Above 100 ms | <p>**Poor** – Your network latency is likely degrading your point of sale operations. Although latency in the 100–150 ms range might not cause noticeable performance degradation for common operations, latency above 150 ms slows down most operations.</p><p>To further diagnose network latency, run an internet speed test on the register. If the internet speed test result latency is high, notify your system administrator that you're experiencing high latency with your internet connection.</p> |

### Health check charts

The following health check charts are added to provide more insights into network connectivity and performance. They also help admins analyze any app issues that might be linked to network connectivity during a specific period. 

- **History of connectivity** – Provides insights about whether the connectivity was with **internet access**, **local access** with no internet, or **no access** at all. The chart shows an hourly view for a 24-hour period. However, the period can be narrowed to minutes to provide insights into any network fluctuations that occurred during a specific period when app issues were noticed.

    :::image type="content" source="media/connectivityhistory.jpg" alt-text="Screenshot that shows an example of a History of connectivity chart on the Connectivity health report page.":::

- **Connection type** – Provides insights into the type of connection that the point of sale device uses to connect to the internet.

    :::image type="content" source="media/connectivitytype.jpg" alt-text="Screenshot that shows an example of a Connection type chart on the Connectivity health report page.":::

- **Wi-Fi signal strength** – Provides insights into the quality of the Wi-Fi signal strength for a 24-hour period. The period can be narrowed to minutes to provide detailed insights into any Wi-Fi fluctuations that might be responsible for app issues during specific times of a day.

    :::image type="content" source="media/WIFIsignalstrength.jpg" alt-text="Screenshot that shows an example of a Wi-Fi signal strength chart on the Connectivity health report page.":::

To access a health check chart in Store Commerce, follow these steps.

1. Go to the **Available tests** page.
1. Select the checkbox for the network health check that you want to run.
1. In the **Details** pane on the right, select the **About** tab.
1. Select **View connectivity insights**.

### Extend health checks

The out-of-box health check tests are configured to provide some user-friendly messages for typical errors. However, not all scenarios are covered. Through extensibility, merchants can map user-friendly messages to errors that might be specific to their environment.

Custom health checks can also be created to test devices that aren't supported out of the box, or to test any services that the POS depends on.

## Related articles

[Store Commerce app triggers and printing](dev-itpro/pos-trigger-printing.md)


[!INCLUDE[footer-include](../includes/footer-banner.md)]
