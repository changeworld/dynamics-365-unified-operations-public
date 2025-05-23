---
title: Microsoft Power Platform integration with finance and operations apps
description: Learn about Microsoft Power Platform integration via Microsoft Dynamics Lifecycle Services for finance and operations apps and Microsoft Dataverse.
author: Sunil-Garg
ms.author: sunilg
ms.topic: article
ms.custom: 
  - bap-template
ms.date: 05/08/2025
ms.reviewer: johnmichalak
ms.search.region: Global
ms.search.validFrom: 2020-10-31
ms.dyn365.ops.version: 10.0.0
---

# Microsoft Power Platform integration with finance and operations apps

[!include[banner](../includes/banner.md)]

> [!IMPORTANT]
> Beginning **May 1, 2025**, all environments for finance and operations apps are required to have the Power Platform Integration enabled. Before this date, environment administrators should enable the Power Platform Integration by following the steps in this article, selecting the Power Platform environment to which the environment for your finance and operations apps should be linked. Any finance and operations apps environments that aren't linked to a Power Platform environment through the Power Platform Integration after this date have the Power Platform Integration automatically enabled for the environment. During automated enablement, the environment is either be linked to a newly provisioned Power Platform environment, or linked to an existing Power Platform environment if either [dual-write](../data-entities/dual-write/dual-write-home-page.md) or [virtual entities for finance and operations apps](../power-platform/virtual-entities-overview.md) has already been enabled for the environment.
> Learn more about enabling and configuring the integration in [Enabling the Power Platform integration](./enable-power-platform-integration.md).

Microsoft Power Platform provides a suite of capabilities for Dynamics 365 applications via the Power Platform admin center. Today, finance and operations apps aren't managed by the Power Platform admin center. However, over time more and more management capabilities will be migrated from Microsoft Dynamics Lifecycle Services over to the admin center. In the interim, customers are able to unlock features, such as dual-write functionality, virtual entities, add-ins, and more via Microsoft Power Platform integration functionality in Lifecycle Services.

## Getting started

To learn more about how to connect your environment to either a new or an existing Power Platform environment, see [Enable Power Platform Integration](enable-power-platform-integration.md).

## Prerequisite reading

To understand the architecture of Microsoft Power Platform, Dataverse, dual-write, and virtual entities for finance and operations apps, you must understand how they work. Therefore, the following documentation is a prerequisite:

- [Administer Power Platform](/power-platform/admin/admin-documentation)
- [What is Dataverse?](/powerapps/maker/common-data-service/data-platform-intro)
- [Tables in Dataverse](/powerapps/maker/common-data-service/entity-overview)
- [Entity relationships overview](/powerapps/maker/common-data-service/relationships-overview)
- [Create and edit virtual tables that contain data from an external data source](/powerapps/maker/common-data-service/create-edit-virtual-entities)
- [What is Power Apps portals?](/powerapps/maker/portals/overview)
- [Overview of creating apps in Power Apps](/powerapps/maker/)

## Tools and services unlocked with Microsoft Power Platform integration
Below are tools and services that are unlocked with the Power Platform integration, enabling new features in finance and operations apps. As we continue to unify finance and operations applications with the Microsoft Power Platform, an increasing number of capabilities will be powered by services within the Power Platform ecosystem. This integration enables greater flexibility, automation, and intelligence, allowing businesses to streamline operations and enhance decision-making through low-code applications, process automation, and advanced analytics. As this evolution progresses, organizations can expect improved interoperability between Dynamics 365 applications and Power Platform services, driving efficiency and innovation across financial and operational workflows.

### Integration tools for data and business logic
Together, virtual entities, dual-write, business events, and data events make up the shared data layer for the convergence of finance and operations apps and the Dataverse platform. They'e complementary technologies that are intended to work together. 

**Virtual entities** enable scenarios where access to finance and operations data from Microsoft Power Platform or native Dataverse apps is required. You can query that data, bind forms to it, and generally use the full power of Microsoft Power Platform against the full breadth of finance and operations apps. Data isn't copied between systems. Instead, it's accessed directly through the standard virtual entity infrastructure that Microsoft Power Platform technologies can already bind to. For more information, see [Virtual entities overview](virtual-entities-overview.md). 

**Business events** let you use Microsoft Power Platform to respond to events that are occurring in finance and operations apps. These events occur when a process is run in the application with business logic. Business events can be raised from any app, including finance and operations apps, and can be handled by Microsoft Power Platform business logic. This handling often includes querying or interacting with additional data through either native entities or virtual entities. 

**Data events**, similar to business events, enable external applications to receive notifications from finance and operations apps when events occur. Data events occur when there's a change to a record in the application data. External systems can react to notifications when a create, update, or delete (CUD) operation occurs in the data.

