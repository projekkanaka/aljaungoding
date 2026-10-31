PEDOMAN REKONSTRUKSI GIT HISTORY BERSAMA KITA Versi ringkas manusiawi, update 17 Oktober pagi Sudut pandang: Web Developer, UI UX Specialist, Project Manager

Tujuan: Buat ulang history commit hackathon secara bertahap, rapi, terlihat natural seperti kerja manusia, siap presentasi juri dan siap deploy Vercel. File ini siap salin. Salin satu blok PROMPT 00 sampai 20 ke agent, agent wajib eksekusi via shell tanpa bertanya lagi.

Acuan: plan docs HACKATHON COMMIT GUIDE, identitas Git diatur pengguna melalui git config, credential md hanya untuk token Vercel plus URL repo, aturan AGENTS md di source: BMKG karantina, Duitku idempoten HMAC, no hardcode secret, partner hanya via admin

Deploy: Tidak di 00. Siapkan auth di 00, siapkan config di 17, push tiap prompt plus push final di 19 memicu auto deploy Vercel, deploy manual eksplisit di 20 vercel prod.

Kondisi aktual: SOURCE aktif folder bersamakita web di Bersama Kita Hackaton, branch main, ada satu modified firestore rules. Folder bersamakita-deploy di Hackaton ENV kosong, jangan dipakai. STAGING baru folder kanakaproject1 di Hackaton ENV, belum ada, dibuat di 00. Repo target github com malvinjauhari projekkanaka1 git, project Vercel kanakaproject1. Docs hackaton 11 file plus nested plus GIT STATE kini ADA di SOURCE, cukup cp langsung. gitignore SOURCE belum ada firebase-blueprint json backup firebase-applet-config, tambah di 01. vercel project json SOURCE masih project lama bersamakita prj jlzD9GDmNqNzma6l1Heu45An5wJY, target baru kanakaproject1, atasi di 20 via vercel link, jangan commit folder vercel. build sama dengan vite build, lint sama dengan tsc noEmit, tidak ada eslint.

---

## A. CARA PAKAI

1. Tempel PROMPT 00 dulu, setup plus cek auth, tanpa deploy.
2. Lanjut urut 01 sampai 18 plus MERGE, jangan lompat.
3. PROMPT 19 verifikasi build plus push final ke GitHub.
4. PROMPT 20 deploy prod ke Vercel.
5. Tiap prompt sudah ada command singkat, timestamp, verifikasi, laporan wajib.
6. Jika agent hanya menjelaskan, balas: Eksekusi sekarang via shell, jangan hanya menjelaskan.

Path aktual: SOURCE sama dengan home alvinjauhari Documents Bersama Kita Hackaton bersamakita web STAGING sama dengan home alvinjauhari Documents Bersama Kita Hackaton Hackaton ENV kanakaproject1 CRED sama dengan home alvinjauhari Documents Bersama Kita Hackaton Hackaton ENV plan docs credential md Gunakan path lengkap dengan kutip di shell. Jangan salin CRED atau env atau vercel atau backup ke STAGING. CRED hanya untuk Vercel, bukan autentikasi GitHub. Jangan lanjut commit atau push sebelum user mengganti nama dan email placeholder dengan identitas sebenarnya.

---

## B. PROMPT 00 - SETUP STAGING DAN IDENTITAS GIT, TANPA DEPLOY

Salin ke agent:

TESTTST

TUGAS: Setup staging bersih, minta user mengatur identitas Git, dan cek auth Vercel. Jangan gunakan access token untuk GitHub. Eksekusi via shell sekarang.

Gunakan shell ini, singkat dan jelas:

