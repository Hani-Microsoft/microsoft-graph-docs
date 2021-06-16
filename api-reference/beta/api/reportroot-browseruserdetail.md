---
title: "reportRoot: browserUserDetail"
description: "Get a report that provides the details about which browser users have used."
localization_priority: Normal
ms.prod: "reports"
author: "sarahwxy"
doc_type: apiPageType
---

# reportRoot: browserUserDetail

Namespace: microsoft.graph

[!INCLUDE [beta-disclaimer](../../includes/beta-disclaimer.md)]

Get a report that provides the details about which browser users have used.

> **Note:** For details about different report views and names, see [Microsoft 365 reports - Microsoft browser usage](/microsoft-365/admin/activity-reports/browser-usage-report).

## Permissions

One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](/graph/permissions-reference).

| Permission type                        | Permissions (from least to most privileged) |
| :------------------------------------- | :------------------------------------------ |
| Delegated (work or school account)     | Reports.Read.All                            |
| Delegated (personal Microsoft account) | Not supported.                              |
| Application                            | Reports.Read.All                            |

> **Note:** For delegated permissions to allow apps to read service usage reports on behalf of a user, the tenant administrator must have assigned the user the appropriate Azure AD limited administrator role. For more details, see [Authorization for APIs to read Microsoft 365 usage reports](/graph/reportroot-authorization).

## HTTP request

<!-- { "blockType": "ignored" } --> 

```http
GET /reports/browserUserDetail(period='{period_value}')
```

## Function parameters

In the request URL, provide the following parameter with a valid value.

| Parameter | Type   | Description                                                                                                                                                                                                                                             |
| :-------- | :----- | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| period    | string | Specifies the length of time over which the report is aggregated. The supported values for {period_value} are: `D7`, `D30`, `D90`, and `D180`. These values follow the format D*n* where *n* represents the number of days over which the report is aggregated. |

> **Note:** You need to set either `period` in the URL.

## Optional query parameters

This method supports the `$format`, `$top`, and `$skipToken` [OData query parameters](/graph/query-parameters) to customize the response. The default output type is text/csv. However, if you want to specify the output type, you can use the OData `$format` query parameter to set the default output to text/csv or application/json.

## Request headers

| Name          | Description               |
| :------------ | :------------------------ |
| Authorization | Bearer {token}. Required. |

## Request body

Do not supply a request body with this method.

## Response

If successful, this method returns a `200 OK` response code and a [report](../resources/intune-shared-report.md) object in the response body. Report data is contained in the **content** property of the **report** object.

### CSV

If successful, requesting the **content** property returns a `302 Found` response that redirects to a preauthenticated download URL for the report. That URL can be found in the `Location` header in the response.

Preauthenticated download URLs are only valid for a short period of time (a few minutes) and do not require an `Authorization` header.

The CSV file has the following headers for columns:

- Report Refresh Date
- User Id
- Edge
- Edge Legacy
- Internet Explorer

### JSON

If successful, requesting the **content** property returns a `200 OK` response code and a JSON object in response body.

The default page size for this request is 200 items.

## Examples

### Example 1: CSV output

The following is an example that outputs CSV.

#### Request

The following is an example of the request to get the **content** property.



# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "reportroot_browserUserDetail"
}-->

```msgraph-interactive
GET https://graph.microsoft.com/beta/reports/browserUserDetail(period='D7')/content?$format=text/csv
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/reportroot-browseruserdetail-csv-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/reportroot-browseruserdetail-csv-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/reportroot-browseruserdetail-csv-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/reportroot-browseruserdetail-csv-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---



#### Response

The following is an example of the response.


<!-- { "blockType": "response" } --> 

```http
HTTP/1.1 302 Found
Content-Type: text/plain
Location: https://reports.office.com/data/download/JDFKdf2_eJXKS034dbc7e0t__XDe
```

Follow the 302 redirection and the CSV file that downloads will have the following schema.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "stream"
} -->

```http
HTTP/1.1 200 OK
Content-Type: application/octet-stream

Report Refresh Date,User Id, Report Period, Edge, Edge Legacy, Internet Explorer
```

### Example 2: JSON output

The following is an example that returns JSON.

#### Request

The following is an example of the request to get the **content** property.



# [HTTP](#tab/http)
<!-- {
  "blockType": "request",
  "name": "reportroot_browserUserDetail"
}-->

```msgraph-interactive
GET https://graph.microsoft.com/beta/reports/browserUserDetail(period='D7')/content?$format=application/json
```
# [C#](#tab/csharp)
[!INCLUDE [sample-code](../includes/snippets/csharp/reportroot-browseruserdetail-json-csharp-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [JavaScript](#tab/javascript)
[!INCLUDE [sample-code](../includes/snippets/javascript/reportroot-browseruserdetail-json-javascript-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Objective-C](#tab/objc)
[!INCLUDE [sample-code](../includes/snippets/objc/reportroot-browseruserdetail-json-objc-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

# [Java](#tab/java)
[!INCLUDE [sample-code](../includes/snippets/java/reportroot-browseruserdetail-json-java-snippets.md)]
[!INCLUDE [sdk-documentation](../includes/snippets/snippets-sdk-documentation-link.md)]

---



#### Response

The following is an example of the response.

> **Note:** The response object shown here might be shortened for readability.

<!-- {
  "blockType": "response",
  "truncated": true,
  "@odata.type": "stream"
} -->

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 304

{
  "@odata.nextLink": "https://graph.microsoft.com/beta/reports/browserUserDetail(period='D7')/content?$format=application/json&$skiptoken=D07uj",
   "value":[
      {
         "reportRefreshDate":"2021-04-17",
         "userId": "195C9BCCF6704E4CA3A0F5F4A4E6872B",
         "details":[
            {
               "reportPeriod":7,
               "edge":true,
               "edgeLegacy":true,
               "ie":false
            }
         ]
      }
   ]
}
```
<!-- uuid: 8fcb5dbc-d5aa-4681-8e31-b001d5168d79 
2015-10-25 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "Example",
  "keywords": "",
  "section": "documentation",
  "tocPath": "",
  "suppressions": [
  ]
}-->