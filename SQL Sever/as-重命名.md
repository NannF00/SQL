该命令用于重命名具有别名的列或表。AS

别名仅在查询期间存在。

![image](https://github.com/NannF00/SQL/assets/117897416/29c10b4b-2178-4a3c-b843-2e686707196c)


       SELECT
        doc.sCompany, 
        a.sCountryIso,
        com.sCompanyName,
        doc.nCustomer, 
        c.sMatchCode,
        c.sRegion,
        doc.sDocumentType, 
        doc.nDocNumber, 
        doc.dDocDate, 
        doc.sExecutive, 
        doc.fNetAmount, 
        (
            doc.fTaxAmount1 + 
            doc.fTaxAmount2 + 
            doc.fTaxAmount3 + 
            doc.fTaxAmount4 + 
            doc.fTaxAmount5
        )   AS 'fTaxSum', 
        doc.fGrossAmount, 
        cur.sAbbreviation
    FROM PUB.sBillingDocument AS doc
    LEFT JOIN PUB.xCompany    AS com ON doc.sCompany = com.sCompany
    LEFT JOIN PUB.bCustomer   AS c   ON doc.sCompany = c.sCompany   AND doc.nCustomer = c.nCustomer
    LEFT JOIN PUB.bCurrency   AS cur ON doc.sCompany = cur.sCompany AND doc.nCurrency = cur.nCurrency
    LEFT JOIN PUB.bAddress    AS a   ON doc.xidSenderAddress = a.xidAddress
    WHERE
        (
            doc.sCompany = '10' OR 
            doc.sCompany = '90' OR 
            doc.sCompany = '40' OR 
            doc.sCompany = '50' OR 
            doc.sCompany = '70'
        ) AND 
        doc.dDocDate >= @DateFrom AND 
        doc.dDocDate <= @DateTo AND 
        doc.sDocumentType = 'R'
