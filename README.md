
# Dynamic Web Project + Ant to Gradle build Project Migration Test

본 문서는 **Dynamic Web Project**를 **Ant → Gradle** 기반으로 전환하는 과정에서의 마이그레이션 테스트 가이드를 정리한 것입니다.  
**목표**는 프로젝트 구조를 최대한 변경하지 않고, 이클립스(Eclipse) 환경에서 실행 및 배포가 가능하도록 하는 것입니다.

---

## 마이그레이션 주요 원칙
- 기존 **프로젝트 구조**를 유지한다.
- **이클립스 환경**에서 실행 및 배포되는 것을 전제로 한다.

---

## 마이그레이션 절차

1. **라이브러리 관리 전환**  
   - 기존 `WEB-INF/lib`에 존재하던 라이브러리 파일들을 직접 포함하지 않고,  
     **Nexus** 또는 **외부 Maven 저장소**에서 가져오도록 변경한다.  

2. **`build.gradle` 생성**  
   - Gradle 빌드 스크립트를 신규 생성하여 의존성을 선언한다.  

3. **프로젝트 Gradle 연동**  
   - `프로젝트 우클릭 → Configure → Add Gradle Nature`  

4. **Gradle 초기 동기화**  
   - `프로젝트 우클릭 → Gradle → Refresh Gradle`  

5. **Gradle Wrapper 설정**  
   - `gradle/wrapper/gradle-x.x-bin.zip` 버전에 맞는 Gradle 파일을 이동/적용한다.
   - 이후 로컬에 설치된 gradle을 사용하여 프로젝트내에서 `gradle wrapper` 명령어 실행  

6. **Gradle 재동기화**  
   - `프로젝트 우클릭 → Gradle → Refresh Gradle`  

7. **Web Deployment Assembly 확인**  
   - `프로젝트 우클릭 → Properties → Web Deployment Assembly`  
   - 다음 항목들이 포함되어 있는지 확인:
     - `src`
     - `WebContent`
     - `Project and External Dependencies`  

8. **Project Facets 확인**  
   - `프로젝트 우클릭 → Properties → Project Facets`  
   - 다음 사항을 확인/연결한다:
     - Java 버전
     - Dynamic Web Project 버전
     - Runtimes (Tomcat 버전)  

---

## 참고 사항
- `war` 플러그인 및 `eclipse-wtp` 플러그인을 사용하여 WAR 빌드 및 이클립스 연동을 지원한다.
- 프로젝트 구조 변경은 최소화하되, 빌드/배포 관리 방식을 **Gradle 중심**으로 전환한다.
