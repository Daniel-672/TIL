### - DynamoQuery

```html
<!-- 
  Copyright 2010-2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.
 
  This file is licensed under the Apache License, Version 2.0 (the "License").
  You may not use this file except in compliance with the License. A copy of
  the License is located at
 
  http://aws.amazon.com/apache2.0/
 
  This file is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR
  CONDITIONS OF ANY KIND, either express or implied. See the License for the
  specific language governing permissions and limitations under the License.
-->
<html>
<head>
<script src="https://sdk.amazonaws.com/js/aws-sdk-2.7.16.min.js"></script>

<script>
AWS.config.update({
  region: "ap-northeast-2",
  // endpoint: 'http://localhost:8000',
  // accessKeyId default can be used while using the downloadable version of DynamoDB. 
  // For security reasons, do not store AWS Credentials in your files. Use Amazon Cognito instead.
  accessKeyId: "",
  // secretAccessKey default can be used while using the downloadable version of DynamoDB. 
  // For security reasons, do not store AWS Credentials in your files. Use Amazon Cognito instead.
  secretAccessKey: ""
});


var docClient = new AWS.DynamoDB.DocumentClient();

function queryData() {
    document.getElementById('textarea').innerHTML += "1bd90b17-95fa-4105-bf39-125bed3ece2b";

    var params = {
        TableName : "faceTable-dev",
        IndexName : "userIdcreatedAt",
        KeyConditionExpression: "#userId = :userId and begins_with(#ent, :EN)",
        ExpressionAttributeNames:{
            "#userId": "userId",
            "#ent": "createdAt"
        },
        ExpressionAttributeValues: {
            ":userId":'1bd90b17-95fa-4105-bf39-125bed3ece2b',
            ":EN":"2020-12-15 12:59:4"
        }
    };


//    var params = {
//        TableName : "faceTable-dev",
//        IndexName : "createdAt",
//    };

    docClient.query(params, function(err, data) {
        if (err) {
            document.getElementById('textarea').innerHTML += "Unable to query. Error: " + "\n" + JSON.stringify(err, undefined, 2);
        } else {
            document.getElementById('textarea').innerHTML += "Querying for : " + "\n" + JSON.stringify(data, undefined, 2);
        }
    });
}

</script>
</head>

<body>
<input id="queryData" type="button" value="Query" onclick="queryData();" />
<br><br>
<textarea readonly id= "textarea" style="width:400px; height:800px"></textarea>

</body>
</html> 
```