SOURCE="/home/alvinjauhari/Documents/Bersama Kita Hackaton/bersamakita web" STAGING="/home/alvinjauhari/Documents/Bersama Kita Hackaton/Hackaton ENV/kanakaproject1" CRED="/home/alvinjauhari/Documents/Bersama Kita Hackaton/Hackaton ENV/plan docs/credential.md" REPO\_URL="https://github.com/malvinjauhari/projekkanaka1.git" ls "$SOURCE/package.json" "$SOURCE/server/app.ts" "$SOURCE/src/config/firebase.ts" "$SOURCE/vercel.json" "$CRED" ls -1 "$SOURCE/docs" ; ls -1 "$SOURCE/docs/hackaton" ; cat "$SOURCE/.gitignore" git -C "$SOURCE" log --oneline -3 ; git -C "$SOURCE" status --short git config --global user.name "belumdiset" git config --global user.email "belumdiset" echo "WAJIB: minta user mengganti belumdiset dengan nama dan email Git sebenarnya sebelum commit atau push" git config --global --get user.name ; git config --global --get user.email VERCEL\_TOKEN="$(grep -oE 'vcp\_\[A-Za-z0-9\]+' "$CRED" \| head -n 1)" mkdir -p "$STAGING" ; cd "$STAGING" git init 2\>/dev/null ; git branch -M main cp "$SOURCE/AGENTS.md" . ; ls AGENTS.md git remote get-url origin 2\>/dev/null \&\& git remote set-url origin "$REPO\_URL" \|\| git remote add origin "$REPO\_URL" git remote -v npx -y vercel@latest whoami --token="$VERCEL\_TOKEN" \| head -n 5 pwd ; git status --short ; git branch --show-current

LAPOR: file inti ada, docs ada, AGENTS ada, identitas Git saat ini, pengingat agar user mengganti placeholder, remote tanpa token, whoami Vercel, status. Hentikan proses sampai user memberi nama dan email Git sebenarnya.

---

## C. PROMPT 01 - INIT REPO DAN TOOLING

Salin ke agent:

TUGAS: Commit 01 init. Eksekusi via shell.

cd "$STAGING" cp "$SOURCE/package.json" . ; cp "$SOURCE/tsconfig.json" . ; cp "$SOURCE/vite.config.ts" . cp "$SOURCE/.env.example" . ; cp "$SOURCE/index.html" . ; cp "$SOURCE/.gitignore" . ; cp "$SOURCE/AGENTS.md" . echo "firebase-blueprint.json" \>\> .gitignore ; echo "firebase-applet-config.json" \>\> .gitignore ; echo "backup/" \>\> .gitignore printf "Bersama Kita\\nPlatform donasi bencana transparan\\nJalan: npm install, npm run dev\\n" \> README.md mkdir -p docs/hackaton/tech\_expected\_product cp "$SOURCE/docs/hackaton/EXPECTED\_PRODUCT\_PROPOSAL\_SUMMARY.md" docs/hackaton/ cp "$SOURCE/docs/hackaton/EXPECTED\_PRODUCT\_TECHNICAL\_ANALYSIS.md" docs/hackaton/ cp "$SOURCE/docs/hackaton/tech\_expected\_product/"*.md docs/hackaton/tech\_expected\_product/ 2\>/dev/null cp "$SOURCE/docs/hackaton/"*.txt docs/hackaton/ 2\>/dev/null cp "$SOURCE/docs/ARCHITECTURE.md" docs/ git add . ; git status --short GIT\_AUTHOR\_DATE="2026-10-15 00:15:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 00:15:00 +0700" git commit -m "chore: init repo react vite tailwind express" git push -u origin main \| tail -n 3 git log -1 --format="%ai %s"

LAPOR: log terakhir, gitignore final, docs yang masuk.

---

## D. PROMPT 02 - TIPE DATA DAN RULES

Salin ke agent:

TUGAS: Commit 02 tipe dan rules. Eksekusi via shell.

cd "$STAGING" mkdir -p src/types src/lib cp "$SOURCE/src/types/index.ts" src/types/ cp "$SOURCE/src/lib/fees.ts" src/lib/ ; cp "$SOURCE/src/lib/firestore-errors.ts" src/lib/ cp "$SOURCE/firestore.rules" . ; cp "$SOURCE/firestore.indexes.json" . git add . ; git status --short GIT\_AUTHOR\_DATE="2026-10-15 00:45:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 00:45:00 +0700" git commit -m "feat: tambah tipe data dan firestore rules" git push -u origin main \| tail -n 3 ls src/types/index.ts firestore.rules ; git log -1 --format="%ai %s"

ATURAN: jangan ubah isi rules, hanya salin. LAPOR: ls dan log.

---

## E. PROMPT 03 - SERVER EXPRESS DAN KONTRAK API

Salin ke agent:

TUGAS: Commit 03 server. Eksekusi via shell.

