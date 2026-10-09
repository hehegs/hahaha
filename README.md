# Word Tower Defense

알파벳 타일로 영단어를 만들면 그 **단어의 뜻**에 따라 다른 능력의 타워가 생기는 타워 디펜스 프로토타입입니다.

## 실행

`index.html`을 브라우저로 열면 바로 실행됩니다 (빌드·설치 불필요).

## 학습 모드 (단원 낱말)

하단 **단원** 목록에서 6학년 영어(최희경 외) 단원을 고르면 그 단원 낱말만 정답으로 인정됩니다.

- 한글 뜻과 첫 글자(`W _ _ _ _`)가 힌트로 나오고, 타일은 그 낱말을 반드시 만들 수 있게 나옵니다.
- **글자 힌트(5G)**로 한 글자씩 더 볼 수 있고, **다른 낱말(15G)**로 건너뛸 수 있습니다.
- 어구(play soccer 등)는 띄어쓰기 없이 글자만 이어서 만듭니다. 12글자를 넘는 어구는 제외됩니다.
- 낱말 데이터는 `index.html`의 `<script id="unitdata">` JSON입니다. 교체하면 다른 교과서에도 쓸 수 있습니다.
- **자유 모드**를 고르면 모든 영단어를 쓸 수 있습니다.

## 플레이 방법

1. 하단 타일을 클릭(또는 키보드 입력)해 단어를 만듭니다.
2. **단어 확정**(Enter) → 맵의 빈 칸을 클릭해 타워를 배치합니다. 우클릭/Esc로 취소.
3. **웨이브 시작**으로 적을 소환합니다. 생명이 0이 되면 패배.

| 단어 종류 | 예시 | 효과 |
|---|---|---|
| 특수 단어 | GUN, ICE, MINER, FIRE, BOMB, ZAP, SNIPER | 고유 능력 |
| 의미 태그 | SNOW·COLD(감속), FLAME·LAVA(화염), SWORD(무기), GOLD(수입), STORM(번개) | 태그 능력 + 길이 보정 |
| 일반 단어 | TABLE, HOUSE … | 길이² 비례 데미지 |

## 코드 구조 (`index.html` 내부 모듈)

- `Lexicon` — 단어 사전(Set). 기본으로 SCOWL 단어 약 4만 개(3~8글자)가 `index.html`에 내장되어 있고,
  `Lexicon.loadFromUrl('words.txt')`로 더 큰 단어 목록을 추가할 수 있음
- `WordValidator` — 규칙 파이프라인. `addRule()`로 금칙어·서버 검증 등 추가
- `Archetypes` — 타워 행동 구현 (shooter / splash / slow / chain / income)
- `AbilityRegistry` — 단어 → 능력 해석: 정확 일치 → 의미 태그 → 일반 단어.
  `loadWordTags({ WORD: [tag] })`로 대규모 의미 태그 데이터 연동
- `Game`, `Enemy`, `Tower`, `Projectile`, `Path` — 디펜스 엔진
- `Renderer`, `UI` — Canvas 렌더링과 DOM 입력 처리

## 단어 데이터 출처

내장 단어 목록은 [SCOWL](http://wordlist.aspell.net/) (Copyright 2000-2016 Kevin Atkinson)에서 가져왔습니다. 라이선스 전문은 `index.html`의 단어 목록 위 주석에 있습니다.
