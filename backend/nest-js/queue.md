# Queue

nest js 에서 queue 를 사용하려면 `@nestjs/queue` 를 설치해야한다.



NestJS에서 제공하는 Queue 시스템을 사용하여 비동기 작업을 관리하고 효율적으로 처리할 수 있습니다. 이는 특히 대량의 데이터 처리나 복잡한 비즈니스 로직을 실행할 때 유용합니다. Queue를 사용하면 작업을 백그라운드에서 실행할 수 있으며, 이는 애플리케이션의 성능과 응답성을 향상시키는 데 도움이 됩니다.

Queue를 사용하려면, 다음과 같은 단계를 따르는 것이 좋습니다:

### redis 셋팅

로컬에서 설치를 해도 되고 , docker compose 파일을 생성해서 작업해도 된다.

```bash
version: "3"
services:
  watcha-redis:
    container_name: watcha-redis
    image: redis:alpine
    ports:
      - 6379:6379
    volumes:
      - watcha-redis:/data
    command: redis-server --requirepass foobared

volumes:
  watcha-redis:

```

이후 `redis-cli -h localhost -p 6379 -a foobared`

리스트 검색 : `keys *`



1.  **Queue 라이브러리 설치**: NestJS에서는 Bull이라는 라이브러리를 주로 사용합니다. `@nestjs/bull`과 `bull` 패키지를 설치합니다.

    ```bash
    npm install @nestjs/bull bull
    ```
2.  **Queue 모듈 설정**: `BullModule`을 애플리케이션 모듈에 추가합니다. Queue 이름과 Redis와 같은 백엔드 저장소를 설정합니다.

    ```typescript
    import { BullModule } from '@nestjs/bull';

    @Module({
      imports: [
          CacheModule.registerAsync({
              useFactory: (configService: ConfigService) => ({
                isGlobal: true,
                host: configService.get<string>('REDIS_HOST'),
                port: configService.get<number>('REDIS_PORT'),
                password: configService.get<string>('REDIS_PASSWORD'),
                ttl: configService.get<number>('CACHE_TTL'),
                max: configService.get<number>('CACHE_MAX'),
                }),
              inject: [ConfigService],
            }),
        BullModule.forRootAsync({
              useFactory: (configService: ConfigService) => ({
                redis: {
                  host: configService.get<string>('REDIS_HOST'),
                  port: configService.get<number>('REDIS_PORT'),
                  password: configService.get<string>('REDIS_PASSWORD'),
                },
            }),
    	inject: [ConfigService],
        }),
        BullModule.forRoot({
          redis: {
            host: 'localhost',
            port: 6379,
          },
        }),
        BullModule.registerQueue({
          name: 'document-processing',
        }),
        // 다른 모듈들...
      ],
      // ...
    })
    export class AppModule {}

    ```

    \
    그런데 queue 와 redis 가 무슨관계가 있을까 ??\
    \
    `@nestjs/bull` 패키지는 NestJS에서 사용할 수 있는 Queue 시스템을 구현하는 데 사용되며, 내부적으로 `bull` 라이브러리를 사용합니다. `bull`은 Node.js에서 사용되는 강력하고 견고한 Queue 시스템으로, Redis를 백엔드 저장소로 활용합니다.

    Redis와 `bull`의 관계는 다음과 같습니다:

    1. **데이터 저장**: Redis는 `bull` Queue 시스템의 데이터를 저장하는 데 사용됩니다. 이 데이터에는 작업 항목, 상태, 결과 등이 포함될 수 있습니다. Redis는 메모리 내 데이터베이스로서 빠른 데이터 액세스와 효율적인 데이터 처리를 제공합니다.
    2. **분산 처리**: Redis를 사용하면 여러 서버나 프로세스에서 Queue에 접근하고 작업을 처리할 수 있습니다. 이는 분산 시스템에서의 작업 부하 분산과 확장성 향상에 기여합니다.
    3. **신뢰성과 지속성**: Redis는 데이터의 지속성을 지원합니다. 이는 시스템이 다운되더라도 Queue의 데이터가 유실되지 않음을 의미합니다. Redis의 지속성 옵션을 통해 데이터가 안전하게 보관됩니다.
    4. **실시간 알림**: `bull`은 Redis의 PUB/SUB 기능을 사용하여 작업의 완료나 진행 상태와 같은 이벤트에 대한 실시간 알림을 지원합니다. 이를 통해 애플리케이션은 작업의 상태 변경을 실시간으로 추적하고 대응할 수 있습니다.

    이러한 이유로 `@nestjs/bull`을 사용할 때 Redis를 설치하고 구성해야 합니다. Redis는 `bull` Queue의 백엔드로서 중요한 역할을 하며, 복잡한 큐잉 시스템을 구축하고 운영하는 데 필수적인 구성 요소입니다. Redis 서버의 주소와 포트 번호는 `BullModule` 설정에서 명시해야 합니다.<br>
3.  **Producer 서비스 생성**: `DocumentService` 내에서 Queue에 작업을 추가하는 로직을 구현합니다. 예를 들어, `upload` 함수에서 문서 변환 작업을 Queue에 추가할 수 있습니다.

    ```typescript
    import { InjectQueue } from '@nestjs/bull';
    import { Queue } from 'bull';

    export class DocumentService {
      constructor(@InjectQueue('document-processing') private documentQueue: Queue) {}

      async upload(...) {
        // ... 기타 로직 ...

        // Queue에 작업 추가
        await this.documentQueue.add({
          id,
          documents: convertedDocuments,
        });

        // ...
      }
    }
    ```
4.  **Consumer 프로세서 생성**: 별도의 프로세서를 만들어 실제 작업을 처리합니다. 이 프로세서는 Queue에서 작업을 받아 처리하며, 이는 별도의 프로세스에서 실행될 수 있습니다.

    ```typescript
    import { Process, Processor } from '@nestjs/bull';
    import { Job } from 'bull';

    @Processor('document-processing')
    export class DocumentProcessingConsumer {
      @Process()
      async handleDocumentProcessing(job: Job) {
        const { id, documents } = job.data;
        // 문서 처리 로직 구현
      }
    }
    ```

이러한 방식으로 `upload` 함수의 로직 일부를 Queue 시스템으로 이동시키면, 대량의 데이터 처리나 시간이 많이 소요되는 작업을 비동기적으로 처리할 수 있어, 애플리케이션의 전반적인 성능과 안정성이 향상될 수 있습니다. Queue를 사용하면 작업을 분산시키고, 애플리케이션의 메인 스레드가 블로킹되는 것을 방지할 수 있습니다.