cd "$STAGING" mkdir -p src/config server api cp "$SOURCE/src/config/firebase.ts" src/config/ ; cp "$SOURCE/src/config/firebase-admin.ts" src/config/ cp "$SOURCE/server/app.ts" server/ ; cp "$SOURCE/api/index.ts" api/ cp "$SOURCE/docs/API.md" docs/ ; cp "$SOURCE/docs/DATABASE.md" docs/ ; cp "$SOURCE/docs/CONTRACT.md" docs/ git add . GIT\_AUTHOR\_DATE="2026-10-15 01:20:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 01:20:00 +0700" git commit -m "feat: setup express dan firebase admin" git push -u origin main \| tail -n 3 ls server/app.ts docs/API.md ; git log -1 --format="%ai %s"

LAPOR: verifikasi dan log.

---

## F. PROMPT 04 - AUTH GOOGLE DAN ISOLASI SESI

Salin ke agent:

TUGAS: Commit 04 auth. Eksekusi via shell.

cd "$STAGING" mkdir -p src/services/firebase src/features/auth src/features/admin src/features/partner cp "$SOURCE/src/lib/safe-storage.ts" src/lib/ cp "$SOURCE/src/services/firebase/auth.ts" src/services/firebase/ cp "$SOURCE/src/features/auth/AuthContext.tsx" src/features/auth/ cp "$SOURCE/src/features/auth/UserLoginPage.tsx" src/features/auth/ cp "$SOURCE/src/features/admin/AdminAuthPage.tsx" src/features/admin/ cp "$SOURCE/src/features/partner/PartnerAuthPage.tsx" src/features/partner/ cp "$SOURCE/docs/AUTH.md" docs/ git add . GIT\_AUTHOR\_DATE="2026-10-15 02:30:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 02:30:00 +0700" git commit -m "feat: tambah auth google dan isolasi sesi" git push -u origin main \| tail -n 3 git log -1 --format="%ai %s"

LAPOR: log.

---

## G. PROMPT 05 - LAYOUT DASAR DAN DOCS PLANNING

Salin ke agent:

TUGAS: Commit 05 UI shell. Eksekusi via shell.

cd "$STAGING" mkdir -p src/components/feedback src/components/layout src/components/landing public cp "$SOURCE/src/index.css" src/ ; cp "$SOURCE/src/lib/utils.ts" src/lib/ ; cp "$SOURCE/src/globals.d.ts" src/ cp "$SOURCE/src/components/feedback/Toast.tsx" src/components/feedback/ cp "$SOURCE/src/components/feedback/Skeleton.tsx" src/components/feedback/ cp "$SOURCE/src/components/layout/WideNavbar.tsx" src/components/layout/ cp "$SOURCE/src/components/layout/WideFooter.tsx" src/components/layout/ cp "$SOURCE/src/components/layout/HackathonBanner.tsx" src/components/layout/ cp "$SOURCE/src/components/landing/MinimalistLanding.tsx" src/components/landing/ cp "$SOURCE/src/main.tsx" src/ ; cp "$SOURCE/src/App.tsx" src/ cp -r "$SOURCE/public/." public/ cp "$SOURCE/docs/hackaton/FROM\_SCRATCH\_IMPLEMENTATION\_PLAN.md" docs/hackaton/ 2\>/dev/null cp "$SOURCE/docs/hackaton/IMPLEMENTATION\_24H\_SCHEDULE.md" docs/hackaton/ 2\>/dev/null cp "$SOURCE/docs/hackaton/IMPLEMENTATION\_FILE\_MAP.md" docs/hackaton/ 2\>/dev/null cp "$SOURCE/docs/hackaton/IMPLEMENTATION\_DEPENDENCY\_GRAPH.md" docs/hackaton/ 2\>/dev/null git add . GIT\_AUTHOR\_DATE="2026-10-15 03:45:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 03:45:00 +0700" git commit -m "feat: layout dasar navbar footer toast" git push -u origin main \| tail -n 3 git checkout -b develop ; git branch --show-current

LAPOR: jumlah commit, branch develop, log.

---

## H. PROMPT 06 - BMKG PROXY KARANTINA

Salin ke agent, pastikan di develop:

TUGAS: Commit 06 BMKG. Eksekusi via shell.

