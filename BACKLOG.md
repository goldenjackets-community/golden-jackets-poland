# 🏆 Golden Jackets Brazil — Backlog

## ✅ Concluído

### Infraestrutura
- [x] Site estático S3 + CloudFront + WAF
- [x] Cognito User Pool (autenticação Lounge)
- [x] API Gateway HTTP API (apply, article, sponsor, admin)
- [x] Lambdas: gj-apply, gj-article, gj-sponsor, gj-admin
- [x] SES para emails transacionais
- [x] SNS para notificações admin
- [x] AWS Backup (diário/semanal/mensal)
- [x] GitHub Actions CI/CD (deploy + user onboarding)
- [x] Smoke tests no pipeline
- [x] CloudWatch alarmes nas Lambdas
- [x] Cognito JWT Authorizer no /admin
- [x] GitHub Secrets (sem IDs hardcoded)
- [x] SECURITY.md + README atualizado
- [x] Rate limiting no API Gateway (10 req/s, burst 20) — 10/05/2026
- [x] Validação de input nas Lambdas (sanitizar nome, email, URL) — 10/05/2026
- [x] Auto-refresh token no admin (30 dias sem relogin) — 10/05/2026
- [x] Partner click tracking (DynamoDB + API + admin panel) — 09/05/2026
- [x] LGPD: Política de Privacidade + consent checkbox + banner Lounge — 09/05/2026
- [x] Privacy consent registrado no DynamoDB (auditável) — 09/05/2026
- [x] Auto-numbering de cards no deploy (GitHub Actions) — 08/05/2026
- [x] Config.js centralizado (admin email/API URL) — 08/05/2026

### Site
- [x] Seção Golden Jackets com cards numerados
- [x] Seção Challengers (cards prata)
- [x] Seção Alumni (cards âmbar)
- [x] Seção Articles & Talks com tags (Article/Talk)
- [x] Seção Podcast & Videos (YouTube/Spotify links) — 10/05/2026
- [x] Seção Sponsors com formulário
- [x] Seção Events com countdown
- [x] Mapa interativo com pins dourados/prata
- [x] Filtro por estado (Golden + Challengers)
- [x] Medalhas automáticas (🥇🥈🥉) para top contributors
- [x] Contadores dinâmicos (JS conta cards)
- [x] Tagline do Geries no hero
- [x] Missão destacada no About
- [x] Tags coloridas (Awstronaut, Speaker, Ambassador)
- [x] Badges de certificação em pirâmide
- [x] SEO: sitemap.xml, robots.txt, canonical URL, Google Search Console — 10/05/2026
- [x] Parceiros: Tutorials Dojo + Sundog Education (logos, links, seção) — 09/05/2026
- [x] Partner click tracking com contadores no admin — 09/05/2026
- [x] Política de Privacidade (privacy.html) — 09/05/2026
- [x] Critério Challenger atualizado para 10+ certs — 09/05/2026

### Lounge
- [x] Autenticação Cognito
- [x] Change Password (1st Login)
- [x] Forgot Password
- [x] Enter key no login
- [x] Submit Article (com validação obrigatória) — 09/05/2026
- [x] Discord link
- [x] Admin Console (página separada)
- [x] Banner LGPD (aceite de política no primeiro login) — 09/05/2026

### Admin Console
- [x] List Users (via API)
- [x] Create User (formulário)
- [x] Delete User
- [x] Resend Pending
- [x] Backup Status (com fallback pra campos undefined) — 09/05/2026
- [x] Restore (dupla confirmação) — 09/05/2026
- [x] Partner Clicks (filtro por partner + filtro por mês) — 09/05/2026
- [x] Links GitHub (PRs, Actions)
- [x] Card Generator
- [x] Protegido por JWT + auto-refresh token — 10/05/2026

### Lambdas
- [x] gj-apply: markers estáveis (END_GOLDEN_JACKETS, END_ALUMNI, END_CHALLENGERS) — 10/05/2026
- [x] gj-apply: Challengers inserem no final (não no começo) — 09/05/2026
- [x] gj-apply: tags corretas pra Challengers (11/12 + "1 away") — 09/05/2026
- [x] gj-article: marker estável (END_ARTICLES) — 10/05/2026
- [x] gj-article: validação de input (título, URL, resumo obrigatórios) — 10/05/2026
- [x] Contadores removidos das Lambdas (JS dinâmico cuida) — 10/05/2026

---

## 🔴 Alta Prioridade

### Segurança
- [ ] SES sair do sandbox (solicitado, NEGADO — aguardando cooldown pra resubmeter)

---

## 🟡 Média Prioridade

### Refatoração (fazer com cuidado, branch separada)
- [ ] Separar CSS em arquivo externo (styles.css)
- [ ] Separar JS em arquivo externo (app.js)
- [ ] CSS inline → classes reutilizáveis
- [ ] Minificação HTML/CSS/JS no pipeline

### Funcionalidades
- [x] Email de boas-vindas automático (Cognito envia senha temporária)
- [x] Promover Challenger → Golden Jacket (botão no admin) — 10/05/2026
- [x] Dashboard de métricas no admin (membros/mês) — 10/05/2026
- [x] Exportar lista de membros (CSV) no admin — 10/05/2026
- [x] Notificação no Discord quando novo membro entra

### Comunidade
- [ ] Buscar patrocinadores (media kit pronto)
- [ ] Newsletter mensal para membros
- [ ] Página de eventos passados (galeria de fotos)

---

## 🟢 Baixa Prioridade / Futuro

### Técnico
- [ ] Migrar Lambdas para IaC (CDK ou SAM)
- [ ] Testes unitários nas Lambdas
- [ ] EventBridge: lembrete automático para pendentes (a cada 24h)
- [ ] Cognito custom domain (auth.goldenjacketsbrazil.com)
- [ ] SES custom domain (noreply@goldenjacketsbrazil.com)
- [x] Monitoramento de custos (Budget alarm $10/mês) — 10/05/2026

### Site
- [x] Dark/Light mode persistente (já implementado com localStorage)
- [ ] Página individual por membro (perfil completo)
- [ ] Blog integrado (posts longos)
- [ ] Internacionalização completa (PT/EN toggle)
- [ ] PWA (Progressive Web App) — acesso offline

### Comunidade
- [x] Programa de mentoria (Golden Jackets → Challengers) — iniciado 08/05/2026
- [x] Ranking de contribuições (medalhas automáticas 🥇🥈🥉 na seção Articles)
- [ ] Certificação interna da comunidade
- [ ] Meetups regionais (SP, RJ, PR)
- [ ] Parceria com AWS User Groups
- [x] Submeter para AWS Community Builder / Hero — em andamento (Taylor, João Helena, João Gabriel)

---

*Última atualização: 10/05/2026*