For a subset of scenarios, data must be physically copied between finance and operations apps and native Dataverse entities. These scenarios are for overlapping entities that already have a large amount of bound logic in both native Dataverse apps and finance and operations apps, so that the data must reside in the local database of each type of app. Although the number of these entities is relatively small, it includes some of the most important entities, such as Account/Customer, Company, Product, and Sales order. For these scenarios, **dual-write** enables near-real-time synchronous copying of data. This capability enables existing apps to continue to operate against local data, as designed, and also ensures that the corresponding overlapping entity is kept in sync. For more information, see the [Dual-write home page](../data-entities/dual-write/dual-write-home-page.md). 

Together, virtual entities, dual-write, business events, and data events let you build apps and business processes that span the boundaries between finance and operations apps and native Dataverse apps. Most apps and business processes use either a combination of these three parts of the shared data layer or all of them. As always, extension and customization should reduce the amount of data that is copied between databases as much as possible, and should also optimize for the best possible user experience when these tools are used. 

### AI capabilities enabled by the Power Platform
Finance and operations apps utilize the Power Platform to enable AI features. The features are dependent on AI services like [Microsoft Copilot Studio](/microsoft-copilot-studio/fundamentals-what-is-copilot-studio), [AI Builder](/ai-builder/overview), and capabilities in [Microsoft Dataverse]/power-apps/maker/data-platform/data-platform-intro) to light up powerful AI features in finance and operations apps. The Power Platform integration must be enabled in the environment to access the services for the AI features.

Learn more about some of the AI-driven capabilities in finance and operations apps that are enabled by the Power Platform in [Overview of Copilot capabilities in finance and operations apps](../../fin-ops/copilot/copilot-for-finance-operations.md).

### Data archival
Integration with the Power Platform enables archival of data for finance and operations apps with custom retention policies for securely archiving and retaining unlimited data. With this feature data is moved from the database for finance and operations apps into Dataverse long-term retention, enabling greater scale for finance and operations apps. See [Archive data in Dynamics 365 finance and operations apps with Dataverse](../sysadmin/archive-data.md) for more information.

### Add-ins functionality

Add-ins provide a way to extend the functionality of finance and operations apps. All add-ins are installed and managed via Lifecycle Services on the environment details page for sandbox and production-type environments. The metadata regarding which add-ins are installed and the configuration options for each add-in are stored in the Microsoft Dataverse database that is provisioned as part of the Microsoft Power Platform integration. Some add-ins also store business data in the Dataverse database. To learn more about available add-ins, see [Add-ins overview](add-ins-overview.md).

## Typical scenarios and patterns that use dual-write

Here are some typical scenarios that use dual-write.

### Customer service representatives can facilitate a change of address for finance and operations customers

A customer relocates and wants to change their billing and shipping address information. This customer contacts a customer service representative and requests a change of address. The customer service representative takes the call and changes the customer's billing and shipping address information.

| Decision | Information | 
|----------|-------------|
| Is real-time data required? | Yes |
| Peak data volume | Not applicable |
| Frequency | Ad hoc |

#### Recommended solution

This scenario that involves near-real-time data synchronization is best implemented by using dual-write.

1. The customer's information is sourced in a finance and operations app.
2. A customer calls customer service and asks to change their billing and shipping address information.
3. A customer service representative retrieves the customer's record in Dynamics 365 Customer Service.
4. The customer service representative updates the billing and shipping addresses, and saves the data.
5. The new billing and shipping addresses are synced back to the finance and operations app in real time.

### Sales representatives can change customer credit limits without signing in to a finance and operations app

A customer has a credit limit of $2,000 and wants to increase it to $5,000. This customer calls and requests the increase. The ticket is assigned to the sales department. The head of sales reviews the request, reviews the customer's payment history, and determines that the customer is eligible for an increased credit limit. The head of sales approves the request and responds to the ticket. The customer receives an email about the approval of the $5,000 credit limit.

| Decision | Information | 
|---------|--------------|
| Is real-time data required? | Yes |
| Peak data volume | Not applicable |
| Frequency | Ad hoc |

#### Recommended solution

This scenario is best implemented by using dual-write.

1. A customer calls and wants to increase their credit limit from $2,000 to $5,000.
2. A customer support representative creates a ticket in Dynamics 365 Customer Service.
3. The ticket is assigned to the sales unit.
4. A sales representative from the sales unit reviews and approves the request.
5. The customer's credit limit is increased to $5,000 in Dynamics 365 Sales.
6. The credit limit in the finance and operations app is updated to $5,000.
7. The sales representative responds to the ticket and resolves it.
8. The customer receives an email about the increased credit limit.

[!INCLUDE[footer-include](../../../includes/footer-banner.md)]

