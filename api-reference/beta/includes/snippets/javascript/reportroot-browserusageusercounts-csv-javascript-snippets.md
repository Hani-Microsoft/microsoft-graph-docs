---
description: "Automatically generated file. DO NOT MODIFY"
---

```javascript

const options = {
	authProvider,
};

const client = Client.init(options);

let stream = await client.api('/reports/browserUsageUserCounts(period='D7')/content')
	.version('beta')
	.get();

```