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
<textarea readonly id= "tarea" style="width:400px; height:800px"></textarea>

</body>
</html> 
```



### - DynamoQuery 후 점수

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
    document.getElementById('textarea').innerHTML += "";

    var params = {
        TableName : "faceTable-dev",
        IndexName : "userIdcreatedAt",
        KeyConditionExpression: "#userId = :userId and begins_with(#ent, :EN)",
        ExpressionAttributeNames:{
            "#userId": "userId",
            "#ent": "createdAt"
        },
        ExpressionAttributeValues: {
            ":userId":'1f8e09da-d014-42a1-bf03-7e5566aca0c4',
            ":EN":"2020-12-16 04:40:2"
        }
    };


//    var params = {
//        TableName : "faceTable-dev",
//        IndexName : "createdAt",
//    };
    var adata = new Array();
    docClient.query(params, function(err, data) {
        if (err) {
            document.getElementById('textarea').innerHTML += "Unable to query. Error: " + "\n" + JSON.stringify(err, undefined, 2);
        } else {
            
            document.getElementById('textarear').innerHTML += "========== 가감스코어 =========" + "\n" + getScore(data);
            document.getElementById('textarea').innerHTML += "========== raw data =========" + "\n" + JSON.stringify(data, undefined, 2);
        }
    });
}


function getScore(data) {
    var idealLogCount = 1 * 5 * 10              // 1초 * 5개 * 10초 = 50개 (1분: 300개, 5분: 1500개)
    var blinkOffSet = 0.03;                      // 두눈이 0.03 이하일 경우 감은 것 (테스트용)
    var neutralOffSet = 0.8;                    // neutral이 0.8 이상
    var blinkBaseOffSet = idealLogCount * 0.5   // 예상했던 로그수의 반이상이 잡힐 때만, 25개 이상의 log가 잡힐 경우만 졸림을 감지

    var logArray = data.Items                   // 대상 로그 배열
    var logCount = logArray.length              // 추출된 로그수
    var blinkCount = 0;                         // 두눈이 모두 감은 경우
    var neutralCount = 0;                       // neutral이 0.8이상인 로그수
    var returnScore = 0;                        // 최종 가감 스코어

    for (i = 0; i < logCount; i++) {            // 로그 개수 만큼돌면서 변수 계산

        if (logCount >= blinkBaseOffSet && parseFloat(logArray[i].left_eye_blink) <= blinkOffSet && 
            parseFloat(logArray[i].right_eye_blink) <= blinkOffSet) {           // log수가 50%이상 잡히고 두눈을 감은 경우만 
            // console.log(logArray[i].left_eye_blink, logArray[i].right_eye_blink)
            blinkCount += 1;
        }
        if (parseFloat(logArray[i].neutral) >= neutralOffSet) {                 // 일단 neutral만
            neutralCount += 1;
        } 
    }

    if (logCount >= blinkBaseOffSet && blinkCount >= blinkBaseOffSet * 0.8) {    // 졸음 감점 시 화면집중과 안면집중 점수는 적용되지 않음 (1분 졸면 -12 급경히 감소)
        returnScore =- 2;
    } else {
        returnScore = (logCount / idealLogCount) - ((idealLogCount - logCount) / idealLogCount) + (neutralCount / idealLogCount);
    }

    console.log("idealLogCount -> " + idealLogCount);
    console.log("logCount -> " + logCount);
    console.log("blinkCount -> " + blinkCount);
    console.log("neutralCount -> " + neutralCount);
    console.log("blinkScore -> " + (blinkCount == logCount));
    console.log("logCount/idealLogCount -> " + (logCount / idealLogCount));
    console.log("logCount/idealLogCount -> " + '-' + ((idealLogCount - logCount) / idealLogCount));
    console.log("neutralCount/idealLogCount -> " + (neutralCount / idealLogCount));
    
    return returnScore
    } 

</script>
</head>

<body>
<input id="queryData" type="button" value="Query" onclick="queryData();" />
<br><br>
<textarea readonly id= "textarear" style="width:400px; height:250px"></textarea>
<textarea readonly id= "textarea" style="width:400px; height:800px"></textarea>

</body>
</html> 

```

### - 산만도 추가

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
  accessKeyId: "AKIATHFJK7FBLVG2SQ4Y",
  // secretAccessKey default can be used while using the downloadable version of DynamoDB. 
  // For security reasons, do not store AWS Credentials in your files. Use Amazon Cognito instead.
  secretAccessKey: "eq+8/M8GIYF7HgjhUNXMPgOxu2BHSabgnmb9VbrE"
});


var docClient = new AWS.DynamoDB.DocumentClient();

