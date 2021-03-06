# Import.UploadClassifications

Submits SAINT classification data for a Data Connectors integration on behalf of a client.

Individual data blocks can contain no more than 10,000 data rows \(to keep the HTTP POST below 10MB\), so you might need to break up data submissions into multiple data blocks.

## Import.UploadClassifications Parameters

|Parameter|Type|Required|Description|
|---------|----|--------|-----------|
|**integrationCode** |`xsd:string` | Yes| The integration identifier. Call [Partner.GetIntegrationAccess](r_getIntegrationAccess.md#) to get this value.|
|**metricName** | | | The name of the metric where you want to import classification data.

 The metric must be a previously defined variable mapping that is available by calling [Product.GetVariableMappings](../config_api/r_prod_getVarMappings.md#).|
|**columnNames** |[colArray](../../data_types/r_datatype_colArray.md#) | Yes| The names of the classification columns \(the column heading\).

 There must be at least 2 `<item>` elements nested inside this parameter. The first must be `Key`. All others must be valid classifications created through the Product Script \(see [Product.GetProductScript](../config_api/r_prod_getProductScript.md#)\).|
|**rows** |[rowArray](../../data_types/r_datatype_rowArray.md#) | Yes| The classification data to import.

 The `rows` element should contain the same number of columns as specified in the `columnNames` parameter.|
|**endOfBlock** |`xsd:string` | No| A value of 1 indicates that this is the last block in the data submission. A value of 0 indicates that additional data will be sent.

 To indicate the end of a data block, pass the following:

`<endOfBlock>1</endOfBlock>.` To indicate that additional data will be sent, pass the following:

`<endOfBlock>0</endOfBlock>.` If you pass an `endOfBlock` with a value of `0`, you must call [Import.ContinueClassificationsUpload](r_continueClassificationsUpload.md#) to resume uploading.|

## Import.UploadClassifications Response

|Response|Type|Description|
|--------|----|-----------|
|**status** |`xsd:string` | Indicates if the call was successful. Valid return values include `Failed` or `Success`.

 If the call fails, Data Connectors returns an error message to help you understand why the call failed.|
|**blockId** |`xsd:int` | The ID used to append additional data blocks to this Data Connectors classifications submission.

 This parameter is assigned a value only when the request does not include the `<endOfBlock/>` tag.|
|**fileId** |`xsd:int` | The unique ID generated by the Processing Queue to identify a particular Data Connectors classifications submission.

 This parameter is assigned a value only when the request does not include the `<endOfBlock/>` tag.|

**Parent topic:** [Data Connectors Integration API](../../Genesis_API/integration_api/c_genesis_api_integrate.md)

