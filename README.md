# Word Tower Defense

알파벳 타일로 영단어를 만들면 그 **단어의 뜻**에 따라 다른 능력의 타워가 생기는 타워 디펜스 프로토타입입니다.

## 실행

`index.html`을 브라우저로 열면 바로 실행됩니다 (빌드·설치 불필요).

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

- `Lexicon` — 단어 사전(Set). `Lexicon.loadFromUrl('words.txt')`로 대용량 단어 목록 연동
- `WordValidator` — 규칙 파이프라인. `addRule()`로 금칙어·서버 검증 등 추가
- `Archetypes` — 타워 행동 구현 (shooter / splash / slow / chain / income)
- `AbilityRegistry` — 단어 → 능력 해석: 정확 일치 → 의미 태그 → 일반 단어.
  `loadWordTags({ WORD: [tag] })`로 대규모 의미 태그 데이터 연동
- `Game`, `Enemy`, `Tower`, `Projectile`, `Path` — 디펜스 엔진
- `Renderer`, `UI` — Canvas 렌더링과 DOM 입력 처리
