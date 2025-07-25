# AWS Cloud Cards - Amazon Interactive Video Service

## Online Reference

This document is an online companion to the AWS Cloud Cards deck for Amazon Interactive Video Service (Amazon IVS).

## Table of Contents

-   [👋 クラウドカードへようこそ](#-クラウドカードへようこそ)
-   [🤘 IVS Rocks!](#-ivs-rocks)
-   [⭐️ ライブ配信を簡単に](#️-ライブ配信を簡単に)
-   [💪 後から楽しむ（低遅延）](#-後から楽しむ低遅延)
    -   [Code](#code)
-   [💪 自由自在！チャンネル選び](#-自由自在チャンネル選び)
    -   [Code](#code-1)
-   [💪 メンバーズオンリー](#-メンバーズオンリー)
    -   [Code](#code-2)
-   [💪 柔軟なインジェストオプション](#-柔軟なインジェストオプション)
    -   [Code](#code-3)
-   [💪 イコールアクセス](#-イコールアクセス)
    -   [Code](#code-4)
-   [💪 時間厳守！](#-時間厳守)
    -   [Code](#code-5)
-   [💪 海賊版お断り！](#-海賊版お断り)
    -   [Code](#code-6)
-   [💪 途切れない配信！](#-途切れない配信)
-   [⭐️ ステージへようこそ！](#️-ステージへようこそ)
    -   [Code](#code-7)
-   [💪 みんなで広がる配信（パート 1）](#-みんなで広がる配信パート-1)
-   [💪 みんなで広がる配信（パート 2）](#-みんなで広がる配信パート-2)
    -   [Code](#code-8)
-   [💪 後から楽しむ（リアルタイム）](#-後から楽しむリアルタイム)
    -   [Code](#code-9)
-   [💪 WHIP 追加！](#-whip-追加)
-   [💪 パーフェクトタイミング](#-パーフェクトタイミング)
    -   [Code](#code-10)
-   [💪 代替インジェスト](#-代替インジェスト)
    -   [Code](#code-11)
-   [💪 リアルタイム、リアルクオリティ](#-リアルタイムリアルクオリティ)
    -   [Code](#code-12)
-   [⭐️ こんチャット！](#️-こんチャット)
    -   [Code](#code-13)
-   [💪 発言に注意しましょう](#-発言に注意しましょう)
    -   [Code](#code-14)
-   [💪 君が残したチャット](#-君が残したチャット)
    -   [Code](#code-15)
-   [☁️ Amazon CloudWatch](#️-amazon-cloudwatch)
-   [☁️ Amazon EventBridge](#️-amazon-eventbridge)
    -   [Code](#code-16)
-   [☁️ AWS CloudTrail](#️-aws-cloudtrail)
-   [☁️ Amazon S3](#️-amazon-s3)
-   [☁️ AWS AppSync](#️-aws-appsync)
    -   [Code](#code-17)
-   [🧑🏽‍💻 どこでも視聴](#-どこでも視聴)
    -   [Code](#code-18)
-   [🧑🏽‍💻 どこでも配信](#-どこでも配信)
    -   [Code](#code-19)
-   [💡 とことん作り込もう！](#-とことん作り込もう)
-   [💡 ゲームオン！](#-ゲームオン)
-   [💡 授業時間です！](#-授業時間です)
-   [💡 聞こえますか？](#-聞こえますか)
    -   [Code](#code-20)
-   [💡 ショッピング三昧](#-ショッピング三昧)
    -   [Code](#code-21)
-   [💡 ソーシャル配信](#-ソーシャル配信)

## 👋 クラウドカードへようこそ

<img src="output/card-images/ja-jp/0A-Welcome-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/0B-Welcome-ja-jp.png" style="width: 350px;" />

## 🤘 IVS Rocks!

<img src="output/card-images/ja-jp/1A-IVS-Rocks-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/1B-IVS-Rocks-ja-jp.png" style="width: 350px;" />

## ⭐️ ライブ配信を簡単に

<img src="output/card-images/ja-jp/2A-Live-Streaming-Made-Easy-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/2B-Live-Streaming-Made-Easy-ja-jp.png" style="width: 350px;" />

Code Samples

```bash
$ aws ivs create-channel --name low-latency-demo
```

```javascript
import { IvsClient, CreateChannelCommand } from "@aws-sdk/client-ivs";
const client = new IvsClient();
const createChannelInput = {
    name: "low-latency-demo",
    type: "STANDARD",
};
const command = new CreateChannelCommand(createChannelInput);
const response = await client.send(command);
```

## 💪 後から楽しむ（低遅延）

<img src="output/card-images/ja-jp/3A-Save-It-For-Later-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/3B-Save-It-For-Later-ja-jp.png" style="width: 350px;" />

### Code

```bash
# create S3 bucket
$ aws s3 mb s3://ivs-demo-recording-bucket
# create recording config
$ aws ivs create-recording-configuration \
  --name demo-config \
  --destination-configuration '{
    "s3": {
      "bucketName": "ivs-demo-recording-bucket"
    }
  }' \
  --thumbnail-configuration '{
    "recordingMode": "INTERVAL",
    "targetIntervalSeconds": 30,
    "storage": ["LATEST"],
  }'
#create channel, associate new recording config
$ aws ivs create-channel \
  --name recorded-channel-demo \
  --recording-configuration-arn [RECORDING_CONFIG_ARN]
```

## 💪 自由自在！チャンネル選び

<img src="output/card-images/ja-jp/4A-Change-The-Channel-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/4B-Change-The-Channel-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ aws ivs create-channel \
  --name low-latency-demo \
  --type STANDARD
```

## 💪 メンバーズオンリー

<img src="output/card-images/ja-jp/5A-Members-Only-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/5B-Members-Only-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ openssl ecparam -name secp384r1 -genkey -noout -out priv.pem
$ openssl ec -in priv.pem -pubout -out public.pem
```

```bash
$ aws ivs import-playback-key-pair \
  --public-key-material "`cat public.pem`"
```

```bash
$ aws ivs create-channel --authorized
```

## 💪 柔軟なインジェストオプション

<img src="output/card-images/ja-jp/6A-Flexible-Ingest-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/6B-Flexible-Ingest-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ ffmpeg -re -stream_loop -1 \
  -i $VIDEO_FILEPATH -r 30 \
  -c:v libx264 -pix_fmt yuv420p \
  -profile:v main -preset veryfast \
  -x264opts "nal-hrd=cbr:no-scenecut" \
  -minrate 3000 -maxrate 3000 -g 60 \
  -c:a aac -b:a 160k -ac 2 -ar 44100 \
  -f flv rtmps://$INGEST_ENDPOINT:443/app/$STREAM_KEY
```

```bash
$ export URI="srt://$INGEST_ENDPOINT:9000"
$ URI="$URI?streamid=$STREAM_KEY"
$ URI="$URI&passphrase=$PASSPHRASE"
$ ffmpeg -re -i $VIDEO_FILEPATH -c copy -f mpegts $URI
```

## 💪 イコールアクセス

<img src="output/card-images/ja-jp/7A-Equal-Access-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/7B-Equal-Access-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ git clone https://github.com/aws-samples/\
amazon-ivs-webgpu-captions-demo.git

# initialize the infrastructure
$ npm run deploy:init

# deploy the backend stack
$ npm run deploy:backend

# run the client app
$ npm ci
$ npm run dev

# deploy the client app (optional)
$ npm run deploy:website
```

## 💪 時間厳守！

<img src="output/card-images/ja-jp/8A-What-Time-Is-It-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/8B-What-Time-Is-It-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ aws ivs put-metadata \
  --channel-arn "[CHANNEL_ARN]" \
  --metadata "test metadata"
```

```javascript
const videoEl = document.getElementById("video-player");
const streamUrl = "[PLAYBACK_URL]";
const ivsPlayer = IVSPlayer.create();
ivsPlayer.attachHTMLVideoElement(videoEl);
ivsPlayer.load(streamUrl);
ivsPlayer.play();

const evt = IVSPlayer.PlayerEventType.TEXT_METADATA_CUE;
ivsPlayer.addEventListener(evt, (metadata) => {
    console.log(metadata);
});
```

## 💪 海賊版お断り！

<img src="output/card-images/ja-jp/9A-No-Pirates-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/9B-No-Pirates-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ aws ivs create-playback-restriction-policy \
  --name demo-policy \
  --enable-strict-origin-enforcement \
  --allowed-countries "US", "JP" \
  --allowed-origins "https://example.com"
# add policy to channel
$ aws ivs update-channel \
  --arn [CHANNEL_ARN] \
  --playback-restriction-policy-arn [POLICY_ARN]
```

## 💪 途切れない配信！

<img src="output/card-images/ja-jp/10A-No-Interruptions-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/10B-No-Interruptions-ja-jp.png" style="width: 350px;" />

## ⭐️ ステージへようこそ！

<img src="output/card-images/ja-jp/11A-Welcome-To-The-Stage-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/11B-Welcome-To-The-Stage-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ aws ivs-realtime create-stage --name real-time-demo
```

```bash
$ aws ivs-realtime create-stage --name real-time-demo \
  --participant-token-configurations '[{"userId": "1"}]'
```

```javascript
import { IvsRealTimeClient, CreateStageCommand } from "@aws-sdk-client-ivs-realtime";

const client = new IvsRealTimeClient();
const input = {
    name: "real-time-demo",
    participantTokenConfigurations: [
        {
            userId: "1",
        },
    ],
};
const command = new CreateStageCommand(input);
const response = await client.send(command);
```

## 💪 みんなで広がる配信（パート 1）

<img src="output/card-images/ja-jp/12A-Extended-Reach-Part-1-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/12B-Extended-Reach-Part-1-ja-jp.png" style="width: 350px;" />

## 💪 みんなで広がる配信（パート 2）

<img src="output/card-images/ja-jp/13A-Extended-Reach-Part-2-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/13B-Extended-Reach-Part-2-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ aws ivs-realtime create-encoder-configuration \
  --name demo-encoder-configuration \
  --video "bitrate=25000000,height=720,width=1280,framerate=30"
```

```bash
$ aws ivs-realtime start-composition \
  --stage-arn [REAL_TIME_STAGE_ARN] \
  --destination '[
    {
      "channel": {
        "channelArn": "[LOW_LATENCY_CHANNEL_ARN]",
        "encoderConfigurationArn": "[ENCODER_CONFIG_ARN]"
      }
    }
  ]'
```

## 💪 後から楽しむ（リアルタイム）

<img src="output/card-images/ja-jp/14A-Save-It-For-Later-Real-Time-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/14B-Save-It-For-Later-Real-Time-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ aws ivs-realtime create-storage-configuration \
  --name demo-storage-config \
  --s3 "bucket=demo-recording-bucket"
```

```bash
$ aws ivs-realtime create-encoder-configuration \
  --name demo-encoder-configuration \
  --video "bitrate=6000000,height=1080,width=1920,framerate=60"
```

```bash
$ aws ivs-realtime start-composition \
  --stage-arn "[STAGE_ARN]" \
  --destination '[{
    "s3": {
      "encoderConfigurationArn": ["[ENCODER_CONFIG_ARN]"],
      "storageConfigurationArn": "[STORAGE_CONFIG_ARN]"
    }
  }]
  '
```

## 💪 WHIP 追加！

<img src="output/card-images/ja-jp/15A-WHIP-It-Up-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/15B-WHIP-It-Up-ja-jp.png" style="width: 350px;" />

## 💪 パーフェクトタイミング

<img src="output/card-images/ja-jp/16A-Perfect-Timing-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/16B-Perfect-Timing-ja-jp.png" style="width: 350px;" />

### Code

```javascript
const config = {
    inBandMessaging: { enabled: true },
};
const stream = new LocalStageStream(videoTrack, config);
const payload = new TextEncoder().encode("test").buffer;
stream.insertSeiMessage(payload);
```

```javascript
const strategy = {
    subscribeConfiguration: (participant) => {
        return { inBandMessaging: { enabled: true } };
    },
    // ... other strategy functions
};
stage.on(StageEvents.STAGE_STREAM_SEI_MESSAGE_RECEIVED, (participant, seiMessage) => {
    console.log(seiMessage.payload, seiMessage.uuid);
});
```

```javascript
{"timestamp":"...","event":"card_dealt","seat":2,"card":"7H","face_up":true}
{"timestamp":"...","event":"card_dealt","seat":4,"card":"6S","face_up":true}
{"timestamp":"...","event":"card_dealt","card":"3S","face_up":true}
{"timestamp":"...","event":"card_dealt","seat":2,"card":"5H","face_up":true}
{"timestamp":"...","event":"card_dealt","seat":4,"card":"10H","face_up":true}
{"timestamp":"...","event":"card_dealt","card":"4S","face_up":false}
{"timestamp":"...","event":"prompt_player","seat":4}
{"timestamp":"...","event":"player_action","seat":4,"action":"hit"}
{"timestamp":"...","event":"card_dealt","seat":4,"card":"4S","face_up":false}
{"timestamp":"...","event":"prompt_player","seat":4}
{"timestamp":"...","event":"player_action","seat":4,"action":"stand"}
{"timestamp":"...","event":"prompt_player","seat":2}
{"timestamp":"...","event":"player_action","seat":2,"action":"hit"}
{"timestamp":"...","event":"card_dealt","seat":2,"card":"JS","face_up":false}
{"timestamp":"...","event":"prompt_player","seat":2}
{"timestamp":"...","event":"player_action","seat":2,"action":"stay"}
{"timestamp":"...","event":"dealer_reveal","card":"4S"}
```

## 💪 代替インジェスト

<img src="output/card-images/ja-jp/17A-Alternative-Ingest-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/17B-Alternative-Ingest-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ aws ivs-realtime create-ingest-configuration \
  --name demo-ingest-config \
  --stage-arn "[STAGE_ARN]" \
  --ingest-protocol RTMPS
```

## 💪 リアルタイム、リアルクオリティ

<img src="output/card-images/ja-jp/18A-Real-Time-Real-Quality-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/18B-Real-Time-Real-Quality-ja-jp.png" style="width: 350px;" />

### Code

```javascript
let cameraStream = new LocalStageStream(cameraDevice, {
    simulcast: { enabled: true },
});
```

```javascript
const initialLayerPreference: InitialLayerPreference.LOWEST_QUALITY;
const strategy = {
    subscribeConfiguration: (participant) => {
        return {
            simulcast: {
                initialLayerPreference
            }
        }
    },
    preferredLayerForStream: (participant, stream) => {
      return stream.getLowestQualityLayer();
    }
    // ... other strategy functions
}
```

## ⭐️ こんチャット！

<img src="output/card-images/ja-jp/19A-Hey-Chat-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/19B-Hey-Chat-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ aws ivschat create-room --name chat
```

```bash
$ aws ivschat create-chat-token \
  --room-identifier "[CHAT_ARN]" \
  --user-id "1" \
  --capabilities "SEND_MESSAGE"
```

```javascript
const token = "[CHAT_TOKEN]";
const endpoint = "[CHAT_ENDPOINT]";
const connection = new WebSocket(endpoint, token);
const payload = {
    Action: "SEND_MESSAGE",
    Content: "text message",
};
connection.send(JSON.stringify(payload));
connection.onmessage = (event) => {
    const message = JSON.parse(event.data);
    console.log(message);
};
```

## 💪 発言に注意しましょう

<img src="output/card-images/ja-jp/20A-Watch-What-You-Say-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/20B-Watch-What-You-Say-ja-jp.png" style="width: 350px;" />

### Code

```javascript
{
   "Content": "string",
   "MessageId": "string",
   "RoomArn": "string",
   "Attributes": {"string": "string"},
   "Sender": {
      "Attributes": { "string": "string" },
      "UserId": "string",
      "Ip": "string"
   }
}
```

```javascript
{
   "Content": "string",
   "ReviewResult": "string",
   "Attributes": {"string": "string"},
}
```

```javascript
"Attributes": { "Reason": "denied for moderation" }
```

```bash
$ aws ivschat create-room \
  --name demo-chat \
  --message-review-handler '
    {
      "fallbackResult": "DENY",
      "uri": "[LAMBDA_ARN]",
    }
  '
```

## 💪 君が残したチャット

<img src="output/card-images/ja-jp/21A-Remember-What-They-Said-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/21B-Remember-What-They-Said-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ aws logs create-log-group --log-group-name demo-chat-cw-logs
$ aws ivschat create-logging-configuration \
  --name demo-chat-log  \
  --destination-configuration '
    {
      "cloudWatchLogs": {
        "logGroupName" : "demo-chat-cw-logs"
      }
    }
  '
$ aws ivschat create-room \
  --name demo-chat  \
  --logging-configuration-identifiers "[LOGGING_CONFIG_ARN]"
```

```bash
$ aws s3 mb s3://demo-chat-s3-logs
$ aws ivschat create-logging-configuration \
  --name demo-chat-log  \
  --destination-configuration '
    {
      "s3": {
        "bucketName" : "demo-chat-s3-logs"
      }
    }
  '
```

```bash
# create firehose delivery stream first...
$ aws ivschat create-logging-configuration \
  --name demo-chat-log  \
  --destination-configuration '
    {
      "firehose": {
        "deliveryStreamName" : "demo-chat-firehose-stream"
      }
    }
  '
```

## ☁️ Amazon CloudWatch

<img src="output/card-images/ja-jp/22A-Amazon-CloudWatch-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/22B-Amazon-CloudWatch-ja-jp.png" style="width: 350px;" />

## ☁️ Amazon EventBridge

<img src="output/card-images/ja-jp/23A-Amazon-EventBridge-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/23B-Amazon-EventBridge-ja-jp.png" style="width: 350px;" />

### Code

```javascript
export const handler = async (event) => {
    console.log(`
    Received: '${event["detail-type"]}'
    named '${event.detail.event_name}'
    at ${event.time}
    on channel ${event.detail.channel_name}
    with stream id ${event.detail.stream_id}.
  `);
};
```

```bash
# create rule
$ aws events put-rule  \
  --name demo-ivs-event \
  --event-pattern "{\"source\": [\"aws.ivs\"]}" \
  --state ENABLED
# add permission to invoke lambda
$ aws lambda add-permission \
  --function-name ivs-demo-function \
  --statement-id EventBridgeInvoke \
  --action lambda:InvokeFunction \
  --principal events.amazonaws.com \
  --source-arn [RULE_ARN]
# add lambda function as target for rule
$ aws events put-targets --rule demo-ivs-rule \
  --targets '{"Id": "1", "Arn": "[LAMBDA_ARN]"}'
```

## ☁️ AWS CloudTrail

<img src="output/card-images/ja-jp/24A-AWS-CloudTrail-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/24B-AWS-CloudTrail-ja-jp.png" style="width: 350px;" />

## ☁️ Amazon S3

<img src="output/card-images/ja-jp/25A-Amazon-S3-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/25B-Amazon-S3-ja-jp.png" style="width: 350px;" />

## ☁️ AWS AppSync

<img src="output/card-images/ja-jp/26A-AWS-AppSync-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/26B-AWS-AppSync-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ aws appsync create-api \
  --name demo-event-api \
  --event-config '
    {
      "authProviders": [{"authType": "API_KEY"}],
      "connectionAuthModes": [{"authType": "API_KEY"}],
      "defaultPublishAuthModes": [{"authType": "API_KEY"}],
      "defaultSubscribeAuthModes": [{"authType": "API_KEY"}]
    }'
$ aws appsync create-api-key --api-id [API_ID]
$ aws appsync create-channel-namespace \
  --name default-api-ns \
  --api-id [API_ID]
```

## 🧑🏽‍💻 どこでも視聴

<img src="output/card-images/ja-jp/27A-Watch-Anywhere-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/27B-Watch-Anywhere-ja-jp.png" style="width: 350px;" />

### Code

```javascript
const videoEl = document.getElementById("video-player");
const streamUrl = "[PLAYBACK_URL]";
const ivsPlayer = IVSPlayer.create();
ivsPlayer.attachHTMLVideoElement(videoEl);
ivsPlayer.load(streamUrl);
ivsPlayer.play();
```

## 🧑🏽‍💻 どこでも配信

<img src="output/card-images/ja-jp/28A-Streaming-On-The-Go-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/28B-Streaming-On-The-Go-ja-jp.png" style="width: 350px;" />

### Code

```html
<canvas id="preview"></canvas>

<script type="module">
    const streamKey = "[STREAM_KEY]";
    const ingestEndpoint = "[INGEST_ENDPOINT]";
    const streamConfig = IVSBroadcastClient.STANDARD_LANDSCAPE;
    const config = { streamConfig, ingestEndpoint };
    const client = IVSBroadcastClient.create(config);
    await navigator.mediaDevices.getUserMedia({ video: true, audio: true });
    client.attachPreview(document.getElementById("preview"));
    const devices = await navigator.mediaDevices.enumerateDevices();
    const videoDevices = devices.filter((d) => d.kind == "videoinput");
    const audioDevices = devices.filter((d) => d.kind == "audioinput");
    const cameraStream = await navigator.mediaDevices.getUserMedia({
        video: {
            deviceId: videoDevices[0].deviceId,
            aspectRatio: 16 / 9,
        },
    });
    const microphoneStream = await navigator.mediaDevices.getUserMedia({
        audio: {
            deviceId: audioDevices[0].deviceId,
        },
    });
    client.addVideoInputDevice(cameraStream, "camera1", { index: 0 });
    client.addAudioInputDevice(microphoneStream, "mic1");
    client.startBroadcast(streamKey);
</script>
```

## 💡 とことん作り込もう！

<img src="output/card-images/ja-jp/29A-Let-Them-Cook-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/29B-Let-Them-Cook-ja-jp.png" style="width: 350px;" />

## 💡 ゲームオン！

<img src="output/card-images/ja-jp/30A-Game-On-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/30B-Game-On-ja-jp.png" style="width: 350px;" />

## 💡 授業時間です！

<img src="output/card-images/ja-jp/31A-Learning-Time-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/31B-Learning-Time-ja-jp.png" style="width: 350px;" />

## 💡 聞こえますか？

<img src="output/card-images/ja-jp/32A-Can-You-Hear-Me-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/32B-Can-You-Hear-Me-ja-jp.png" style="width: 350px;" />

### Code

```bash
$ git clone \
  https://github.com/aws-samples/amazon-ivs-real-time-audio-rooms-web-demo.git
$ cd amazon-ivs-real-time-audio-rooms-web-demo
```

```bash
$ npm run deploy:init
```

```bash
$ npm run deploy:backend:dev # for development
$ npm run deploy:backend:prod # for production
```

```bash
$ npm run deploy:website:dev # for development
$ npm run deploy:website:prod # for production
```

```bash
$ npm run dev
```

## 💡 ショッピング三昧

<img src="output/card-images/ja-jp/33A-Shop-Until-You-Drop-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/33B-Shop-Until-You-Drop-ja-jp.png" style="width: 350px;" />

### Code

```bash
# check out the project
$ git clone \
  https://github.com/aws-samples/\
amazon-ivs-real-time-basic-web-demo.git
$ cd amazon-ivs-real-time-basic-web-demo

# install required packages
$ npm ci

# run the deploy
# when the deployment successfully completes
# copy the url provided in the output
# you may need the url when running client app
$ npm run deploy

# retrieve the CloudFormation stack outputs
$ aws cloudformation describe-stacks \
  --stack-name AmazonIVSRtWebDemoStack \
  --query 'Stacks[].Outputs'

# cleanup (delete all resources associated
# with this demo including DynamoDB table)
$ npm run destroy
```

## 💡 ソーシャル配信

<img src="output/card-images/ja-jp/34A-Social-Streaming-ja-jp.png" style="width: 350px;" />
<img src="output/card-images/ja-jp/34B-Social-Streaming-ja-jp.png" style="width: 350px;" />
