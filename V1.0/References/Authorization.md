# Authorization Reference

The Authorization Message is the method a company has to formalize its "attorney" to act on their behalf and perform transactions with a Trading Partner.

> Please see the ANVISA´s Attorney reference.

### Fields of the Message

|Field|Description|Data Type|Sample|Note|
|-----|-----------|---------|------|----|
|id|The Message ID|Alphanumeric String|123456978696050595050AAAABBBDDDDD| The ID has to be unique for the Trading Partner|
|date|Message Generation Date|Datetime with Timezone|2021-10-03T22:06:45Z| The date reference is always defined as GMT-0|
|schemaVersion|The version of the GS1 HC Schema used|Double|1.0||
|expireDate|Authorization Expiration Date|Datetime with Timezone|2021-12-01T00:00:00Z|The Authorization will be valid till this date|
|sender|Partner that is giving the Authorization|Partner (see XSD)|```<sender><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></sender>```||
|partnerAttorney|Partner that is allowed to use the Authorization|Partner (see XSD)|```<partnerAttorney><partnerKey>CNPJ</partnerKey><partnerValue>15041786000176</partnerValue></partnerAttorney>```||

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<AttorneyAuthorization id="123456978696050595050AAAABBBDDDDD" date="2021-10-03T22:06:45Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <expireDate>2021-12-01T00:00:00Z</expireDate>
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15041786000176</partnerValue>
    </sender>
    <partnerAttorney>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15041786000176</partnerValue>
    </partnerAttorney>
</AttorneyAuthorization>
```
