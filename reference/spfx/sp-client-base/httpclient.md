# HttpClient class

_Implements: [`BasicHttpClient`](../sp-client-base/basichttpclient.md)_



HttpClient is used to perform REST calls against SharePoint. It adds default 
headers, manages the digest needed for writes, and collects telemetry that 
helps the service to monitor the performance of an application. 
 
For communicating with non-SharePoint services, use the BasicHttpClient 
class instead.


## Constructor


**Signature:** `constructor(serviceScope: ServiceScope)`

**Returns**: [`HttpClient`](../sp-client-base/httpclient.md)



#### Parameters


| Parameter	   | Type    | Description |
|:-------------|:---------------|:------------|
| `serviceScope`    | [`ServiceScope`](../sp-client-base/servicescope.md) |  |





## Methods

| Method	   | Access Modifier | Returns	| Description|
|:-------------|:----|:-------|:-----------|
|[`beginBatch`](#beginbatch)     | `public` | [`ODataBatch`](../sp-client-base/odatabatch.md) | Begins an ODATA batch,which allows multiple REST queries to be bundled into  a single web request. |
|[`fetch`](#fetch)     | `public` | [`Promise<Response>`](../es6-promise/promise.md) | Generally,the parameters and semantics for HttpClient.fetch() are essentially  the same as the WHATWG API standard that is documented here:  https://fetch.spec.whatwg.org/    The HttpClient subclass adds some additional behaviors that are convenient when  working with SharePoint ODATA API's (which can be avoided by using  BasicHttpClient instead):  - Default "Accept" and "Content-Type" headers are added if not explicitly specified.  - For write operations, an "X-RequestDigest" header is automatically added  - The request digest token is automatically fetched and stored in a cache, with  support for preloading    For a write operation, HttpClient will automatically add the "X-RequestDigest"  header, which may need to be obtained by issuing a seperate request such as  "https://example.com/sites/sample/_api/contextinfo". Typically the appropriate  SPWeb URL can be guessed by looking for a reserved URL segment such as "_api"  in the original URL passed to fetch(); if not, use IHttpClientOptions.webUrl  to specify it explicitly.   |
|[`get`](#get)     | `public` | [`Promise<Response>`](../es6-promise/promise.md) | Calls fetch(),but sets the method to 'GET'. |
|[`getWebUrlFromRequestUrl`](#getweburlfromrequesturl)     | `public, static` | `string` | This uses a heuristic to guess the SPWeb URL associated with the provided  REST URL. This is necessary for operations such as the X-RequestDigest  and ODATA batching, which require POSTing to a separate REST endpoint  in order to complete a request.  For excample, if the requestUrl is "/sites/site/web/_api/service",  the returned URL would be "/sites/site/web". Or if the requestUrl  is "http://example.com/_layouts/service", the returned URL would be  "http://example.com". |
|[`post`](#post)     | `public` | [`Promise<Response>`](../es6-promise/promise.md) | Calls fetch(),but sets the method to 'POST'. |





### beginBatch

Begins an ODATA batch,which allows multiple REST queries to be bundled into 
a single web request.

**Signature:** ``beginBatch(batchOptions?: IODataBatchOptions): ODataBatch``

**Returns**: [`ODataBatch`](../sp-client-base/odatabatch.md)



#### Parameters


| Parameter	   | Type    | Description |
|:-------------|:---------------|:------------|
| `batchOptions`    | [`IODataBatchOptions`](../sp-client-base/iodatabatchoptions.md) | _Optional._ |


### fetch

Generally,the parameters and semantics for HttpClient.fetch() are essentially 
the same as the WHATWG API standard that is documented here: 
https://fetch.spec.whatwg.org/ 
 
The HttpClient subclass adds some additional behaviors that are convenient when 
working with SharePoint ODATA API's (which can be avoided by using 
BasicHttpClient instead): 
- Default "Accept" and "Content-Type" headers are added if not explicitly specified. 
- For write operations, an "X-RequestDigest" header is automatically added 
- The request digest token is automatically fetched and stored in a cache, with 
support for preloading 
 
For a write operation, HttpClient will automatically add the "X-RequestDigest" 
header, which may need to be obtained by issuing a seperate request such as 
"https://example.com/sites/sample/_api/contextinfo". Typically the appropriate 
SPWeb URL can be guessed by looking for a reserved URL segment such as "_api" 
in the original URL passed to fetch(); if not, use IHttpClientOptions.webUrl 
to specify it explicitly. 


**Signature:** ``fetch(url: string,options: IHttpClientOptions): Promise<Response>``

**Returns**: [`Promise<Response>`](../es6-promise/promise.md)

a promise that will return the result

#### Parameters


| Parameter	   | Type    | Description |
|:-------------|:---------------|:------------|
| `url`    | `string` | - the URL to fetch |
| `options`    | [`IHttpClientOptions`](../sp-client-base/ihttpclientoptions.md) | - additional options that affect the request |


### get

Calls fetch(),but sets the method to 'GET'.

**Signature:** ``get(url: string,options?: IHttpClientOptions): Promise<Response>``

**Returns**: [`Promise<Response>`](../es6-promise/promise.md)

a promise that will return the result

#### Parameters


| Parameter	   | Type    | Description |
|:-------------|:---------------|:------------|
| `url`    | `string` | - the URL to fetch |
| `options`    | [`IHttpClientOptions`](../sp-client-base/ihttpclientoptions.md) | _Optional._- additional options that affect the request |


### getWebUrlFromRequestUrl

This uses a heuristic to guess the SPWeb URL associated with the provided 
REST URL. This is necessary for operations such as the X-RequestDigest 
and ODATA batching, which require POSTing to a separate REST endpoint 
in order to complete a request. 
For excample, if the requestUrl is "/sites/site/web/_api/service", 
the returned URL would be "/sites/site/web". Or if the requestUrl 
is "http://example.com/_layouts/service", the returned URL would be 
"http://example.com".

**Signature:** ``getWebUrlFromRequestUrl(requestUrl: string): string``

**Returns**: `string`

the inferred SPWeb URL

#### Parameters


| Parameter	   | Type    | Description |
|:-------------|:---------------|:------------|
| `requestUrl`    | `string` | The URL for a SharePoint REST service |


### post

Calls fetch(),but sets the method to 'POST'.

**Signature:** ``post(url: string,options: IHttpClientOptions): Promise<Response>``

**Returns**: [`Promise<Response>`](../es6-promise/promise.md)

a promise that will return the result

#### Parameters


| Parameter	   | Type    | Description |
|:-------------|:---------------|:------------|
| `url`    | `string` | - the URL to fetch |
| `options`    | [`IHttpClientOptions`](../sp-client-base/ihttpclientoptions.md) | - additional options that affect the request |
