---
title: Submit alerts about country/region-specific regulatory features
description: Learn about how to use Microsoft Dynamics Lifecycle Services to submit alerts through the Regulatory alert submission service.
author: filatovm
ms.author: evgenypopov
ms.topic: how-to
ms.date: 04/29/2025
ms.reviewer: johnmichalak
ms.search.region: global
ms.search.validFrom: 2016-02-28
ms.dyn365.ops.version: AX 7.0.0
ms.assetid: b37140b4-5d6f-460f-ae36-f0d7bd90c0d3
---

# Submit alerts about country/region-specific regulatory features

[!include [banner](../includes/banner.md)]

This article describes how to use Microsoft Dynamics 365 Lifecycle Services to submit alerts through the Dynamics 365 regulatory alert submission service. This article also explains how to track planned and released regulatory features through Lifecycle Services Issue search. 

A regulatory alert is a notification for Microsoft about an **upcoming** (that is, not yet enforced) change in country- or region-specific laws or regulations that may affect business processes supported in Dynamics 365 finance and operations apps. Microsoft processes such alerts and decides whether any changes in Dynamics 365 finance and operations apps are required to support the regulatory changes. Microsoft then releases corresponding [regulatory updates](../../../finance/localizations/global/regulatory-updates.md).

> [!IMPORTANT]
> The Dynamics regulatory alert submission service shouldn't be used to communicate the information about issues in existing regulatory features, missing regulatory features, or not supported existing regulatory requirements. In such cases, contact Microsoft support for further guidance.

## Accessing the regulatory alert submission service

To access the regulatory alert submission service, in your project or a project you're invited to in Dynamics Lifecycle Services, do one of the following:
- From the menu, select **Alert service**.
- Scroll to the right side of the page, and under **More tools**, select **Alert service**. 

The **Dynamics regulatory alert submission** page appears. You can use this page to view any alerts that have previously been submitted by you or your organization.

## Submitting a regulatory alert
To enter a new regulatory alert, Select the plus sign (**+**) at the top of the **Dynamics regulatory alert submission** page, above the filter. The **Alert submission** wizard starts. You can complete the following tasks in this wizard:

- Search for existing regulatory items.
- Describe an alert.
- Confirm submissions.

### Search for existing regulatory items

Use Issue search to identify whether a regulatory feature that is related to the alert already exists.

1.  Enter a search term, such as a keyword, country/region, Microsoft Knowledge Base (KB) number, or Application Object Tree (AOT) object. Select the search button. Any items that include the search term, in either product issues or regulatory features, appear in the search results. You can narrow the search by using the available filters.
2.  If you don't find the regulatory feature that you're looking for, you can submit a regulatory alert by selecting **Submit regulatory alert** at the bottom of the browser window. 

### Describe the alert

1. Enter information about the alert in the appropriate fields. Required fields are indicated with a red asterisk. The following table provides more information about the fields on the **Describe the alert** page.

    <table >
            <tr>
                <td >
                <p><strong>Field</strong></p>
                </td>
                <td >
                <p><strong>Description</strong></p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Title</p>
                </td>
                <td>
                <p>Enter a descriptive title to identify the area of impact. For example, enter <strong>Changes in invoice document as of January 1, 2018</strong>.</p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Description</p>
                </td>
                <td>
                <p>Enter a brief overview of the law. Your description should focus on issues that are relevant to enterprise resource planning (ERP), so that users can understand the requirements at a high level without having to read the legislation first. </p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Country/region</p>
                </td>
                <td>
                <p>Select the country or region that the legislation applies to. </p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Industry</p>
                </td>
                <td>
                <p>Select the industry, if the requirement applies only to specific industries. For example, select <strong>Public sector</strong>, <strong>Commerce</strong>, or <strong>Manufacturing</strong>. </p><br/>            </td>
            </tr>
            <tr>
                <td>
                <p>Feature reference</p>
                </td>
                <td>
                <p>Enter the feature reference, if available.</p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Law enforcement date</p>
                </td>
                <td>
                <p>Select the date when affected customers must start to comply with the law.  </p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Government announcement date</p>
                </td>
                <td>
                <p>Select the date when the authority announced the change. </p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Latest filing date</p>
                </td>
                <td>
                <p>Select the deadline for the first submission of the new or changed report.     </p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Link to legislation </p>
                </td>
                <td>
                <p>Enter one or more links to the published law, interpretation guideline, implementation guidance, or any other useful documentation that help users understand or implement the requirement.</p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Company name</p>
                </td>
                <td>
                <p>Enter the company name for the person who is submitting the alert.         </p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Contact name</p>
                </td>
                <td>
                <p>Enter the name of the person who is submitting the alert.     </p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Contact email</p>
                </td>
                <td>
                <p>The email address of the person who is submitting the alert.   </p>
                </td>
            </tr>
            <tr>
                <td>
                <p>Business process</p>
                </td>
                <td>
                <p>The business processes that you selected through the <strong>Alert submission</strong> wizard.</p>
                </td>
            </tr>
            <tr>
                <td>Comments</td>
                <td>
                <p>Enter any other information that might be help users understand or implement the requirement. Select <strong>Submit</strong> to save your comment. Multiple comments can be added and should be submitted separately. Comments are saved in the order that they're added. </p>
                </td>
            </tr>
            <tr>
                <td> Attachments </td>
                <td> <p>Select the <strong>Upload</strong> button, and then browse to select a file to add as an attachment. After you select the file, it&#39;s uploaded and appears as a linked file. You can add up to three files that have a size of 5 MB each. To delete attached files, select <strong>Remove</strong> under the title of the file. <strong>Note</strong> Attachments must be publicly available materials. They can&#39;t be propriety or customer-specific/partner-specific.</p>
                </td>
            </tr>
    </table>

2.  After you've finished entering all the information, select the consent check box (**By submitting this regulatory alert, I consent to Microsoft contacting me for more information about this alert. Microsoft Privacy Statement.**). When you select the check box, the **Submit** button becomes available.
3.  Select **Submit** to save and submit the alert.

If you don't have all of the required information, or if you're not yet ready to submit the alert, you can save a partially completed alert.

### Confirm your submission

-   When the alert is successfully submitted, you receive a confirmation message. Select **Done** to exit the wizard.
-   If you save the alert before you submit it, an alert ID is generated, and you receive confirmation that the alert has been saved.

## Track the status of regulatory features in Issue search
You can use Issue search in Lifecycle Services to find planned and released regulatory features, and any associated localization documentation, certifications, and reports. To narrow your search to regulatory features, use the following filters:

-   **Category** - Select **Regulatory feature** only.
-   **Country/region** - Select **&gt;** to select the country/region that you're interested in.

To narrow the search even more, you can apply the following filters

-   **Product** - Select the products and product versions that you're interested in.
-   **Status** - Select specific statuses.



[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
