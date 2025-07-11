---
title: Migration to Planning Optimization for master planning
description: Learn about the new master planning engine, Planning Optimization, and about migration from the existing engine with an outline on new deployments. 
author: Henrikan
ms.author: henrikan
ms.reviewer: kamaybac
ms.search.form: 
ms.topic: how-to
ms.date: 06/17/2025
ms.custom: 
  - bap-template
---

# Migration to Planning Optimization for master planning

[!include [banner](../includes/banner.md)]

The built-in master planning engine is now obsolete (deprecated). It's being replaced by the Planning Optimization Add-in for Microsoft Dynamics 365 Supply Chain Management. This article provides information about the impact on new and existing deployments. It includes information about required actions.

Planning Optimization enables master planning calculations to occur outside Supply Chain Management and its Azure SQL database. The benefits that are associated with Planning Optimization include improved performance and minimized impact on the SQL database during master planning runs. Because quick planning runs can be done even during office hours, planners can immediately react to demand or parameter changes.

For more information about Planning Optimization, see [Master planning system architecture](master-planning-architecture.md).

## Obsolescence of the deprecated master planning engine

Microsoft has deprecated the built-in master planning engine in favor of Planning Optimization. This change affects all cloud environments. On-premises installations aren't affected.

For more information about the deprecated master planning engine, see the announcements in [Removed or deprecated features in Dynamics 365 Supply Chain Management](../get-started/removed-deprecated-features-scm-updates.md).

A deprecated feature is a feature that's no longer in active development and might be removed in a future release. For the deprecated master planning engine, there will be no new features, and support will be provided only for blocking issues (where master planning doesn't create any planned orders and/or continuously fails) and for regressions in the functionality. In March 2023, Microsoft adopted a strict policy against providing support for the deprecated master planning engine, except for blocking issues or regressions. These conditions apply to all customers, including the following types:

- Customers whose needs aren't yet fully supported by Planning Optimization.
- Customers who have received an exception so that they can continue to use the deprecated planning engine.
- All on-premises customers.

There's currently no timeline for full removal of the deprecated planning engine from Supply Chain Management. If Microsoft does make plans to remove it, we'll announce those plans 12 months before the removal date.

## New deployments

Planning Optimization is now the standard master planning engine and must be used for all new cloud deployments. Starting with Supply Chain Management version 10.0.32, the first time you enable planning processes for any legal entity, the system will require you to install and enable Planning Optimization if you haven't already done so.

Starting in Supply Chain Management version 10.0.41, the deprecated master planning engine is blocked for all new deployments. There's no manual way to enable the deprecated master planning engine for these environments. However, Microsoft customers who require planning support for the following feature will be permitted to use the deprecated master planning engine as a temporary solution until Planning Optimization supports it:

- Lean manufacturing

If you require support for lean manufacturing (only), submit a support ticket to Microsoft Support.

> [!NOTE]
> This is only a temporary solution until Planning Optimization supports lean manufacturing. No reason other than requiring lean manufacturing support will be considered for enabling deprecated planning on a new environment.

## Adding a new legal entity to an existing environment

When you add a new legal entity (company) to an existing environment, that company must use Planning Optimization. Starting with Supply Chain Management version 10.0.32, the first time you enable planning processes for any newly added legal entity, the system will require you to install and enable Planning Optimization if you haven't already done so.

