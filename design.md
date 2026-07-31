# Design System · 2026 Sydney Trip Brief

## Visual Identity

이 슬라이드 덱은 **에디토리얼 매거진** 스타일을 기반으로 합니다.
여행 일정이라는 실용적 정보를, 보는 사람이 기대감을 느끼도록 시각적으로 표현하는 것이 목표입니다.

## Design References

| 참고 | 요소 | 적용 |
|------|------|------|
| [Monocle Magazine](https://monocle.com) | 따뜻한 크래프트 컬러, 모노스페이스 메타 정보, 깔끔한 타임라인 | 전체 색상 체계, chrome/foot 영역 |
| [Cereal Magazine](https://readcereal.com) | 여백 활용, 대형 타이포, 사진과 텍스트의 호흡 | 커버 레이아웃, lead 텍스트 |
| Swiss International Typographic Style | 그리드 기반 정보 배치, 강한 위계 대비 | 타임라인, 테이블, pill 컴포넌트 |
| Apple Keynote 2024 | 극단적 타입 사이즈 대비 (96px h1 vs 11px meta) | 커버-본문 사이즈 비율 |
| [Guizang PPT Skill](https://github.com/op7418/guizang-ppt-skill) – Style A | editorial magazine × electronic ink, 수평 스와이프 네비게이션 | 네비게이션 패턴, 레이아웃 리듬 |

## Color System

```
:root {
  --ink:    #112a35   /* 주 텍스트, 어두운 배경 */
  --ink-2:  #244550   /* 보조 텍스트 */
  --paper:  #f5f0e6   /* 메인 배경 (따뜻한 크래프트) */
  --paper-2:#e9e0d2   /* 보조 배경 */
  --white:  #fffdf8   /* 순백이 아닌 따뜻한 화이트 */
  --ocean:  #0e6f78   /* 액센트 (바다/하버) */
  --sky:    #9ad3d8   /* 밝은 하늘 */
  --sun:    #f1b24a   /* 강조, CTA, 알림 */
  --coral:  #d75f48   /* 시간, 경고, 포인트 */
  --leaf:   #7c906b   /* 자연, Option B */
}
```

### 색상 역할
- **coral**: 시간 표시 (`timeline__time`), 날짜 뱃지, 에너지가 필요한 포인트
- **sun**: kicker 하이라이트, 선택 안내, CTA 영역, 결정 사항
- **ocean**: 확정 사항 pill, 타임라인 마커, 탭 컬러
- **leaf**: 자연 관련 옵션 (Blue Mountains), Option B 구분

## Typography

| 용도 | Font | Size | Weight |
|------|------|------|--------|
| 제목 h1 | Pretendard (sans) | 96px → 48px (mobile) | 900 |
| 소제목 h2 | Pretendard | 60px → 38px | 900 |
| 본문 h3 | Pretendard | 23px → 18px | 850 |
| 리드 텍스트 | Pretendard | 20px → 15px | 650 |
| 메타 정보 | SFMono/Menlo (mono) | 11–12px → 9px | 700–900 |
| 내비게이션 | Mono | 10px | 900 |

### 타입 원칙
- `word-break: keep-all` — 한국어 단어 단위 줄바꿈
- `line-height: 0.95` (h1) → `1.55` (lead) — 계층별 행간 구분
- 모노스페이스는 "시스템 정보" (날짜, 시간, 숫자)에만 사용

## Layout System

### 슬라이드 구조
```
.slide {
  display: grid;
  grid-template-rows: auto minmax(0, 1fr) auto;  /* chrome / content / foot */
  width: 100vw;
  height: 100dvh;
}
```

### 주요 레이아웃 패턴
1. **Cover** — 전면 배경 이미지 + 오버레이 + 좌측 타이틀 + 우측 메타
2. **Day Layout** — 좌측 소개(intro + tags) + 우측 타임라인
3. **Harbour (split background)** — 우측 절반 배경 사진 + 좌측 텍스트 + 카드형 스케줄
4. **Bondi (photo strip)** — 좌측 39% 전면 사진 + 우측 콘텐츠
5. **Split Day** — 우측 1/3 배경 사진 + 좌측 2/3에 두 갈래 옵션 그리드
6. **Departure** — 어두운 배경 + 좌측 결정사항 + 우측 타임라인 목록
7. **Stay Appendix** — 사진(figcaption) + 디테일 그리드
8. **Run Appendix** — 탭 네비게이션 + 사진 스테이지
9. **Table Appendix** — 반응형 테이블

## Animation

```css
[data-anim] {
  opacity: 0;
  transform: translateY(16px);
}
.slide.is-active [data-anim] {
  animation: rise 560ms ease forwards;
  animation-delay: calc(var(--delay, 0) * 70ms);
}
```

- 슬라이드 진입 시 순차 페이드인 (staggered)
- `prefers-reduced-motion: reduce` 시 모든 애니메이션 비활성화
- 전환: `680ms cubic-bezier(0.77, 0, 0.175, 1)` — 무겁지 않은 관성 이징

## v2 Design Improvements (2026-07-31)

### 변경 사항 요약

| # | 카테고리 | 변경 내용 |
|---|---------|----------|
| 1 | 타이포 · 가독성 | h2 `letter-spacing: -0.02em` 추가 — 한국어 큰 글씨에서 더 타이트한 느낌 |
| 2 | 타이포 · 리듬 | kicker `letter-spacing: 0.06em` 추가 — 소문자 모노의 가독성 향상 |
| 3 | 컬러 · 깊이 | 슬라이드 배경에 미세한 노이즈 텍스처 (CSS grain) — 종이 느낌 강화 |
| 4 | 레이아웃 | 타임라인 마커에 `transition` 추가 — 슬라이드 진입 시 부드러운 등장 |
| 5 | 호버 · 인터랙션 | route__day 카드에 `transform: translateY(-2px)` 호버 효과 |
| 6 | 그림자 · 깊이 | harbour__schedule 카드에 미세한 `box-shadow` 추가 — 레이어 분리 |
| 7 | 네비게이션 | nav-dots에 hover시 `scale(1.2)` 트랜지션 |
| 8 | 표지 · 임팩트 | cover h1에 `text-shadow` 추가 — 배경 이미지 위 가독성 강화 |
| 9 | 모바일 | pill 컴포넌트 `gap` 줄여 모바일에서 줄바꿈 최소화 |
| 10 | 접근성 | focus-visible 링 컬러를 sun에서 white로 변경 (어두운 배경 대응) |

### 디자인 원칙 (Guizang에서 차용)
1. **절제가 화려함보다 낫다** — 그레인 텍스처도 `opacity: 0.03` 수준
2. **구조가 장식보다 낫다** — 그림자 대신 border/spacing으로 계층 표현
3. **이미지는 1급 시민** — 비율 유지, 상단/좌우 크롭 금지
4. **리듬은 hero 페이지에 있다** — hero/non-hero 교대로 피로도 관리
5. **동적 효과는 선택적** — `prefers-reduced-motion`에서 모두 비활성화

## Navigation UX

- **키보드**: ← → / PageUp PageDown / Home End
- **터치**: 좌우 스와이프 (42px threshold)
- **클릭**: 좌 1/3 뒤로, 우 1/3 앞으로
- **dot navigation**: 우측 고정, 현재 위치 하이라이트
- **내부 링크**: `data-slide-target` 속성으로 슬라이드 간 점프
- **URL hash**: `#N` 형태로 북마크 가능

## File Structure

```
sydney-trip-brief-2026/
├── index.html      ← 단일 파일 덱 (CSS + HTML + JS 인라인)
└── design.md       ← 이 파일 (디자인 시스템 문서)
```

## Version History

| 날짜 | 버전 | 내용 |
|------|------|------|
| 2026-07-30 | v1.0 | 초기 배포 (13슬라이드: 본편 7 + 부록 6) |
| 2026-07-31 | v1.1 | 날짜 수정, 네비게이션 힌트, 접근성 개선 |
| 2026-07-31 | v2.0 | 디자인 개선 (텍스처, 타이포, 인터랙션, 깊이감) |
