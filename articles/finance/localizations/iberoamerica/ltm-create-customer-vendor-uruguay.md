---
title: Create customer and vendor records with an address in Uruguay
description: Learn how to set up records for customers and vendors in Uruguay, including prerequisites and an outline on creating a record for a customer.
author: Cpicon85
ms.author: v-cpicon
ms.topic: how-to
ms.date: 12/08/2023
ms.custom: bap-template
ms.reviewer: johnmichalak
---

# Create customer and vendor records with an address in Uruguay

The Uruguayan customer and vendor configuration contains the fiscal information that's required by the fiscal authorities. It also includes a reference to the document classes that can be used in transactions with customers and vendors.

## Prerequisites

Before you create records for customers and vendors who are located in Uruguay, the following setup must be completed:

- Create departments and counties from Uruguay by using states and counties from the address setup.
- Create tax codes for the value-added tax (VAT) that will be used (VAT general rate, exempt, and so on).
- Create sales tax groups that contain the tax codes that you created.
- Create item sales tax groups that contain the tax codes that you created.
- Create document classes to use with customer and vendor invoices, credit notes, debit notes, packing slips, and so on. For more information, see [Configure sales and purchase invoices for Uruguay](ltm-configure-invoices-Uruguay.md).
- Create a customer and vendor set that contains all the document classes that will be used.
- Create a tax ID for each type of tax identification that your customers and suppliers have.
- Create a taxpayer type for each type of taxpayer that your customers and suppliers have.

## Create a record for a customer in Uruguay

1. Go to **Accounts receivable** \> **Customers** \> **All customers**, and select **New**.
2. In the **Type** field, select **Organization**.
3. In the **Customer group** field, select a local group.
4. In the **Address** section, select **New**, and provide a name for the address.
5. In the **Country/region** field, select **Uruguay**.
6. Enter the street and street number.
7. Select a state, county, and city, and mark the address as primary.
8. In the **Contact information** section, select **New** to create a record for the company phone number.
9. In the **Sales demographic** section, set the currency to **UYU** (Uruguayan peso).
10. Configure the terms of payments and the invoice account.
11. Set the delivery terms, mode of delivery, and delivery reason.
12. Select a sales tax group that contains all the tax codes that can have transactions with this customer.
13. In the **LATAM** section, enter the following information:

    - In the **Customer set** field, select a set that contains the document classes to use with the customer.
    - In the **Taxpayer type** field, select a taxpayer that represents an organization. For example, select **persona juridica**.
    - In the **Based in country/region** field, select **Uruguay**.
    - In the **Country document type** field, select a tax ID type. For example, select **RUT** (tax identification).
    - Complete the **Country document number** field with the customer's tax ID number.

## Create a record for a vendor in Uruguay

1. Go to **Accounts payable** \> **Vendors** \> **All vendors**, and select **New**.
2. In the **Type** field, select **Organization**.
3. In the **Vendor group** field, select a local group.
4. In the **Address** section, select **New**, and provide a name for the address.
5. In the **Country/region** field, select **Uruguay**.
6. Enter the street and street number.
7. Select a state, county, and city, and mark the address as primary.
8. In the **Contact information** section, select **New** to create a record for the company phone number.
9. In the **Sales demographic** section, set the currency to **UYU**.
10. Configure the terms of payments and the invoice account.
11. Set the delivery terms, mode of delivery, and delivery reason.
12. Select a sales tax group that contains all the tax codes that can have transactions with this vendor.
13. In the **LATAM** section, enter the following information:

    - In the **Vendor set** field, select a set that contains the document classes to use with the vendor.
    - In the **Taxpayer type** field, select a taxpayer that represents the organization. For example, select **persona juridica**.
    - In the **Based in country/region** field, select **Uruguay**.
    - In the **Country document type** field, select a tax ID type. For example, select **RUT**.
    - Complete the **Country document number** field with the vendor's tax ID number.
