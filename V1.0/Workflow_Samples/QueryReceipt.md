# QueryMessage Sample

Following the previous workflow samples, in this section, we will explain how to query a trading partner webservice to retrieve the processing results.

In this hypothetical scenario, a manufacturer has the CNPJ 15042274000195 and its trading partner (distributor) has the CNPJ 83042274000167.

The manufacturer wants to know how messages need to be sent to the distributor’s webservice.

- Sender - CNPJ 15042274000195 (Manufacturer)
- Receiver - CNPJ 83042274000167 (Distributor)

> Just be aware that the messages 
> in this example do not have 
> the SIGNATURE tags

### Communication flow

![image info](../images/getPreferences.jpg)

Based on the scenario above, the manufacturer will call the getMessage method in the distributor’s webservice.

To perform this operation, a QueryRequest message has to be created and sent through the manufacturer’s webservice.

### Creating the QueryRequest

```xml
<?xml version="1.0" encoding="UTF-8"?><QueryRequest xmlns="http://hc.gs1br.org.br/" date="2021-09-27T06:13:29Z" id="123456978696050595050AAAABBBDDDDD" schemaVersion="1.0">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
    	   <partnerKey>CNPJ</partnerKey>
        <partnerKey>83042274000167</partnerKey>
    </receiver>
    <queryRequestItem>
        <parameterKey>sender.Key</parameterKey>
        <parameterValue>CNPJ</parameterValue>
    </queryRequestItem>
    <queryRequestItem>
        <parameterKey>sender.Value</parameterKey>
        <parameterValue>15042274000195</parameterValue>
    </queryRequestItem>
	<queryRequestItem>
        <parameterKey>receiver.Key</parameterKey>
        <parameterValue>CNPJ</parameterValue>
    </queryRequestItem>
    <queryRequestItem>
        <parameterKey>receiver.Value</parameterKey>
        <parameterValue>83042274000167</parameterValue>
    </queryRequestItem>
    <queryRequestItem>
        <parameterKey>receipt.id</parameterKey>
        <parameterValue>01919199103294949</parameterValue>
    </queryRequestItem>
</QueryRequest>
```

The Distributor webservice will answer with the list of the errors.

> if the manufacturer receives a message with 0 errors.

### QueryResponse with Message

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<QueryResponse id="123456978696050595050AAAABBBDDDDD" date="2021-10-06T12:52:01Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
    <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
    	   <partnerKey>CNPJ</partnerKey>
        <partnerKey>83042274000167</partnerKey>
    </receiver>
    <response>
        <message>
            <messageCode>9999</messageCode>
            <messageDescription>Message Received</messageDescription>
        </message>
    </response>
</QueryResponse>
```

### QueryResponse with Error

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<QueryResponse id="123456978696050595050AAAABBBDDDDD" date="2021-10-06T12:52:01Z" schemaVersion="1.0" xmlns="http://hc.gs1br.org.br/">
   <sender>
        <partnerKey>CNPJ</partnerKey>
        <partnerValue>15042274000195</partnerValue>
    </sender>
    <receiver>
    	   <partnerKey>CNPJ</partnerKey>
        <partnerKey>83042274000167</partnerKey>
    </receiver>
    <response>
        <error>
            <errorCode>400</errorCode>
            <errorDescription>Unable to process</errorDescription>
        </error>
    </response>
</QueryResponse>
```