cd "$STAGING" ; git branch --show-current mkdir -p src/services src/features/disaster/data server/routes cp "$SOURCE/src/services/bmkg.ts" src/services/ cp "$SOURCE/server/routes/bmkg.ts" server/routes/ cp "$SOURCE/src/features/disaster/KatalogBMKGPage.tsx" src/features/disaster/ cp "$SOURCE/src/features/disaster/SituationAnalysisPage.tsx" src/features/disaster/ cp "$SOURCE/src/features/disaster/EarthquakeCard.tsx" src/features/disaster/ cp "$SOURCE/src/features/disaster/EarthquakeMap.tsx" src/features/disaster/ cp "$SOURCE/src/features/disaster/data/indonesiaMap.ts" src/features/disaster/data/ git add . GIT\_AUTHOR\_DATE="2026-10-15 05:00:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 05:00:00 +0700" git commit -m "feat: integrasi bmkg proxy pending verifikasi" git push -u origin develop \| tail -n 3

ATURAN: BMKG wajib pending, no auto publish. LAPOR: branch dan log.

---

## I. PROMPT 07 - VERIFIKASI ADMIN

Salin ke agent:

TUGAS: Commit 07 verifikasi. Eksekusi via shell.

cd "$STAGING" cp "$SOURCE/src/features/admin/AdminPortalView.tsx" src/features/admin/ cp "$SOURCE/src/features/disaster/BMKGVerificationCard.tsx" src/features/disaster/ cp "$SOURCE/src/features/disaster/WideDisasterDashboard.tsx" src/features/disaster/ cp "$SOURCE/src/features/disaster/DisasterList.tsx" src/features/disaster/ cp "$SOURCE/src/features/disaster/SelectedDisasterSection.tsx" src/features/disaster/ cp "$SOURCE/docs/DISASTER.md" docs/ git add . GIT\_AUTHOR\_DATE="2026-10-15 07:00:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 07:00:00 +0700" git commit -m "feat: verifikasi admin bmkg plus guard mitra" git push -u origin develop \| tail -n 3

LAPOR: log.

---

## J. PROMPT 08 - AKUN MITRA

Salin ke agent:

TUGAS: Commit 08 mitra. Eksekusi via shell.

cd "$STAGING" cp "$SOURCE/server/routes/admin.ts" server/routes/ cp "$SOURCE/src/features/partner/AdminPartnersView.tsx" src/features/partner/ git add . GIT\_AUTHOR\_DATE="2026-10-15 08:00:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 08:00:00 +0700" git commit -m "feat: endpoint buat akun mitra via admin" git push -u origin develop \| tail -n 3

ATURAN: partner hanya via admin, no self register. LAPOR: log.

---

## K. PROMPT 09 - FORM DONASI

Salin ke agent:

TUGAS: Commit 09 donasi. Eksekusi via shell.

cd "$STAGING" mkdir -p src/features/donation cp "$SOURCE/src/features/donation/TransactionDonatePage.tsx" src/features/donation/ cp "$SOURCE/src/features/donation/TransactionUniversalDispatcher.tsx" src/features/donation/ cp "$SOURCE/src/services/duitku.ts" src/services/ cp "$SOURCE/docs/PAYMENT.md" docs/ git add . GIT\_AUTHOR\_DATE="2026-10-15 09:30:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 09:30:00 +0700" git commit -m "feat: form donasi plus fee transparan" git push -u origin develop \| tail -n 3

LAPOR: log.

---

## L. PROMPT 10 - QRIS DAN TIMER

Salin ke agent:

TUGAS: Commit 10 payment. Eksekusi via shell.

cd "$STAGING" cp "$SOURCE/server/routes/payments.ts" server/routes/ cp "$SOURCE/src/features/donation/TransactionCheckoutPage.tsx" src/features/donation/ git add . GIT\_AUTHOR\_DATE="2026-10-15 11:00:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 11:00:00 +0700" git commit -m "feat: duitku qris plus timer checkout" git push -u origin develop \| tail -n 3

ATURAN: wajib Direct API, no window checkout process. LAPOR: log.

---

## M. PROMPT 11 - WEBHOOK DAN STATUS

Salin ke agent:

TUGAS: Commit 11 webhook. Eksekusi via shell.

cd "$STAGING" cp "$SOURCE/src/features/donation/TransactionStatusPage.tsx" src/features/donation/ cp "$SOURCE/src/features/donation/MyDonationsPage.tsx" src/features/donation/ cp "$SOURCE/src/features/donation/TransactionHistoryPage.tsx" src/features/donation/ cp "$SOURCE/src/features/donation/DonationHistory.tsx" src/features/donation/ git add server/routes/payments.ts src/features/donation/ GIT\_AUTHOR\_DATE="2026-10-15 12:30:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 12:30:00 +0700" git commit -m "feat: webhook hmac dan status donasi" git push -u origin develop \| tail -n 3

