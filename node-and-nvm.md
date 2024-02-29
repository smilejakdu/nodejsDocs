# Node 셋팅 & nvm

#### NVM 설치:

1. **터미널 열기**: Mac에서는 Spotlight 검색(Cmd + Space)을 사용하여 'Terminal'을 찾거나, 'Applications' > 'Utilities' 폴더 내에서 Terminal 애플리케이션을 찾을 수 있습니다.
2.  **NVM 설치 스크립트 실행**: NVM의 GitHub 페이지에서 제공하는 설치 스크립트를 사용합니다. 아래는 cURL을 사용하는 방법입니다:

    ```bash
    curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    ```

    또는 wget을 사용하는 경우:

    ```bash
    wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
    ```

    여기서 `v0.39.1`은 NVM의 버전이며, 최신 버전으로 변경될 수 있습니다. 최신 버전은 NVM의 GitHub 페이지에서 확인하세요.
3.  **환경설정 적용**: 설치 후, NVM을 사용할 수 있도록 터미널 환경을 업데이트합니다. 터미널을 재시작하거나 다음 명령어를 실행합니다:

    ```bash
    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
    [ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion
    ```

    이 명령은 보통 `.bash_profile`, `.zshrc`, `.profile`, 또는 `.bashrc` 파일에 추가됩니다. 설치 스크립트가 이를 자동으로 처리해줄 수도 있습니다.

#### Node.js 설치 및 사용:

1.  **사용 가능한 Node.js 버전 확인**: 설치 가능한 Node.js의 버전을 확인하려면, 터미널에서 다음 명령어를 입력합니다:

    ```bash
    nvm list-remote
    ```
2.  **Node.js 설치**: 원하는 버전의 Node.js를 설치하려면, 예를 들어 14.17.0 버전을 설치하고 싶다면 다음과 같이 입력합니다:

    ```bash
    nvm install 14.17.0
    ```
3.  **설치된 Node.js 버전 사용**: 설치한 Node.js 버전을 사용 설정하려면, 다음 명령어를 사용합니다:

    ```bash
    nvm use 14.17.0
    ```
4.  **현재 사용 중인 Node.js 버전 확인**: 현재 사용 중인 Node.js 버전을 확인하려면, 다음 명령어를 입력합니다:

    ```bash
    node --version
    ```

이러한 단계를 통해 Mac에서 NVM을 사용하여 Node.js 버전을 설치하고 관리할 수 있습니다. 이제 원하는 버전의 Node.js로 작업을 시작할 수 있습니다.



## Node 21 version

설치는 간단하다.

nvm install 21

로 설치를 하면된다.





