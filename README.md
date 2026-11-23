# 비공식듀오 MVP

레드크리스탈 중매사가 엄선한 소개팅 프로필. Next.js + Supabase + Vercel.

## 기능
- 로그인 없이 남성/여성 공개 프로필 목록과 상세 보기
- 관리자 이메일 로그인, 프로필 등록/수정/삭제, 사진 업로드, 공개/비공개
- 모바일 반응형

## 시작
1. Node.js 20 이상 설치 후 `npm install`
2. Supabase 새 프로젝트 생성 → SQL Editor에서 `supabase/schema.sql` 실행
3. Supabase Authentication > Users에서 관리자 이메일 계정 생성. 이메일 인증 완료 확인
4. 해당 사용자의 UUID로 SQL Editor에서 `insert into public.admins(user_id) values ('UUID');` 실행
5. `.env.example`을 `.env.local`로 복사하고 프로젝트 URL과 publishable/anon key 입력. **service_role 키를 절대 넣지 마세요.**
6. `npm run dev` → http://localhost:3000 / 관리자 http://localhost:3000/admin
7. GitHub 저장소에 올리고 Vercel에서 Import Project. 환경 변수 2개를 Vercel에 등록 후 Deploy

## 운영 및 보안 참고
- 관리자 회원가입 페이지는 없습니다. Supabase에서 관리자 계정을 직접 생성하고 `admins` 테이블에 승인합니다.
- 공개 프로필과 공개 Storage 버킷의 사진은 누구나 열람할 수 있습니다. 업로드 전에 사진/정보 공개 동의를 반드시 확보하세요.
- 비공개 전환 시 DB 목록/상세 조회는 차단되지만 **이미 발급된 공개 사진 URL은 계속 접근 가능**합니다. 공개 취소/삭제 요청 시 Storage에서 원본 파일도 별도로 삭제해야 합니다. 운영 전 비공개 사진 버킷 + 서명 URL 또는 서버 프록시로 개선을 권장합니다.
- 파일 제거 버튼은 프로필 연결만 제거하며 Storage 원본은 삭제하지 않습니다. 운영 시 스토리지 정리 기능을 추가하세요.
- 공개 프로필은 검색 엔진에도 노출될 수 있습니다. 필요한 경우 robots 정책 및 접근 제어를 추가하세요.
- 서비스 출시 전 개인정보 처리방침, 보유기간, 동의 철회 및 삭제 절차, 관리자 권한/접근 기록을 정비하세요.
- 프로필 삭제는 DB에서 즉시 삭제되며 복구 기능은 없습니다.
- Vercel Hobby 요금제는 상업적 사용 조건을 확인하고 적절한 요금제를 선택하세요.