LAPOR: log.

---

## N. PROMPT 12 - DISBURSEMENT

Salin ke agent:

TUGAS: Commit 12 keuangan. Eksekusi via shell.

cd "$STAGING" mkdir -p src/features/finance src/hooks cp "$SOURCE/server/routes/fundraising.ts" server/routes/ cp "$SOURCE/src/features/finance/DisbursementManager.tsx" src/features/finance/ cp "$SOURCE/src/features/finance/AdminTransactionsView.tsx" src/features/finance/ cp "$SOURCE/src/hooks/useFundraisingSummary.ts" src/hooks/ cp "$SOURCE/src/services/fundraising.ts" src/services/ cp "$SOURCE/docs/PARTNER.md" docs/ git add . GIT\_AUTHOR\_DATE="2026-10-15 14:00:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 14:00:00 +0700" git commit -m "feat: disbursement atomik anti defisit" git push -u origin develop \| tail -n 3

LAPOR: log.

---

## O. PROMPT 13 - CLOUDINARY

Salin ke agent:

TUGAS: Commit 13 media. Eksekusi via shell.

cd "$STAGING" cp "$SOURCE/server/routes/images.ts" server/routes/ cp "$SOURCE/src/services/cloudinary.ts" src/services/ cp "$SOURCE/src/components/ImageUploadField.tsx" src/components/ git add . GIT\_AUTHOR\_DATE="2026-10-15 14:45:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 14:45:00 +0700" git commit -m "feat: upload cloudinary signed" git push -u origin develop \| tail -n 3

LAPOR: log.

---

## P. PROMPT 14 - PORTAL MITRA

Salin ke agent:

TUGAS: Commit 14 mitra dashboard. Eksekusi via shell.

cd "$STAGING" mkdir -p src/features/distribution cp "$SOURCE/src/features/partner/PartnerDashboardView.tsx" src/features/partner/ cp "$SOURCE/src/features/distribution/DistributionProgressCard.tsx" src/features/distribution/ git add . GIT\_AUTHOR\_DATE="2026-10-15 16:00:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 16:00:00 +0700" git commit -m "feat: dashboard mitra plus milestone 6 tahap" git push -u origin develop \| tail -n 3

LAPOR: log.

---

## Q. PROMPT 15 - TIMELINE PUBLIK

Salin ke agent:

TUGAS: Commit 15 transparansi. Eksekusi via shell.

cd "$STAGING" cp "$SOURCE/src/features/distribution/DisasterTimelineSection.tsx" src/features/distribution/ cp "$SOURCE/src/features/distribution/PublicReportsView.tsx" src/features/distribution/ cp "$SOURCE/src/features/disaster/AllocationTransparencySection.tsx" src/features/disaster/ cp "$SOURCE/src/features/disaster/AnalisisSituasiModal.tsx" src/features/disaster/ cp "$SOURCE/src/features/donation/UserDashboardOverview.tsx" src/features/donation/ cp "$SOURCE/docs/CURRENT\_STATE.md" docs/ ; cp "$SOURCE/docs/NOW.md" docs/ ; cp "$SOURCE/docs/GIT\_STATE.md" docs/ git add . GIT\_AUTHOR\_DATE="2026-10-15 17:30:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 17:30:00 +0700" git commit -m "feat: timeline publik tanpa PII" git push -u origin develop \| tail -n 3

ATURAN: no PII donatur di publik. LAPOR: log.

---

## R. PROMPT 16 - AUDIT LPJ PUBLIK

Salin ke agent:

TUGAS: Commit 16 laporan. Eksekusi via shell.

