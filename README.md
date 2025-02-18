# 프론트엔드 배포 파이프라인

## 개요

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/6912169d-ce70-41bf-b624-946d4ee984eb/Untitled.png)

GitHub Actions에 워크플로우를 작성해 다음과 같이 배포가 진행되도록 합니다.

 (사전작업: Ubuntu 최신 버전 설치)

1. Checkout 액션을 사용해 코드 내려받기
2. `npm ci` 명령어로 프로젝트 의존성 설치
3. `npm run build` 명령어로 Next.js 프로젝트 빌드
4. AWS 자격 증명 구성
5. 빌드된 파일을 S3 버킷에 동기화
6. CloudFront 캐시 무효화

## 주요 링크

- S3 버킷 웹사이트 엔드포인트: _________
- CloudFrount 배포 도메인 이름: _________

## 주요 개념

- GitHub Actions과 CI/CD 도구: _________
- S3와 스토리지: _________
- CloudFront와 CDN: _________
- 캐시 무효화(Cache Invalidation): _________
- Repository secret과 환경변수: _________

- 과제 팁1: 다이어그램 작성엔 Draw.io, Lucidchart 등을 이용합니다.
- 과제 팁2: 새로운 프로젝트 진행시, 프론트엔드팀 리더는 예시에 있는 다이어그램을 준비한 후, 전사 회의에 들어가 발표하게 됩니다. 미리 팀장이 되었다 생각하고 아키텍쳐를 도식화 하는걸 연습해봅시다.
- 과제 팁3: 캐시 무효화는 배포와 장애 대응에 중요한 개념입니다. `.github/workflows/deployment.yml` 에서 캐시 무효화가 어떤 시점에 동작하는지 보고, 추가 리서치를 통해 반드시 개념을 이해하고 넘어갑시다.
- 과제 팁4: 상용 프로젝트에선 DNS 서비스가 필요합니다. 도메인 구입이 필요해 본 과제에선 ‘Route53’을 붙이는걸 하지 않았지만, 실무에선 다음과 같은 인프라 구성이 필요하다는걸 알아둡시다.
    - 그림
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/2669fd36-261b-4035-b863-e52cf14a3743/Untitled.png)

## CDN과 성능최적화

- (CDN 도입 전과 도입 후의 성능 개선 보고서 작성)

- 과제 팁1 : CDN 도입후 성능 개선 보고서 영역은 [프론트엔드 개발자를 위한 CloudFront ](https://www.notion.so/CloudFront-2c0653cb130f42b2b21078389511cca2?pvs=21)에서 네트워크 탭을 비교한 영역을 참고해주세요. **이미지와 수치등을 표로 정리**해서 보여주면 가독성이 높은 보고서가 됩니다.
- 과제 팁2 : 저장소 → 스토리지 → CDN을 통해 정적파일을 배포하는 방식을 이해하지 못하면 다양한 기술 문서를 이해하지 못합니다. [링크](https://toss.tech/article/engineering-note-9)로 첨부한 문서를 보고 실무에서 이런 네트워크 지식이 어떻게 쓰이는지 맛보기 해보세요.