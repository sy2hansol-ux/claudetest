# 리서치 노트 (Claude 독자 수집분, 2026-10-14)

> 이 파일은 작업 중간 기록입니다. 최종 보고서가 아니며, 새 세션에서 이어서 작업할 때 참고용입니다.

## 수집 환경 이슈
- 이 세션의 네트워크 정책상 youtube.com / googlevideo.com / i.ytimg.com / socialblade.com 등이 차단(403)되어
  채널 원자료(전 영상 메타데이터, 영상 다운로드, 자막, 음성) 직접 수집이 막혀 있음.
- 허용 필요 도메인: youtube.com, www.youtube.com, m.youtube.com, googlevideo.com(와일드카드), i.ytimg.com, socialblade.com
- 수집 스크립트 계획: yt-dlp --flat-playlist → 영상별 -J 메타 → 상/중/하위·최근 영상 다운로드 → ffmpeg 프레임 추출 → 자동자막(ko) → 음성 F0/RMS 분석

## 정책·수익 구조 (웹 검색으로 확인)
- YPP 2025-07-15: "repetitious content" → "inauthentic content"로 명칭 변경, 대량생산·반복·템플릿형 콘텐츠 판단 강화.
  공식 도움말: 템플릿으로 만든 듯 영상 간 변화가 거의 없는 콘텐츠, 이미지 슬라이드쇼/스크롤 텍스트(해설·교육적 가치 없음) 등이 예시.
  "평균 시청자가 영상마다 다르다는 걸 분명히 알 수 있으면 수익화 가능". 채널 단위로 적용(일부 영상 위반 시 채널 전체 수익화 해제 가능).
  https://support.google.com/youtube/answer/1311392
- 일본: 2026년 연초 AI 양산형 쇼츠 채널 수익화 정지·계정 삭제 보고 다수 (AI 음성만, 템플릿 구성, 슬라이드 중심, 소재 재사용, 매일 대량 투고가 공통점).
  https://hashout.jp/ai/267/ , https://bloomeria.jp/blog/youtube-ai-slop-demonetization-2026
- 쇼츠 조회수 집계 변경(2025-03-31): 재생/반복재생 시작마다 1회 카운트. 수익·YPP 기준은 기존 지표 'engaged views' 유지.
  → 2025-03-31 이후 공개 조회수는 수익 기준 조회수보다 부풀려져 있음.
- 쇼츠 수익: 국가별 쇼츠 피드 광고 → 음악 비용 차감 → 크리에이터 풀 → engaged views 점유율로 배분 → 크리에이터 45%.
  개인 배분액은 음악 사용 여부와 무관(공식 도움말). https://support.google.com/youtube/answer/12504220
- YPP 기준: 구독 1,000 + 최근 90일 쇼츠 유효조회 1,000만 (또는 시청시간 4,000h). 팬 후원 1단계 500명 + 300만.
- 쇼츠 RPM: AIR Media-Tech 2025 국가별 — 한국 약 $0.185, 일본 약 $0.144, 미국 약 $0.328 /1,000회 (파트너 채널 표본).
  일본 국내 자료: 1회 재생당 0.003~0.01엔 (=1,000회당 3~10엔). 한국 국내 자료: 1,000회당 35~104원 수준.
  https://air.io/en/monetization/what-rpm-can-you-expect-from-shorts-in-2026 , https://biz-journal.jp/it/post_356666.html
- AI 합성 콘텐츠 공개 라벨: 실제 인물·장소·사건으로 오인 가능한 '사실적' 합성물은 공개 의무. 대본·아이디어·자동자막 등 생산성 용도 AI는 공개 불필요.
  https://blog.youtube/news-and-events/disclosing-ai-generated-content
- YouTube Data API 업로드: 2020-07-28 이후 생성된 미감사(unverified) API 프로젝트로 videos.insert 하면 비공개로 고정 → 감사(audit) 필요.
  기본 쿼터 10,000 units/일, videos.insert는 2025-12 이후 약 100 units(구 문서 1,600) — 콘솔에서 확인 필요.
- YouTube 쇼핑 제휴 프로그램 일본 출시: 2026-02-19, 첫 파트너 라쿠텐 시장. 영상에 라쿠텐 상품 태그 → 판매 시 수수료.
  https://global.rakuten.com/corp/news/press/2026/0219_01.html

## 일본 법규
- 스테마 규제(경품표시법 지정고시, 2023-10-01 시행): 사업자 의뢰·대가 있는 표시는 'PR/広告' 명시 필요. 제휴링크도 해당 가능.
- 저작권법 32조 인용: 공정한 관행 + 정당한 범위, 실무 요건 = 주종관계, 명료구별, 출처명시. 스크린샷 인용은 판례 갈림(지재고재 2023: 인용 인정 사례).
- 신용훼손죄(형법 233조)/명예훼손(230조): 기업의 경제적 신용에 관한 허위 사실 유포 시 성립 가능.

## 일본 시장·소재
- 일본 YouTube 활성 사용자 약 8,100만(2026 추정, 인구 66%), Google Ads 도달 9,680만. https://japanbuzz.info/data/youtube-users-in-japan/
- 식 잡학(食の雑学) 계열 수요 검증: '「食の雑学」をゆっくり解説' 등록자 41.2만(2026-07). 채널 매매 사이트에 잡학 쇼츠 채널(5.3만 구독, 최고 월 26만엔, 1편 900만 재생) 매물.
- PB 제조원: 제조소 고유기호 제도(2015 식품표시법 이후 엄격화), 세븐 프리미엄 일부는 明星食品/東洋水産 등 대형 메이커 제조 보도.
- 2026 일본 식품 트렌드 예측: 엔젤헤어 초코, 사고, 3D 과일 아이스(한국발, 2025-12 일본 상륙), 에그타르트, 쌀가루 쫀득 식감, 두바이 다이후쿠(한국발) 등.
- 코스트코 재판매점(再販店) 확산, 업무슈퍼 팬덤.

## 기술 스택 후보
- TTS(일본어): ElevenLabs(v3, 자연스러움 최상위권, 타임스탬프 API), Google Chirp 3 HD(ja-JP, 저가 대량), Azure ja-JP(단어 경계 이벤트),
  OpenAI gpt-4o-mini-tts, 로컬 AivisSpeech / Style-Bert-VITS2, VOICEVOX(무료·크레딧 표기 "VOICEVOX:ずんだもん" 조건 상업 이용 가능).
  ABEJA 벤치마크 일본어 품질: Polly 91.3 / gpt-4o-mini-tts 90.2 / Chirp3 HD 89.6 / ElevenLabs 89.0 (차이 작음).
- 렌더링: Remotion(3인 이하 무료, 자동화 회사 라이선스 $0.01/렌더·최소 $100/월), 또는 FFmpeg+Pillow(무료).
- 코스트코 코리아 'Nusspo 두바이 초콜릿 크림 스프레드 1kg': 헤이즐넛/피스타치오 크림 반반, 카다이프 3% (채널 1위 영상 소재 실재 확인).
