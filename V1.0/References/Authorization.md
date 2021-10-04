# Authorization Reference

The Authorization Message is a way to expose to a Trading Partner the authorization to perform transactions on benhalf of another.

> Please see the ANVISA´s Attorney reference.

### Fields of the Message

|Field|Description|Data Type|Sample|Note|
|-----|-----------|---------|------|----|
|id|The id of the Message|Alphanumeric String|123456978696050595050AAAABBBDDDDD| The ID have to be unique inside the Trading Partner|
|date|The date of the Message Generation|Datetime with Timezone|2021-10-03T22:06:45Z| The date reference is always defined with GMT-0|
|schemaVersion|The version of the GS1 HC Schema used|Double|1.0||
|expireDate|The expire date of this Authorization|Datetime with Timezone|2021-12-01T00:00:00Z|The Authorization will be valid until this date|
|partnerFrom|Partner that is generating this Authorization|Partner (see XSD)|```<partnerFrom><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></partnerFrom>```||
|partnerAttorney|Partner that is allowed to use this Authorization|Partner (see XSD)|```<partnerAttorney><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></partnerAttorney>```||

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<AttorneyAuthorization id="123456978696050595050AAAABBBDDDDD" date="2021-10-03T22:06:45Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <expireDate>2021-12-01T00:00:00Z</expireDate>
    <partnerFrom>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15041786000176</partnerValue>
    </partnerFrom>
    <partnerAttorney>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15041786000176</partnerValue>
    </partnerAttorney>
</AttorneyAuthorization>
```