---
title: Set the session inactivity timeout
description: Learn about how to set the session inactivity timeout, including an overview on alerting users before sessions end due to inactivity.
author: paulliew
ms.author: paulliew
ms.topic: how-to
ms.date: 11/19/2020
ms.reviewer: johnmichalak
audience: IT Pro
ms.search.region: Global
ms.search.validFrom: 2019-08-30
ms.search.form: SystemAdministrationWorkspaceForm
ms.dyn365.ops.version: Platform update 29
---

# Set the session inactivity timeout

[!include [banner](../includes/banner.md)]

The session inactivity timeout setting represents the amount of time a user can be inactive before the user's session times out and closes. It only affects user browser sessions.

You can set the values from 5 minutes to 60 minutes.

This function has a default value of 30 minutes. You can set the value up to 60 minutes, however doing so might cause extra load on the system.

> [!NOTE] 
> This feature is available as of Platform update 29.
>
> If you previously set a session inactivity timeout in the web.config (**WebClientStatefulSessionTimeoutInSeconds** key) through a support request, then that old value will still be honored. The change in default will only affect those who had not explicitly set a new session inactivity timeout in the web config.

To change the value, follow these steps:

1. Select **System administration > Setup > System parameters** to open the **System parameters** page.
2. On the **General** tab, in the **Session management** section, enter a value in the **Session inactivity timeout in minutes** field.
3. Select **Save**. 

    If you set the value to greater than 30, you will be prompted to confirm your selection. The confirmation prompt says "Increasing the inactivity session timeout can cause extra load on your system, which can lead to a decrease in performance. Are you sure you want to continue?" The higher the value, the higher the load will be, which can affect negatively system performance. Select **Yes** to save the changes, or **No** to revert to the existing value.
    
### Alerting users before sessions end due to inactivity
To give users awareness of an impending session suspension due to inactivity and to help prevent users from losing any unsaved changes when this occurs, users will be notified before their sessions are set to be terminated due to inactivity and given an opportunity to reconnect. The notice given to the user is dependent on the **Session inactivity timeout** setting. 

-  If the **Session inactivity timeout** is more than 30 minutes, the user will see a countdown notification starting **5 minutes** before the session is set to close. 
-  If the **Session inactivity timeout** is between 10 and 30 minutes, the user will see a countdown notification starting **2 minutes** before the session is set to close. 
-  If the **Session inactivity timeout** is less than 10 minutes, the user will see a countdown notification starting **30 seconds** before the session is set to close.



[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
