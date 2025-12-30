# NextJS Mono Repo



**Turborepo(터보레포) 기반 모노레포**를 기준으로 핵심만 정리해서 설명할게요.\
(질문에서 `turno`라고 하셨는데, 일반적으로 **Turborepo**를 의미하는 경우가 대부분이라 이 기준으로 설명합니다.)

***

### 🧩 모노레포(Monorepo)란?

**여러 개의 앱·패키지를 하나의 Git 저장소에서 관리**하는 방식입니다.

#### 기존 방식 (멀티레포)

```
frontend-web/
frontend-admin/
backend-api/
shared-ui/
```

#### 모노레포

```
my-repo/
 ├─ apps/
 │   ├─ web/
 │   ├─ admin/
 │   └─ api/
 └─ packages/
     ├─ ui/
     ├─ hooks/
     └─ utils/
```

***

### 🚀 Turborepo란?

Vercel에서 만든 **모노레포 빌드 & 태스크 최적화 도구**입니다.

> 핵심 목표\
> 👉 **빌드/테스트/린트 시간을 캐싱으로 미친 듯이 줄이자**

![Image](https://www.maxpou.fr/_astro/turborepo-pipeline.Byba11M-_2oPoM.webp)

![Image](https://miro.medium.com/1*Mxb0_OUzqRgtDQwjnnVyxg.png)

![Image](https://engineering.linecorp.com/wp-content/uploads/2022/04/turborepo6.png)

***

### 🔥 Turborepo의 핵심 개념 5가지

#### 1️⃣ apps / packages 구조

* **apps**: 실제 서비스 (Next.js, NestJS, Vite 등)
* **packages**: 공통 라이브러리 (ui, hooks, utils)

```
apps/web        → Next.js
apps/admin      → Next.js
apps/api        → NestJS

packages/ui     → 공통 UI 컴포넌트
packages/utils  → 공통 유틸
```

***

#### 2️⃣ turbo.json (파이프라인 정의)

```json
{
  "pipeline": {
    "build": {
      "dependsOn": ["^build"],
      "outputs": [".next/**", "dist/**"]
    },
    "lint": {},
    "test": {}
  }
}
```

의미:

* `^build` → **의존하는 패키지부터 먼저 빌드**
* `outputs` → 결과물 캐싱

***

#### 3️⃣ 강력한 캐싱 (Local + Remote)

* **코드 변경 없으면 → 빌드 스킵**
* 팀 단위 캐시 공유 가능 (Vercel Remote Cache)

```
❌ 기존: 5분 빌드
✅ Turborepo: 3초 (캐시 HIT)
```

👉 대규모 레포에서 체감이 압도적

***

#### 4️⃣ workspace 기반 패키지 관리

보통 조합:

* `pnpm + workspaces` ⭐⭐⭐⭐⭐
* `yarn workspaces`
* `npm workspaces`

```json
// package.json
{
  "workspaces": ["apps/*", "packages/*"]
}
```

```ts
import { Button } from "@repo/ui";
```

***

#### 5️⃣ 병렬 실행 & 의존성 그래프

```bash
pnpm turbo run build
```

* 가능한 작업은 **병렬 실행**
* 필요한 것만 **순서 보장**

***

### 🧠 Turborepo를 쓰는 이유 (한 줄 요약)

| 항목   | 이유                 |
| ---- | ------------------ |
| 속도   | 캐시로 CI/CD 시간 대폭 감소 |
| 구조   | 대규모 서비스 구조 정리      |
| 재사용  | 공통 코드 재사용          |
| 확장성  | 앱 추가가 매우 쉬움        |
| 팀 협업 | 프론트/백엔드 통합 관리      |

***

### 🧪 Next.js Page Router도 사용 가능할까?

👉 **완전히 가능**합니다. (중요 포인트 👍)

* Turborepo는 **라우터와 무관**
* App Router / Page Router 차이 없음

```
apps/web/pages/index.tsx  ✅ OK
apps/admin/pages/login.tsx ✅ OK
```

***

### ❌ Turborepo가 안 어울리는 경우

* 앱이 1개뿐
* 공통 코드가 거의 없음
* CI/CD 최적화 필요 없음

→ 이 경우는 **단일 레포가 더 단순**

***

### ✅ 추천 조합 (실무 최강)

```
Turborepo
+ pnpm
+ Next.js (pages or app)
+ NestJS
+ shared packages
```

***

### ✨ 한 문장 정리

> **Turborepo 모노레포는 “대규모 서비스에서 속도와 구조를 동시에 잡기 위한 표준 도구”다.**

원하시면

* **Next.js + NestJS 기준 실제 폴더 구조**
* **CI/CD (GitHub Actions)**
* **배포 전략 (앱별 배포 vs 단일 배포)**\
  까지 이어서 정리해줄게요.
