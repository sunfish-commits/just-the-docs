목적
-------
이 파일은 AI 코딩 에이전트가 "Just the Docs" Jekyll 테마 저장소에서 즉시 생산성을 발휘할 수 있도록 간결하고 실행 가능한 지침을 제공합니다.

빠른 시작 (명령어)
- Ruby 의존성 설치: `bundle install` (`Gemfile` 사용).
- 로컬에서 사이트 실행: `bundle exec jekyll serve --livereload` (개발 서버 http://localhost:4000).
- 프로덕션 빌드: `bundle exec jekyll build`.
- 검색 데이터 생성 (`lib/tasks/search.rake` 사용): `bundle exec rake search:init` (`/assets/js/search-data.json` 작성).
- Ruby 테스트 실행: `bundle exec rspec` (`Gemfile`에 RSpec 설정).
- 프론트엔드 자산 린트/포매팅: `npm run lint`, `npm run format` (`package.json` 스크립트 참고).

큰 그림의 아키텍처
- 이 저장소는 Jekyll 테마입니다 (독립형 앱이 아님). 주요 경계:
  - 테마 자산/레이아웃: `_layouts/`, `_includes/`, `_sass/` — gem으로 패키징됩니다.
  - 예제 사이트/문서 콘텐츠: `docs/` — 테마를 사용하는 예제 페이지와 문서 사이트를 포함합니다.
  - 패키징/메타데이터: `just-the-docs.gemspec`, `Gemfile`에서 gem 기반 배포를 정의합니다.
  - 빌드/테스트 헬퍼: `lib/tasks/` (예: `search.rake`)와 `spec/`에 테스트가 포함됩니다.

프로젝트별 관례와 패턴
- Gem 기반 테마: 개발에서 `bundle`과 `bundle exec jekyll ...` 사용합니다. 테마를 gem으로 사용할 때, gemspec에 추적된 파일만 포함됩니다 (주로 `_layouts`, `_includes`, `_sass`).
- 검색 데이터 생성: `lib/tasks/search.rake`는 `assets/js/zzzz-search-data.json`을 생성하며 퍼머링크는 `/assets/js/search-data.json`입니다. 콘텐츠 변경 후 검색 인덱스를 재생성하려면 `rake search:init`을 사용합니다.
- 문서 기본값: `_config.yml`에서 `path: "docs"`와 `layout: default`의 `defaults:`를 설정합니다. `docs/` 콘텐츠는 테마 레이아웃을 사용해 제공됩니다.
- Mermaid: `_config.yml`의 `mermaid:` 블록과 `_includes/mermaid_config.js`의 설정을 통해 선택적으로 활성화됩니다.
- 프론트엔드 스타일링: SCSS는 `_sass/` 아래에 있고 컴파일된 자산은 `assets/css/`에 있습니다. `npm run lint`와 `npm run format`을 사용해 스타일을 확인하고 포매팅합니다.

개발자 워크플로우 (일반적인 작업 및 위치)
- 테마 코드를 편집하면서 변경 사항 미리보기: 저장소 루트에서 `bundle exec jekyll serve --livereload`을 실행하고 `_layouts/` 또는 `_includes/`의 파일을 편집합니다.
- 접근성 및 통합 테스트 실행: `spec/`의 스펙은 RSpec, Capybara, axe-core를 사용합니다 (`Gemfile` 개발 그룹 참고). `bundle exec rspec`을 실행합니다.
- 검색 동작 업데이트: `lib/tasks/search.rake` 또는 `docs/` 콘텐츠를 편집한 후 `bundle exec rake search:init`을 실행합니다.
- 패키징 참고: gem/사이트에서 제외된 파일은 `_config.yml` `exclude:`에 선언됩니다. — gemspec, Gemfile과 같은 패키징 관련 파일을 변경할 때 주의하세요. 이 파일들은 gem에 포함되지 않습니다.

검사할 유용한 파일 (예시)
- `Gemfile` — 프로젝트 의존성 및 테스트 gem.
- `_config.yml` — 사이트 기본값, `search` 옵션, `mermaid` 선택 및 패키징 `exclude` 목록.
- `lib/tasks/search.rake` — 검색 JSON 생성 로직 및 퍼머링크 매핑.
- `package.json` — 프론트엔드 자산을 위한 린트/포매팅 스크립트.
- `_layouts/default.html`, `_includes/` — 레이아웃 및 페이지 구성이 있는 곳.
- `docs/` — 지원되는 패턴을 보여주는 예제 콘텐츠 (`docs/index-test.md` 및 `docs/ui-components/` 아래 UI 컴포넌트 참고).

에이전트가 문맥 없이 변경하지 말아야 할 것
- `gemspec`, `just-the-docs` 패키징, 또는 `_config.yml` `exclude:`에 나열된 파일을 gem 동작 변경의 명시적 의도 없이 수정합니다.
- 로컬 서버를 실행해서 검증하지 않고 사이트 생성에 영향을 미치는 `_config.yml` 키 (예: `permalink`, `defaults`, `plugins`)를 변경합니다.

불명확하거나 더 많은 문맥이 필요할 경우
- 우선순위를 정할 워크플로우 (테마 개발, 문서 작성, 패키징, 또는 접근성 테스트)와 CI를 로컬에서 실행할지 여부를 문의합니다. 다음에 실행할 정확한 명령어를 포함합니다.

파일 끝