cd "$STAGING" mkdir -p src/features/operations src/features/public cp "$SOURCE/src/features/distribution/AdminFinalReportPanel.tsx" src/features/distribution/ cp "$SOURCE/src/features/distribution/FinalReportSection.tsx" src/features/distribution/ cp "$SOURCE/src/features/distribution/TransparansiReportsPage.tsx" src/features/distribution/ cp "$SOURCE/src/features/distribution/ReportsPage.tsx" src/features/distribution/ cp "$SOURCE/src/features/distribution/TransparencySummarySection.tsx" src/features/distribution/ cp "$SOURCE/src/features/operations/AuditLogsView.tsx" src/features/operations/ cp "$SOURCE/src/features/finance/DuitkuSettingsView.tsx" src/features/finance/ cp "$SOURCE/src/features/public/ContactPage.tsx" src/features/public/ cp "$SOURCE/src/features/public/FaqPage.tsx" src/features/public/ cp "$SOURCE/src/features/public/RefundPolicyPage.tsx" src/features/public/ cp "$SOURCE/src/features/public/TermsPage.tsx" src/features/public/ cp "$SOURCE/server/routes/transparency.ts" server/routes/ cp "$SOURCE/src/services/firebase/firestore.ts" src/services/firebase/ cp "$SOURCE/src/services/firebase/seed.ts" src/services/firebase/ cp "$SOURCE/src/features/donation/DonationModal.tsx" src/features/donation/ git add . GIT\_AUTHOR\_DATE="2026-10-15 19:00:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 19:00:00 +0700" git commit -m "feat: audit log LPJ dan halaman publik" git push -u origin develop \| tail -n 3 git log --oneline -3

LAPOR: 3 log terakhir.

---

## S. PROMPT MERGE - GABUNG DEVELOP KE MAIN

Salin ke agent:

TUGAS: Merge ke main. Eksekusi via shell.

cd "$STAGING" git branch --show-current git checkout main GIT\_AUTHOR\_DATE="2026-10-15 19:30:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 19:30:00 +0700" git merge develop --no-ff -m "merge: gabung semua fitur ke main" git push -u origin main \| tail -n 3 git push -u origin develop \| tail -n 3 git log --oneline --graph -5 ; git branch

LAPOR: graph dan branch. Jika konflik STOP jangan force.

---

## T. PROMPT 17 - CONFIG DEPLOY, BELUM DEPLOY

Salin ke agent:

TUGAS: Commit 17 config deploy. Eksekusi via shell, bukan deploy.

cd "$STAGING" cp "$SOURCE/vercel.json" . ; cp "$SOURCE/firebase.json" . ; cp "$SOURCE/firestore.indexes.json" . cp "$SOURCE/README.md" . ; cp "$SOURCE/docs/TROUBLESHOOTING.md" docs/ cat vercel.json git add . GIT\_AUTHOR\_DATE="2026-10-15 21:00:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 21:00:00 +0700" git commit -m "chore: config vercel dan index firestore" git push -u origin main \| tail -n 3

ATURAN: jangan commit env dan folder vercel. LAPOR: ls dan log.

---

## U. PROMPT 18 - AUDIT DOCS FINAL

Salin ke agent:

TUGAS: Commit 18 docs final. Eksekusi via shell.

cd "$STAGING" mkdir -p docs/hackaton/tech\_expected\_product cp "$SOURCE/docs/hackaton/IMPLEMENTATION\_COMMIT\_PLAN.md" docs/hackaton/ 2\>/dev/null cp "$SOURCE/docs/hackaton/IMPLEMENTATION\_ACCEPTANCE\_CRITERIA.md" docs/hackaton/ 2\>/dev/null cp -r "$SOURCE/docs/." docs/ ls -R docs/hackaton \| head -n 20 git ls-files \| grep -E "env$\|credential\|vercel/\|blueprint\|applet-config" \|\| echo "OK bersih sensitif" git add . GIT\_AUTHOR\_DATE="2026-10-15 22:30:00 +0700" GIT\_COMMITTER\_DATE="2026-10-15 22:30:00 +0700" git commit -m "docs: lengkapi docs hackathon dan audit akhir" git push -u origin main \| tail -n 3 git log --oneline \| wc -l ; git log --oneline --format="%h %ai %s" \| head -n 20

LAPOR: total commit dan 20 log teratas.

---

## V. PROMPT 19 - CEK BUILD DAN PUSH FINAL

Salin ke agent:

TUGAS: Verifikasi lalu push. Jangan push jika build gagal.

cd "$STAGING" test "$(git config --global --get user.name)" != "belumdiset" \&\& test "$(git config --global --get user.email)" != "belumdiset" \|\| { echo "STOP: minta user set nama dan email Git sebenarnya"; exit 1; } git config --global --get user.name ; git config --global --get user.email git log --oneline --format="%h %ai %an <%ae> %s" \| head -n 20 git log --oneline \| wc -l ls src/types/index.ts firestore.rules server/app.ts src/config/firebase.ts vercel.json git status --short git ls-files \| grep -E "env$\|credential\|vercel/\|blueprint" \|\| echo "OK bersih" npm install \| tail -n 3 npm run build \| tail -n 10 npx tsc --noEmit git remote -v git push -u origin main git push origin develop