You can continue to use the deprecated master planning engine for one or more previously created companies (until you're ready to migrate them) even while using Planning Optimization for the others. For instructions on how to set a company to use the deprecated master planning engine, see [Continue to use deprecated master planning with existing companies](continue-using-deprecated-planning.md).

> [!NOTE]
> Remember that you must still move each legal entity to Planning Optimization once they're supported.

## If you use kanban or are going live very soon and need time to test Planning Optimization

All new deployments and legal entities must use Planning Optimization from the beginning. However, if you have been preparing a new deployment for some time, and the functionality you needed wasn't yet supported by Planning Optimization while you were developing it, then you can still go live using the deprecated master planning engine for that deployment until you've had enough time to install and test Planning Optimization on it.

Planning Optimization doesn't yet support kanban, so if you need to use kanban, then you can go live using the deprecated planning engine for now. You should still plan to move to Planning Optimization as soon as kanban is supported.

## Existing deployments

Owners of existing cloud-based deployments that depend on master planning must plan to migrate to Planning Optimization. If your implementation depends on functionality that Planning Optimization doesn't currently support, you must request an exception to continue to use the deprecated master planning engine.

Starting in Supply Chain Management version 10.0.32, it's possible to allow some companies (legal entities) to run Planning Optimization while others continue to use the deprecated master planning engine until they're ready to be migrated. Therefore, Microsoft will now grant exceptions on a per-company basis. The exception only applies to existing companies&mdash;starting with version 10.0.32, all new companies that you add to your existing environment must use Planning Optimization. For instructions on how to set a company to use the deprecated master planning engine, see [Continue to use deprecated master planning with existing companies](continue-using-deprecated-planning.md).

We recommend that you migrate companies to Planning Optimization one at a time, as soon as they're supported.

## Migration recommendations

There are several differences between the deprecated master planning engine and Planning Optimization.

For distribution companies, the two planning engines provide very similar feature sets. Based on our experience helping other customers migrate, we recommend that distribution companies enable and test Planning Optimization in a test environment, and then, when testing is successful, enable it in a production environment.

Manufacturing companies might be affected by some of the minor architectural differences that exist between Planning Optimization and the deprecated planning engine. Based on our experience helping other customers migrate, we recommend that you set up a test environment and proceed in the following way:

1. Create two testing plans, one for Planning Optimization and the other for the deprecated planning engine. Use the same settings for both plans.
1. While the deprecated planning engine is enabled, run the plan that you created for it.
1. Enable Planning Optimization, and run the plan that you created for it.
1. For each plan, export the planned orders to an Excel file.
1. For each plan, sum the planned order quantities for each of several regular periods (for example, every month).
1. Compare the quantities for each plan to make sure that the result is the same (or very similar). Some variation can be expected for orders that occur at the start or end of a period.
1. If your test is successful, continue testing on the test environment.
1. If all of your tests are successful, enable Planning Optimization in your production system.

## Exception process for version 10.0.32 and later

As of Supply Chain Management version 10.0.32, the process of evaluating your system and moving to Planning Optimization is fully automated. The system will analyze your setup and automatically show you the correct instructions for your situation and for each company (legal entity). The following subsections provide details about the possible cases.

### Deployments where Planning Optimization supports all required features

If the system detects that all the relevant features that you're using are supported by Planning Optimization, but you're still running the deprecated planning engine, it will ask you to migrate. The next time that you manually run master planning, the system will show the following message:

> You are supported to use the non-deprecated and faster master planning (Planning Optimization).
>
> We need you to provide some information regarding master planning.
>
> Do you have customizations on the master planning engine?

The following screenshot shows how the message looks.

[<img src="media/exception-process-dialog.png" alt="The Exception process dialog." title="The Exception process dialog" width="720" />](media/exception-process-dialog.png#lightbox)

If you haven't customized the master planning engine for this deployment, you must migrate to Planning Optimization. If you require some more time to test and migrate, select the time that you'll require. The system will automatically apply an exception for the selected time.

If you do have customizations, you must move them to the existing extensibility point. Learn more in [Planning Optimization extensibility](../supply-chain-dev/extensibility.md).

### Deployments requiring features not yet supported by Planning Optimization

If the system detects that you're using features that aren't supported by Planning Optimization, it will show the following message the next time that you manually run master planning:

> You are not supported yet to use the non-deprecated master planning (Planning Optimization). We expect to be supporting you in the coming future. When you are supported, you will be asked to move to Planning Optimization. If you have customizations on the master planning engine, you can already start evaluating them and preparing to move them to the [Planning Optimization extensibility point](../supply-chain-dev/extensibility.md).

This message informs you that you should start planning to move to Planning Optimization as soon as it supports the features that you're using. Therefore, you should evaluate any customizations that you've made to the deprecated planning engine, plan to move them to the existing extensibility point (see [Planning Optimization extensibility](../supply-chain-dev/extensibility.md)), and take other actions to prepare for the migration (for example, by contacting your Microsoft partner or consultant).

For information about which features are already supported and estimates about when each feature will become available for Planning Optimization, see [Planning Optimization fit analysis](planning-optimization/planning-optimization-fit-analysis.md).

If you have already received an exception, it will remain in place until Planning Optimization supports the features that you require.

### <a name="unsupported-environments"></a>Environments that don't support Planning Optimization

Regardless of the features that you're using, to use Planning Optimization, you must be running Supply Chain Management version 10.0.7 or later in a tier 2 or higher high-availability environment that's Microsoft Dynamics Lifecycle Services–enabled. The environment must **not** be a OneBox environment. If you try to install the add-in in a OneBox environment, the installation won't be completed, and you'll have to cancel it.

If your environment doesn't support Planning Optimization, you'll receive the following message:

> You can only run deprecated master planning in this environment. If you would like to get an environment that supports non-deprecated planning (Planning Optimization) please follow the instructions: [Get started with master planning](planning-optimization/get-started.md)

If you're a Microsoft partner or independent software vendor (ISV), you can obtain, at a reduced price, a nonproduction environment that supports Planning Optimization, and that includes Microsoft business applications and demo data. These environments are available only to partners and ISVs, and they can be used only on partner tenants, never on customer tenants. You can use the environment that you obtain to learn how Planning Optimization works, test your solutions while you're using it, and deliver end-to-end customer demos. To request a license, go to the [partner sandbox request page](https://experience.dynamics.com/requestlicense/).

## Frequently asked questions about migration

### What impact does Planning Optimization have on current planning users?

Users will still work in the same module and use the same pages to initiate planning and review planned orders. The only visible difference will be that the processing window shows **Run Planning Optimization**.

### If I'm running classic planning in a batch job, do I have to update this job when I enable Planning Optimization?

Yes, you'll have to set up a new batch job to run Planning Optimization instead of classic master planning.

### If I'm running deprecated planning in some companies and Planning Optimization in others, can I use intercompany master planning?

Yes. Although the intercompany master planning page isn't supported, you can achieve the same effect by scheduling sequential batch jobs to run planning for the different companies in their desired order. Use the Planning Optimization batch job for the companies that are running Planning Optimization (*Planning Optimization* task) and the deprecated engine for the others (*Master planning* task).

To use intercompany master planning for different companies that use Planning Optimization, the process is the same: schedule Planning Optimization tasks as batch jobs the run sequentially.

### How much will my performance improve when I move to Planning Optimization?

There's no specific rule about how much your performance will improve. In general, companies that run with large datasets and are already experiencing performance issues with deprecated master planning will see the biggest improvement. The best way to find out is to test Planning Optimization.

### Does it cost extra to use Planning Optimization?

No, it's included in your Supply Chain Management license. There are no extra costs.

### Can I run Planning Optimization in a Government Community Cloud (GCC) environment?

Yes, Planning Optimization is supported in Government Community Cloud (GCC) environments now that GCC is compatible with the Microsoft Dynamics Lifecycle Services microservices framework.

### Can I run Planning Optimization in a tier-1 environment?

No, Planning Optimization runs via a Lifecycle Services add-in that can be installed only in tier-2 or higher environments.

### What data center does Planning Optimization run on?

Planning Optimization runs on the same data center as your Supply Chain Management environment.

### I'm a partner, and I want to demo or test Planning Optimization. How can I do that?

For partners and independent software vendors (ISVs), Microsoft offers a special license for accessing tier-2 environments. For details, see [\[ISV\] Request License](https://experience.dynamics.com/requestlicense/).

### I'm going live with version 10.0.32 or higher, but Planning Optimization doesn't yet have all the features I need. Can I go live using the deprecated planning engine for now?

Yes. When you start using the planning features, the system will ask you to install and enable Planning Optimization because this has been mandatory since Supply Chain Management version 10.0.32. However, if one or more of your companies isn't yet ready to use Planning Optimization, you can exclude them from running Planning Optimization by going to the **Planning Optimization parameters** page. For instructions, see [Continue to use deprecated master planning with existing companies](continue-using-deprecated-planning.md).

### How do I request an exception to continue using the deprecated planning engine on version 10.0.32 or higher?

The system will automatically give you an opportunity to request an exception. Just fill out the dialogs when prompted. The exception will then be applied automatically in the background.

### Why do I get an error message when running the deprecated master planning engine?

You might sometimes get an error message when running the deprecated master planning engine. It indicates that you must move to Planning Optimization and provides the following information:

> The built-in master planning engine is deprecated. This means that it is not supported (unless a blocking issue) and it will no longer be invested in. It's being replaced by the Planning Optimization Add-in for Microsoft Dynamics 365 Supply Chain Management.

For information about how to migrate to Planning Optimization, see the earlier sections of this article.

You can continue using the deprecated master planning engine for one or more of your companies if necessary. For instructions, see [Continue to use deprecated master planning with existing companies](continue-using-deprecated-planning.md).

If you see this error while running on a sandbox and you'd like to remove it, follow the instructions provided in [Can I use the deprecated master planning engine on my sandbox environment?](#faq-sandbox)

### <a name="faq-sandbox"></a>Can I use the deprecated master planning engine on my sandbox environment?

Yes. Even if you receive the error message described in the answer to the previous question on a sandbox environment, the deprecated master planning engine will still run successfully. However, if the error message disturbs you, you can disable it on an IaaS (not Service Fabric) sandbox environment by running the following query on your database:

```sql
-- Insert or update an enabled flight:
DECLARE @flightName NVARCHAR(100) = 'ReqPlanningOptimizationExceptionToggle';
IF NOT EXISTS (SELECT TOP 1 1 FROM SysFlighting WHERE flightName = @flightName)
    INSERT INTO SYSFLIGHTING(FLIGHTNAME,ENABLED, FLIGHTSERVICEID,PARTITION)
    SELECT @flightName, 1, 12719367,RECID FROM DBO.[PARTITIONS];
ELSE
    UPDATE SysFlighting SET enabled = 1, flightServiceId = 12719367 WHERE flightName = @flightName;
```

### My environment is on-premises. Do I need an exception to continue using the deprecated master planning engine?

No. An exception isn't required for on-premises environments. You can continue to use the deprecated master planning engine. Your environment admin will be informed if any action is required.

### We use planned production orders, but I'm concerned about what will happen when we upgrade to version 10.0.16. Should I take any action?

You shouldn't be concerned. You can continue to use the deprecated master planning engine in version 10.0.16. However, we recommend that you evaluate whether migration to Planning Optimization can start with the current functionality. We also recommend that you remain informed about new functionality.

### I'm getting an error message when running master planning. Is master planning blocked?

If you're running version 10.0.16 or later, you might receive the following error message when you run master planning:

> You receive this error message because the deprecated master planning engine was used for scenarios supported by Planning Optimization. You should migrate to Planning Optimization now, as the built-in master planning engine has been deprecated. Note that this master planning run did complete successfully.
>
> In case your migration has strong dependencies on pending features, an exception to continued usage of the deprecated master planning engine can be requested.
>
> Please complete the following questionnaire to get started and if relevant request exception from migration to Planning Optimization.

Master planning isn't blocked. Your master planning run was successfully completed, and you can use the result in the usual way. However, to avoid receiving this error message during future master planning runs, you must either migrate to Planning Optimization immediately or request an exception by using the link in the error message.

[!INCLUDE[footer-include](../../includes/footer-banner.md)]
