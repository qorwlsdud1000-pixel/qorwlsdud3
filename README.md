# EcoScan — AI 재활용품 분류 웹사이트

컴퓨터비전2 수업 과제용으로 제작한 교육용 이미지 분류 웹사이트입니다.

## 주요 기능

- JPG/PNG/WEBP 이미지 드래그앤드롭 및 파일 선택 (10MB 제한)
- 브라우저 내 CLIP 비전-언어 모델을 통한 **실제 제로샷 이미지 분류**
- 10가지 후보 범주 비교: 투명 페트병, 플라스틱 용기, 금속 캔, 유리병, 종이, 골판지, 종이팩, 비닐, 스티로폼, 일반쓰레기·기타
- 상위 3개 범주 상대 점수 및 분리배출 가이드
- 브라우저 localStorage 최근 10개 분석 기록 (이미지 저장 안 함)
- PC/모바일 반응형 화면

## 실행 방법 (Windows PowerShell)

Node.js 20.19 이상 또는 22.12 이상 설치 후 프로젝트 폴더에서:

```powershell
npm install
npm run dev
```

표시되는 주소(기본 http://localhost:5173)로 접속하세요.

## 배포 빌드

```powershell
npm run build
npm run preview
```

빌드 후 `dist/`가 생성됩니다. Vercel에서 GitHub 저장소를 연결해 Vite 프레임워크로 Import하면 자동 배포됩니다.

## 실제 모델 안내

`@huggingface/transformers`의 `zero-shot-image-classification` 파이프라인을 이용하며 모델은 `Xenova/clip-vit-base-patch32` 입니다.
최초 분석에서 Hugging Face에서 모델 파일을 다운로드합니다. 환경에 따라 다운로드와 초기화에 시간이 걸리고 인터넷 연결이 필요합니다. 이미지 추론은 브라우저에서 진행되며 업로드 이미지가 별도 애플리케이션 서버에 전송되지는 않습니다. 외부 모델 파일 다운로드가 제한된 네트워크에서는 실행되지 않을 수 있습니다.

CLIP은 재활용품만을 위해 학습된 전용 모델이 아닙니다. 본 서비스는 영문 후보 문장 30개(범주별 3개)에 대한 유사도 점수를 범주별로 합산·정규화해 상대 순위를 제공합니다. **표시된 수치는 정답 확률 또는 공식적 정확도가 아닙니다.** 복합소재/오염/지방자치단체 수거 기준은 별도로 확인해야 합니다.

## 파일 구성

- `index.html` : HTML 진입점
- `src/main.js` : 이미지 입력, 모델 추론, 결과 화면, 기록 기능
- `src/data.js` : 10개 분류 범주, 모델 후보 텍스트, 배출 안내
- `src/style.css` : 반응형 UI 스타일
- `package.json` : 의존성 및 실행 스크립트
- `vercel.json` : Vercel 배포 설정
- `docs/과제발표가이드.md` : 발표용 기획 및 시연 순서
- `code_txt/` : 소스별 TXT 파일 사본

## 검증

`npm run build`가 성공하는지 우선 확인하세요. 실제 예측 검증은 인터넷에서 모델이 다운로드되는 웹브라우저에서, 직접 촬영한 복수의 이미지로 테스트해야 합니다. 모델 다운로드 및 브라우저 추론의 완전한 실사용 성공 여부는 환경에 따라 달라집니다.

## 저작권/출처

- 모델: [Xenova/clip-vit-base-patch32](https://huggingface.co/Xenova/clip-vit-base-patch32)
- Transformers.js: [Hugging Face](https://huggingface.co/docs/transformers.js)
- 개발 방식: 생성형 AI를 활용한 기획·코드 생성 및 수정

프로젝트는 교육 및 시연 목적으로 작성되었습니다. 배출 안내는 일반적 예시이며 실제 지역별 지침이 우선합니다.
