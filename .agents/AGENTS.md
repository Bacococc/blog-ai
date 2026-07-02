# Custom Tool Rules for Blog AI Workspace

이 워크스페이스에는 블로그 자동화 및 이미지 생성을 위한 커스텀 도구가 로컬 스크립트(`bin/call_tools`)로 구현되어 있습니다. 사용자가 블로그 작성이나 이미지 생성을 요청할 경우, 에이전트는 제공되는 쉘 도구(Bash/Shell)를 사용하여 이 스크립트들을 직접 호출해야 합니다.

## 1. 블로그 초안 작성 도구 (`blog`)
- **역할**: 입력한 텍스트 파일을 분석하여 초보자도 이해하기 쉬운 한국어 블로그 글을 생성하고 마크다운 파일로 저장합니다. (파일명은 원래 파일명 앞에 `draft-`가 붙음)
- **실행 커맨드**:
  ```bash
  echo '{"filename": "<파일명>"}' | ./bin/call_tools blog
  ```

## 2. 이미지 생성 도구 (`gemini-image-gen`)
- **역할**: 입력한 프롬프트에 따라 Gemini API를 호출하여 이미지를 생성하고 `gemini-image-[타임스탬프].png` 파일로 저장합니다.
- **실행 커맨드**:
  ```bash
  echo '{"prompt": "<이미지 생성 프롬프트>"}' | ./bin/call_tools gemini-image-gen
  ```

---

## 에이전트 행동 지침
1. 사용자가 블로그 초안 작성을 요청하는 경우 (예: "PRD.md 내용으로 블로그 써줘"), 에이전트는 쉘 도구를 실행하여 `echo '{"filename": "PRD.md"}' | ./bin/call_tools blog` 명령어를 실행하고 그 결과 파일명을 사용자에게 안내하십시오.
2. 사용자가 이미지 생성을 요청하는 경우 (예: "cyberpunk city 이미지 만들어줘"), 에이전트는 쉘 도구를 실행하여 `echo '{"prompt": "cyberpunk city"}' | ./bin/call_tools gemini-image-gen` 명령어를 실행하고 생성된 파일명을 안내하십시오.