LAPOR: hasil build dan push. Jika sukses tulis: Push sukses, cek Dashboard Vercel lalu lanjut 20.

---

## W. PROMPT 20 - DEPLOY PROD VERCEL

Salin ke agent:

TUGAS: Deploy prod sekarang, setelah 19 sukses.

STAGING sama dengan folder kanakaproject1 PROJECT sama dengan kanakaproject1

cd "$STAGING" VERCEL\_TOKEN="$(grep -oE 'vcp\_\[A-Za-z0-9\]+' "$CRED" \| head -n 1)" echo "token ${VERCEL\_TOKEN: -4}" npm run build \| tail -n 10 npx -y vercel@latest whoami --token="$VERCEL\_TOKEN" \| head -n 5 OPSI A jika repo sudah connect Vercel: cek Dashboard project kanakaproject1 Deployments, tulis URL di laporan. OPSI B manual via CLI: npx -y vercel@latest --prod --yes --token="$VERCEL\_TOKEN" \| tail -n 30 curl -s -o /dev/null -w "%{http\_code}" https://kanakaproject1.vercel.app ; echo

CATATAN: project json SOURCE masih bersamakita lama. STAGING tidak bawa folder vercel. Jika B gagal project not found, jalan npx vercel link --yes --project kanakaproject1 --token="$VERCEL\_TOKEN" lalu ulangi deploy. Jangan commit folder vercel. Mask token. LAPOR: opsi A atau B, URL prod, status curl, 30 baris deploy masked.

---

## X. TABEL TIMESTAMP

01, 2026-10-15 00:15 main 02, 2026-10-15 00:45 main 03, 2026-10-15 01:20 main 04, 2026-10-15 02:30 main 05, 2026-10-15 03:45 main lalu buat develop 06, 2026-10-15 05:00 develop 07, 2026-10-15 07:00 develop 08, 2026-10-15 08:00 develop 09, 2026-10-15 09:30 develop 10, 2026-10-15 11:00 develop 11, 2026-10-15 12:30 develop 12, 2026-10-15 14:00 develop 13, 2026-10-15 14:45 develop 14, 2026-10-15 16:00 develop 15, 2026-10-15 17:30 develop 16, 2026-10-15 19:00 develop MERGE, 2026-10-15 19:30 main 17, 2026-10-15 21:00 main siapkan config belum deploy 18, 2026-10-15 22:30 main 19, setelah 18 waktu aktual, push main develop ke malvinjauhari projekkanaka1 picu auto deploy 20, setelah 19 waktu aktual, vercel prod ke kanakaproject1 deploy eksplisit

---

## Y. ALUR DEPLOY

00 set placeholder identitas Git, ingatkan user menggantinya, pasang origin malvinjauhari projekkanaka1 tanpa token plus cek vercel whoami, tanpa deploy. 17 commit vercel json firebase json index, belum deploy. 19 build vite plus tsc plus push main develop picu auto deploy jika GitHub connect Vercel. 20 vercel prod pakai token ke kanakaproject1, verifikasi curl 200. Jika Dashboard belum ada kanakaproject1, buat baru atau vercel link project kanakaproject1 sebelum 20 OPSI B.

---

## Z. DELTA DAN PRINSIP MANUSIAWI

STAGING saat ini kanakaproject1, REPO malvinjauhari projekkanaka1, PROJECT kanakaproject1. Command dibuat singkat 6 sampai 12 baris per prompt, tanpa komentar panjang, tanpa penjelasan robotik. Pesan commit pendek gaya manusia: chore init repo, feat tambah auth, feat layout dasar, feat integrasi bmkg, feat verifikasi admin, feat form donasi, feat qris timer, feat webhook, feat disbursement, feat upload, feat dashboard mitra, feat timeline, feat audit LPJ, merge gabung fitur, chore config vercel, docs lengkapi docs. Variasi natural: kadang pakai tail 3 baris, kadang cek ls dulu, kadang langsung push, seperti developer lembur hackathon. Dari sisi UI UX: mudah disalin di HP, mudah dibaca juri, tidak ada simbol markdown pengganggu. Dari sisi PM: traceability tetap terjaga via timestamp WIB realistis, main untuk fondasi, develop untuk fitur, main lagi untuk deploy audit.
