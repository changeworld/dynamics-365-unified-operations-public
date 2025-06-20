---
title: VAT statement details for Latvia
description: Learn how to set up the VAT statement for legal entities in Latvia in Microsoft Dynamics 365 Finance.
author: liza-golub
ms.author: egolub
ms.topic: how-to
ms.custom: 
  - bap-template
ms.date: 05/29/2025
ms.reviewer: johnmichalak
ms.search.region: Latvia
ms.search.validFrom: 2016-11-30
ms.search.form: TaxAuthority, TaxReportCollection, TaxReportVoucher, TaxTable
---

# VAT statement details for Latvia

[!include [banner](../../includes/banner.md)]

This article explains how to set up the VAT statement for legal entities in Latvia in Microsoft Dynamics 365 Finance.

> [!NOTE]
> This feature has been replaced with the value-added tax (VAT) declaration functionality. For more information, see [VAT declaration (Latvia)](emea-lva-vat-declaration-latvia.md).

This article includes country/region-specific information about the setup of the value-added tax (VAT) statement for legal entities in Latvia only. For more information about the implementation of VAT statements, see [VAT reporting for Europe](../europe/emea-vat-reporting.md).

## Set up the report layout for sales tax authorities

To generate a VAT declaration in the required format for the appropriate tax authority, you must set up the report layout for sales tax authorities. 

To set up the report layout for sales tax authorities, follow these steps.

1. In Dynamics 365 Finance, go to the **Sales tax authorities** page.
1. Set the **Report layout** field value to **Default**.
1. Select the same sales tax authority for the sales tax settlement period that is used for the sales tax codes.

## Set up sales tax reporting codes

Here is an example that shows how you might set up sales tax reporting codes on the **Report setup** FastTab of the **Sales tax codes** page to generate a VAT statement.

| Sales tax reporting code | Description (English)                                                                    | Description                                                                              | XML tag name |
|--------------------------|------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------|--------------|
| 41                       | Standard rate tax amount                                                                 | Ar standartlikmi apliekamie darījumi                                                     | R41          |
| 411                      | Domestic transactions for which the recipient of the goods or services pays the tax      | Iekšzemē veiktie darījumi, par kuriem nodokli maksā preču vai pakalpojumu saņēmējs       | R411         |
| 42                       | Reduced rate tax amount                                                                  | Ar samazināto likmi apliekamie darījumi                                                  | R42          |
| 45                       | Goods that are delivered to European Union (EU) member states                            | Uz ES dalībvalstīm piegādātās preces                                                     | R45          |
| 46                       | Amount of custom sales in stock                                                          | Ārpuskopienas preču piegādes muitas noliktavās un brīvajās zonās                         | R46          |
| 47                       | New vehicles delivered to EU countries/regions                                                   | Uz ES dalībvalstīm piegādātie jaunie transportlīdzekļi                                   | R47          |
| 48                       | Provided services                                                                        | Par sniegtajiem pakalpojumiem                                                            | R48          |
| 481                      | Export goods                                                                             | Eksportētās preces                                                                       | R48\_1       |
| 482                      | The transactions other countries/regions                                                         | Citās valstīs veiktie darījumi                                                           | R48\_2       |
| 49                       | Not taxable transactions                                                                 | Ar PVN neapliekamie darījumi                                                             | R49          |
| 50                       | Goods and services that are received from EU member states(standard rate)                | No ES dalībvalstīm saņemtās preces un pakalpojumi (standartlikme)                        | R50          |
| 51                       | Goods and services that are received from EU member states (reduced rate)                | No ES dalībvalstīm saņemtās preces (samazinātā likme)                                    | R51          |
| 54                       | Received services                                                                        | Par saņemtajiem pakalpojumiem                                                            | R54          |
| 61                       | Imported goods for the company's economic activities                                     | Par importētajām precēm                                                                  | R61          |
| 62                       | Domestic goods and services for the company's economic activities                        | Par precēm un pakalpojumiem iekšzemē                                                     | R62          |
| 63                       | Calculated tax prepayment                                                                | Aprēķinātā PVN summa saskaņā ar likuma 92.panta pirmās daļas 4.punktu (izņemot 64.rindu) | R63          |
| 64                       | Calculated tax prepayment for goods and services that are received from EU member states | Aprēķinātā PVN summa par precēm un pakalpojumiem, kas saņemti no ES dalībvalstīm         | R64          |
| 65                       | The compensation paid to farmers                                                         | Lauksaimniekiem izmaksātā kompensācija                                                   | R65          |
| 66                       | Not payable tax prepayment                                                               | PVN summa, kas nav atskaitāma kā priekšnodoklis                                          | R66          |
| 67                       | Tax amount reduction calculated for previous tax periods                                 | Iepriekšējos taksācijas periodos samaksai valsts budžetā aprēķinātā nodokļa samazinājums | R67          |
| 57                       | Calculated prepayment tax amount reduction for previous tax periods                      | Iepriekšējos taksācijas periodos atskaitītā priekšnodokļa samazinājums                   | R57          |

## Configure the electronic reporting model and format for the report

To configure the electronic reporting model and format for the report, follow these steps.

1. To review or change the VAT statement configuration, In Dynamics 365 Finance, go to the **Reporting configurations** page.
1. In the list of models, select **VAT declaration model**.
1. Select **Designer** to review or change the model.
1. To review or change the VAT statement format, on the **Reporting configurations** page, select **VAT declaration (LV)**, and then select **Designer**.

## Generate a VAT statement

To generate a VAT statement, follow these steps.

1. To generate a VAT XML file, in Dynamics 365 Finance, go to the **Sales tax payments** page.
2. Select one or more vouchers, and then select **Export VAT XML file**.





[!INCLUDE[footer-include](../../../includes/footer-banner.md)]