function queryData() {
    document.getElementById('textarea').innerHTML += "";
    // 졸음 데이터
    // var params = {
    //     TableName : "faceTable-dev",
    //     IndexName : "userIdcreatedAt",
    //     KeyConditionExpression: "#userId = :userId and begins_with(#ent, :EN)",
    //     ExpressionAttributeNames:{
    //         "#userId": "userId",
    //         "#ent": "createdAt"
    //     },
    //     ExpressionAttributeValues: {
    //         ":userId":'1f8e09da-d014-42a1-bf03-7e5566aca0c4',
    //         ":EN":"2020-12-16 05:20:2"
    //     }
    // };

    // 집중 데이터
    // var params = {
    //     TableName : "faceTable-dev",
    //     IndexName : "userIdcreatedAt",
    //     KeyConditionExpression: "#userId = :userId and begins_with(#ent, :EN)",
    //     ExpressionAttributeNames:{
    //         "#userId": "userId",
    //         "#ent": "createdAt"
    //     },
    //     ExpressionAttributeValues: {
    //         ":userId":'1f8e09da-d014-42a1-bf03-7e5566aca0c4',
    //         ":EN":"2020-12-16 04:40:2"
    //     }
    // };

    // 산만 데이터
    var params = {
        TableName : "faceTable-dev",
        IndexName : "userIdcreatedAt",
        KeyConditionExpression: "#userId = :userId and begins_with(#ent, :EN)",
        ExpressionAttributeNames:{
            "#userId": "userId",
            "#ent": "createdAt"
        },
        ExpressionAttributeValues: {
            ":userId":'1f8e09da-d014-42a1-bf03-7e5566aca0c4',
            ":EN":"2020-12-17 21:1"
        }
    };

    var adata = new Array();
    docClient.query(params, function(err, data) {
        if (err) {
            document.getElementById('textarea').innerHTML += "Unable to query. Error: " + "\n" + JSON.stringify(err, undefined, 2);
        } else {
            document.getElementById('textarear').innerHTML += "========== 가감스코어 =========" + "\n" + getScore(data);
            document.getElementById('textarea').innerHTML += "========== raw data =========" + "\n" + JSON.stringify(data, undefined, 2);
        }
    });
}


function getScore(data) {
    var idealLogCount = 1 * 5 * 10              // 1초 * 5개 * 10초 = 50개 (1분: 300개, 5분: 1500개)
    var blinkOffSet = 0.02;                     // 두눈이 0.03 이하일 경우 감은 것
    var neutralOffSet = 0.9;                     // neutral 이 0.8 이상이면 잘 집중함
    var othersOffSet = 0.7;                     // neutral 이 0.8 이상이면 잘 집중함
    var blinkBaseOffSet = idealLogCount * 0.5   // 예상했던 로그수의 반이상이 잡힐 때만, 25개 이상의 log가 잡힐 경우만 졸림을 감지


    var logArray = data.Items                   // 대상 로그 배열
    var logCount = logArray.length              // 추출된 로그수
    var blinkCount = 0;                         // 두눈이 모두 감은 경우
    var neutralCount = 0;                        // neutral 이 0.8 이상인 로그수
    var returnScore = 0;                        // 최종 가감 스코어

    for (i = 0; i < logCount; i++) {            // 로그 개수 만큼돌면서 변수 계산

        if (logCount >= blinkBaseOffSet && parseFloat(logArray[i].left_eye_blink) <= blinkOffSet && 
            parseFloat(logArray[i].right_eye_blink) <= blinkOffSet) {           // log수가 50%이상 잡히고 두눈을 감은 경우만 
            // console.log(logArray[i].left_eye_blink, logArray[i].right_eye_blink)
            blinkCount += 1;
        }

        if (parseFloat(logArray[i].neutral) >= neutralOffSet) {       // neutral이 0.8이상인 경우 OK
            neutralCount += 1;
        } else if ( parseFloat(logArray[i].happy) >= othersOffSet ||           // 0.8 이하인데 명확한 표정이 보이면 OK 나머지는 산만
                    parseFloat(logArray[i].disgusted) >= othersOffSet ||
                    parseFloat(logArray[i].fearful) >= othersOffSet ||
                    parseFloat(logArray[i].sad) >= othersOffSet ||
                    parseFloat(logArray[i].surprised) >= othersOffSet ||
                    parseFloat(logArray[i].angry) >= othersOffSet
        ) {                 
            neutralCount += 1;
        }
    }

    if (logCount >= blinkBaseOffSet && blinkCount >= (blinkBaseOffSet * 0.8)) {    // 졸음 감점 시 화면집중과 안면집중 점수는 적용되지 않음 (1분 졸면 -12 급경히 감소)
        returnScore =- 2;
    } else {
        returnScore = (logCount / idealLogCount) - ((idealLogCount - logCount) / idealLogCount) + (neutralCount / logCount) - ((logCount - neutralCount) / logCount);
    }

    console.log("idealLogCount -> " + idealLogCount);
    console.log("logCount -> " + logCount);
    console.log("blinkCount -> " + blinkCount);
    console.log("neutralCount -> " + neutralCount);

    console.log("blinkScore -> " + (logCount >= blinkBaseOffSet && blinkCount >= blinkBaseOffSet * 0.8));
    console.log("+ detectScore -> " + (logCount / idealLogCount));
    console.log("- detectScore -> " + '-' + ((idealLogCount - logCount) / idealLogCount));
    console.log("+ distract -> " + (neutralCount / logCount));
    console.log("- distract -> " + '-' + ((logCount - neutralCount) / logCount));
    
    return returnScore
    } 

</script>
</head>

<body>
<input id="queryData" type="button" value="Query" onclick="queryData();" />
<br><br>
<textarea readonly id= "textarear" style="width:400px; height:250px"></textarea>
<textarea readonly id= "textarea" style="width:400px; height:800px"></textarea>

</body>
</html> 
```



