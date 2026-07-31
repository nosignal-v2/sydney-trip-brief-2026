# Design System · 2026 Sydney Trip Brief

## Visual Identity

이 슬라이드 덱은 **Anthropic Design System**을 기반으로 합니다.
Slate ink on ivory cream — 모노크롬 절제 위에 clay/orange 액센트 하나로 포인트를 주는 에디토리얼 접근입니다.
Pretendard(sans) + Noto Serif KR(본문) 조합으로 한글 가독성을 확보합니다.

## Design References

| 참고 | 요소 | 적용 |
|------|------|------|
| [Anthropic Design System](https://anthropic.com) | Slate #141413 / Cream #faf9f5, clay accent, cream↔black 밴드 리듬 | 전체 색상, 밴드 교대 |
| Anthropic Typography Stack | Serif(디스플레이/본문) + Sans(헤드라인) + Mono(메타) | 3-typeface 계층 |
| [Monocle Magazine](https://monocle.com) | 모노스페이스 메타 정보, 타임라인 | chrome/foot, 시간 표기 |
| [Cereal Magazine](https://readcereal.com) | 여백 활용, serif 본문, 사진 호흡 | lead 텍스트, 커버 |
| [Guizang PPT Skill](https://github.com/op7418/guizang-ppt-skill) | 수평 스와이프, editorial ink 스타일 | 네비게이션, 레이아웃 리듬 |

## Color System (Anthropic-based)

```
:root {
  --ink:    #141413   /* Anthropic Slate — 주 텍스트, 어두운 배경 */
  --ink-2:  #3d3d3a   /* Ink Soft — 보조 텍스트 */
  --paper:  #faf9f5   /* Anthropic Canvas — 메인 배경 (아이보리 크림) */
  --paper-2:#f0eee6   /* Surface Secondary */
  --white:  #faf9f5   /* Canvas와 동일 */
  --ocean:  #6a9bcc   /* Accent Sky — 확정/링크 */
  --sky:    #bcd1ca   /* Accent Cactus — 밝은 보조 */
  --sun:    #d97757   /* Accent Clay — 주 액센트 (시간, 포인트, CTA) */
  --coral:  #d97757   /* sun과 동일 (단일 액센트 정책) */
  --leaf:   #788c5d   /* Accent Olive — 자연, Option B */
}
Dark slides: background #000000 (Anthropic inverse)
```

### 색상 역할
- **clay (#d97757)**: 시간 표시, kicker 하이라이트, border-left 액센트, CTA — 유일한 고채도 색상
- **sky (#6a9bcc)**: 확정 사항 pill, 타임라인 마커, 링크 암시
- **olive (#788c5d)**: 자연 관련 옵션 (Blue Mountains), Option B 구분
- **ink (#141413)**: 제목, 강한 구분, 어두운 배경
- **#000000**: 히어로/임팩트 슬라이드 배경 (Anthropic의 black band)

## Typography (3-Typeface Stack)

| 용도 | Font Stack | Size | Weight |
|------|-----------|------|--------|
| 제목 h1 | Pretendard Variable (--sans) | 96px → 48px (mobile) | 900 |
| 소제목 h2 | Pretendard Variable | 60px → 38px | 900 |
| 본문 h3 | Pretendard Variable | 23px → 18px | 850 |
| 리드/설명 | Noto Serif KR (--serif) | 19px → 15px | 400 |
| 상태 노트 | Noto Serif KR | 14px | 400 |
| 메타 정보 | SFMono/JetBrains Mono (--mono) | 11–12px → 9px | 700–900 |
| 라벨/배지 | Mono uppercase | 9–12px | 800–900 |

### 타입 원칙 (Anthropic 차용)
- **Serif = 읽는 텍스트** (설명, 리드, 노트) — 에세이 같은 느낌
- **Sans = 보는 텍스트** (제목, 네비게이션) — 임팩트와 구조
- **Mono = 시스템 텍스트** (날짜, 시간, 메타) — 데이터 느낌
- `word-break: keep-all` — 한국어 단어 단위 줄바꿈
- `letter-spacing: -0.02em` (h2) — 한국어 큰 글씨 타이트닝
- `letter-spacing: 0.06em` (kicker mono) — 소형 대문자 가독성

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
| 2026-07-31 | v3.0 | Anthropic Design System 테마 적용 (slate/cream, serif 본문, black band) |
