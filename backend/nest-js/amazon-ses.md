# Amazon SES

<figure><img src="../../.gitbook/assets/스크린샷 2024-09-20 오전 1.21.50.png" alt=""><figcaption></figcaption></figure>

위 사진처럼 샌드박스 해제를 우선 해야합니다.&#x20;

설정 시작 -> 작업열기



<figure><img src="../../.gitbook/assets/스크린샷 2024-09-20 오전 1.33.39.png" alt=""><figcaption></figcaption></figure>



`sendEmail.ts` 파일을 공용으로 사용할 수 있도록 설정하기 위해, AWS SDK를 사용하여 이메일 전송 기능을 모듈화하는 예시를 제공합니다. 이를 통해 다른 파일에서 해당 함수를 쉽게 임포트하고 사용할 수 있도록 할 것입니다.

#### sendEmail.ts 파일 작성:

```typescript
import { SESClient, SendEmailCommand, SendEmailCommandInput } from "@aws-sdk/client-ses";

// SES 클라이언트 초기화
const sesClient = new SESClient({ region: "us-west-2" });

// 이메일 전송 함수
export const sendEmail = async (recipientEmail: string, subject: string, body: string) => {
  const params: SendEmailCommandInput = {
    Source: "sender@example.com", // 실제 발신자 이메일로 교체해야 합니다.
    Destination: {
      ToAddresses: [recipientEmail], // 수신자 이메일
    },
    Message: {
      Subject: {
        Data: subject,
        Charset: 'UTF-8'
      },
      Body: {
        Text: {
          Data: body,
          Charset: 'UTF-8'
        }
      }
    },
  };

  try {
    const data = await sesClient.send(new SendEmailCommand(params));
    console.log("Email sent successfully:", data);
    return data;
  } catch (err) {
    console.error("Failed to send email:", err);
    throw err;
  }
};
```

#### 사용 예시:

`sendEmail` 함수를 다른 파일에서 사용하기 위해서는 다음과 같이 해당 파일을 임포트하고 함수를 호출합니다.

```typescript
// 다른 파일에서 sendEmail 함수 사용
import { sendEmail } from './sendEmail';

async function main() {
  try {
    const response = await sendEmail("recipient@example.com", "Test Email", "This is a test email sent from AWS SES.");
    console.log("Response:", response);
  } catch (error) {
    console.error("Error sending email:", error);
  }
}

main();
```

#### 주의 사항:

* **환경 설정**: SES 사용을 위해서는 AWS Console에서 해당 이메일 주소의 검증이 필요합니다. 발신자 및 수신자 이메일 주소가 SES와 함께 사용하기 위해 검증되어야 합니다.
* **에러 핸들링**: SES에서 발생할 수 있는 여러 에러(검증되지 않은 이메일, 쿼터 초과 등)에 대해 적절한 예외 처리가 필요합니다.

위 코드는 TypeScript를 사용해 작성되었으며, AWS SDK v3의 새로운 모듈형 구조를 활용하고 있습니다. 이렇게 모듈화된 함수는 다양한 부분에서 재사용 가능하며, 관리 및 유지보수가 용이합니다.

