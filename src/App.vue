<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const navigation = [
  { label: 'Quem sou eu?', id: 'perfil' },
  { label: 'Formação', id: 'formacao' },
  { label: 'O que faço?', id: 'experiencia' },
  { label: 'Competências', id: 'competencias' },
  { label: 'Hobbies', id: 'interesses' },
  { label: 'Contacto', id: 'contacto' },
]

const pageIds = new Set(navigation.map((item) => item.id))
const activePage = ref('perfil')

function syncPageWithUrl() {
  const pageFromUrl = window.location.hash.slice(1)
  activePage.value = pageIds.has(pageFromUrl) ? pageFromUrl : 'perfil'
  window.scrollTo(0, 0)
}

function navigateTo(pageId) {
  if (!pageIds.has(pageId)) throw new Error(`Unknown CV section: ${pageId}`)
  if (pageId === activePage.value && window.location.hash === `#${pageId}`) return

  window.history.pushState(null, '', `#${pageId}`)
  activePage.value = pageId
  window.scrollTo(0, 0)
}

onMounted(() => {
  syncPageWithUrl()
  window.addEventListener('popstate', syncPageWithUrl)
  window.addEventListener('hashchange', syncPageWithUrl)
})

onUnmounted(() => {
  window.removeEventListener('popstate', syncPageWithUrl)
  window.removeEventListener('hashchange', syncPageWithUrl)
})

const socialLinks = [
  { name: 'LinkedIn', href: 'https://www.linkedin.com/in/s%C3%A9rgio-rosa-5bb920b7/', icon: 'linkedin' },
  { name: 'Facebook', href: 'https://www.facebook.com/sergio.pa.rosa', icon: 'facebook' },
]

const skills = [
  { name: 'Administração de sistemas', level: 'Linux e Windows' },
  { name: 'Desenvolvimento Web', level: 'HTML, CSS, JavaScript e .NET' },
  { name: 'Bases de dados', level: 'PostgreSQL e SQL' },
  { name: 'Segurança informática', level: 'Infraestruturas e boas práticas' },
]
</script>

<template>
  <div class="page-shell">
    <a class="skip-link" href="#inicio">Saltar para o conteúdo principal</a>
    <header class="site-header">
      <a class="wordmark" href="#perfil" aria-label="Currículo — início" @click.prevent="navigateTo('perfil')">Curiculum Vitae<span>.</span></a>
      <nav class="main-nav" aria-label="Navegação principal">
        <a
          v-for="item in navigation"
          :key="item.id"
          :href="`#${item.id}`"
          :aria-current="activePage === item.id ? 'page' : undefined"
          @click.prevent="navigateTo(item.id)"
        >
          {{ item.label }}
        </a>
      </nav>
    </header>

    <main id="inicio">
      <section v-if="activePage === 'perfil'" id="perfil" class="hero section-wrap" aria-labelledby="profile-title">
        <div class="hero-copy">
          <p class="eyebrow"><span class="availability-dot"></span> CURRÍCULO VITAE · 2026</p>
          <h1 id="profile-title">Olá, sou<br /><span class="name-highlight">Sérgio Rosa.</span></h1>
          <p class="hero-role">Engenheiro Informático · Estudante de Mestrado em Engenharia Informática e Tecnologia Web</p>
          <h2 class="sr-only">Quem sou eu?</h2>
          <p class="hero-intro">
            Trabalho na área das tecnologias e sistemas de informação, com interesse no desenvolvimento Web,
            na administração de infraestruturas e na segurança informática. Este currículo apresenta
            o meu percurso académico, a atividade profissional e os meus interesses.
          </p>
          <div class="hero-actions">
            <a class="button button-primary" href="#experiencia" @click.prevent="navigateTo('experiencia')">Conhecer o meu percurso <span aria-hidden="true">↓</span></a>
            <a class="text-link" href="mailto:sergio.pa.rosa@gmail.com">Enviar email <span aria-hidden="true">↗</span></a>
          </div>
          <div class="hero-meta">
            <span><span class="meta-icon" aria-hidden="true">⌖</span> Ponta Delgada, Portugal</span>
            <span><span class="meta-icon" aria-hidden="true">✉</span> sergio.pa.rosa@gmail.com</span>
          </div>
        </div>

        <aside class="profile-card" aria-label="Resumo do perfil">
          <div class="card-topline"><span>PERFIL</span><span>01 / 05</span></div>
          <div class="avatar" aria-hidden="true"><span>Sergio</span><br><span>Rosa</span></div>
          <p class="card-caption">EM CONSTANTE EVOLUÇÃO</p>
          <h2>Sérgio Rosa</h2>
          <p class="card-role">Engenharia Informática · Tecnologia Web</p>
          <div class="card-divider"></div>
          <p class="card-note">“Aprender, experimentar e crescer — um projeto de cada vez.”</p>
          <a class="card-link" href="#contacto" @click.prevent="navigateTo('contacto')">Vamos conversar <span aria-hidden="true">↗</span></a>
          <span class="card-decoration" aria-hidden="true">✳</span>
        </aside>
      </section>

      <section v-else-if="activePage === 'formacao'" id="formacao" class="content-section section-wrap">
        <div class="section-heading">
          <p class="eyebrow">01 — PERCURSO</p>
          <h2>Formação <span>académica</span></h2>
          <p>As etapas que têm contribuído para o meu crescimento.</p>
        </div>
        <article class="timeline-card">
          <div class="timeline-date">2022-2025</div>
          <div class="timeline-content">
            <h3>Engenharia de Informática</h3>
            <p class="timeline-place">Universidade Aberta - 2022-2025</p>
            <p>Formação em Engenharia Informática. Confirmar datas, instituição e qualificações antes da entrega.</p>
          </div>
          <span class="timeline-marker" aria-hidden="true"></span>
        </article>
        <p class="add-entry"><span aria-hidden="true">＋</span> Podes adicionar aqui outras formações e certificações.</p>
      </section>

      <section v-else-if="activePage === 'experiencia'" id="experiencia" class="content-section experience-section">
        <div class="section-wrap">
          <div class="section-heading">
            <p class="eyebrow">02 — EXPERIÊNCIA</p>
            <h2>O que faço? <span>Experiência e projetos</span></h2>
            <p>Experiência profissional, voluntariado e projetos pessoais.</p>
          </div>
          <article class="timeline-card">
            <div class="timeline-date">Percurso profissional</div>
            <div class="timeline-content">
              <h3>Tecnologias e Sistemas de Informação</h3>
              <p class="timeline-place">Administração Pública Regional · Açores</p>
              <p>Atividade na área dos sistemas e tecnologias de informação, incluindo administração de sistemas, infraestrutura tecnológica e desenvolvimento de soluções Web.</p>
            </div>
            <span class="timeline-marker" aria-hidden="true"></span>
          </article>
        </div>
      </section>

      <section v-else-if="activePage === 'competencias'" id="competencias" class="content-section section-wrap skills-section">
        <div class="section-heading">
          <p class="eyebrow">03 — PONTOS FORTES</p>
          <h2>Competências <span>&amp; ferramentas</span></h2>
          <p>Conhecimentos e capacidades que levo para cada desafio.</p>
        </div>
        <div class="skills-grid">
          <article v-for="(skill, index) in skills" :key="skill.name" class="skill-card">
            <span class="skill-number">0{{ index + 1 }}</span>
            <h3>{{ skill.name }}</h3>
            <p>{{ skill.level }}</p>
          </article>
        </div>
        <p class="skills-hint">As competências e respetivos níveis devem ser confirmados antes da submissão.</p>
      </section>

      <section v-else-if="activePage === 'interesses'" id="interesses" class="interests-section">
        <div class="section-wrap interests-inner">
          <div>
            <p class="eyebrow">04 — FORA DO CURRÍCULO</p>
            <h2>Hobbies <span>&amp; interesses</span></h2>
          </div>
          <p>Ralis e desporto motorizado.</p>
        </div>
      </section>

      <section v-else-if="activePage === 'contacto'" id="contacto" class="contact-section section-wrap">
        <p class="eyebrow">05 — VAMOS FALAR?</p>
        <h2>Uma boa conversa<br />pode ser o <span>início.</span></h2>
        <a class="button button-primary" href="mailto:sergio.pa.rosa@gmail.com">
          sergio.pa.rosa@gmail.com <span aria-hidden="true">↗</span>
        </a>
      </section>
    </main>

    <footer class="site-footer">
      <div class="footer-inner">
        <a class="wordmark footer-wordmark" href="#perfil" aria-label="Voltar ao início" @click.prevent="navigateTo('perfil')">Curriculum Vitae<span>.</span></a>
        <p>Sérgio Rosa · 2026</p>
        <nav class="social-links" aria-label="Redes sociais">
          <a
            v-for="social in socialLinks"
            :key="social.name"
            :href="social.href"
            :aria-label="social.name + ' (abre num novo separador)'"
            target="_blank"
            rel="noopener noreferrer"
          >
            <svg v-if="social.icon === 'linkedin'" viewBox="0 0 24 24" aria-hidden="true">
              <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.35V9h3.414v1.561h.049c.476-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 1 1 0-4.124 2.062 2.062 0 0 1 0 4.124zM7.119 20.452H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z" />
            </svg>
            <svg v-else viewBox="0 0 24 24" aria-hidden="true">
              <path d="M15.117 8.25H12.75v-1.5c0-.621.504-1.125 1.125-1.125H15V3h-2.25a3 3 0 0 0-3 3v2.25H7.5v2.625h2.25V21h3v-10.125H15l.117-2.625z" />
            </svg>
          </a>
        </nav>
      </div>
      <a class="back-to-top" href="#perfil" @click.prevent="navigateTo('perfil')">Voltar ao início ↑</a>
    </footer>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=DM+Sans:wght@400;500;600;700&family=Manrope:wght@400;500;600;700;800&display=swap');

:root {
  font-family: 'DM Sans', sans-serif;
  color: #24231f;
  background: #f7f6f2;
  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-optical-sizing: auto;
  font-weight: 400;
  scroll-behavior: smooth;
  scroll-padding-top: 88px;
  --ink: #24231f;
  --muted: #77766f;
  --green: #2f604d;
  --lime: #d6ed91;
  --paper: #f7f6f2;
}

* { box-sizing: border-box; }
body { min-width: 320px; margin: 0; }
a { color: inherit; text-decoration: none; }
a:focus-visible { outline: 2px solid #67965c; outline-offset: 4px; }
.page-shell { overflow: hidden; }
.section-wrap, .site-header, .footer-inner, .back-to-top { width: min(1120px, calc(100% - 64px)); margin-inline: auto; }
.site-header { height: 82px; display: flex; align-items: center; justify-content: space-between; border-bottom: 1px solid #e8e6df; }
.wordmark { font: 800 25px 'Manrope', sans-serif; letter-spacing: -2px; }
.wordmark span { color: #789b53; }
.main-nav { display: flex; align-items: center; gap: 30px; color: #5e5d57; font-size: 13px; }
.main-nav a, .text-link, .card-link, .back-to-top { transition: color .2s ease; }
.main-nav a:hover, .text-link:hover, .card-link:hover, .back-to-top:hover { color: #789b53; }
.main-nav a[aria-current='page'] { color: var(--green); font-weight: 700; }
.main-nav .nav-contact { padding: 11px 16px; border: 1px solid #dcdad2; border-radius: 4px; color: var(--ink); }
.main-nav .nav-contact span { margin-left: 8px; }
.hero { min-height: 570px; padding-block: 74px 78px; display: grid; grid-template-columns: 1.15fr .85fr; align-items: center; gap: 70px; }
.eyebrow { margin: 0 0 22px; color: #6a7962; font-size: 10px; font-weight: 700; letter-spacing: 1.7px; }
.availability-dot { width: 7px; height: 7px; display: inline-block; margin-right: 7px; border-radius: 50%; background: #86a96a; vertical-align: 1px; }
h1, h2, h3, p { margin-top: 0; }
h1, .section-heading h2, .interests-inner h2, .contact-section h2 { font-family: 'Manrope', sans-serif; }
h1 { margin-bottom: 12px; font-size: clamp(48px, 6vw, 75px); line-height: 1.03; letter-spacing: -5px; }
.name-highlight, .section-heading h2 span, .interests-inner h2 span, .contact-section h2 span { color: var(--green); }
.hero-role { margin-bottom: 19px; color: #5f5e58; font-size: 17px; }
.hero-intro { max-width: 490px; margin-bottom: 27px; color: var(--muted); font-size: 14px; line-height: 1.85; }
.hero-actions { display: flex; align-items: center; gap: 24px; }
.button { display: inline-flex; min-height: 46px; align-items: center; justify-content: center; gap: 18px; padding: 0 18px; border-radius: 4px; font-size: 12px; font-weight: 600; transition: background .2s ease, transform .2s ease; }
.button:hover { transform: translateY(-2px); }
.button-primary { background: var(--green); color: white; }
.button-primary:hover { background: #244b3b; }
.text-link { font-size: 12px; font-weight: 600; }
.text-link span { margin-left: 4px; }
.hero-meta { display: flex; gap: 23px; margin-top: 39px; color: #77766f; font-size: 11px; }
.meta-icon { margin-right: 5px; color: var(--green); font-size: 15px; }
.profile-card { position: relative; min-height: 378px; padding: 23px 27px 25px; overflow: hidden; border: 1px solid #e6e4dc; border-radius: 7px; background: #eeeee7; }
.card-topline { display: flex; justify-content: space-between; color: #77766f; font-size: 9px; font-weight: 700; letter-spacing: 1.2px; }
.avatar { width: 112px; height: 112px; display: grid; place-content: center; margin: 24px auto 18px; transform: rotate(-7deg); border-radius: 50%; background: var(--lime); color: var(--green); font: 800 42px 'Manrope', sans-serif; letter-spacing: -7px; }
.avatar span:first-child { position: relative; left: -7px; }
.avatar span:last-child { position: relative; top: -38px; left: 16px; font-size: 26px; }
.card-caption { margin-bottom: 7px; color: #788369; text-align: center; font-size: 8px; font-weight: 700; letter-spacing: 1.4px; }
.profile-card h2 { margin-bottom: 3px; text-align: center; font: 700 19px 'Manrope', sans-serif; }
.card-role { margin-bottom: 17px; color: var(--muted); text-align: center; font-size: 11px; }
.card-divider { height: 1px; background: #deddd5; }
.card-note { position: relative; z-index: 1; margin: 15px 0 17px; color: #5f5e58; font-size: 11px; font-style: italic; line-height: 1.6; }
.card-link { position: relative; z-index: 1; font-size: 10px; font-weight: 700; }
.card-link span { margin-left: 6px; color: var(--green); }
.card-decoration { position: absolute; right: 12px; bottom: -34px; color: #e5e5d9; font-size: 130px; }
.content-section { padding-block: 83px; }
.section-heading { margin-bottom: 33px; }
.section-heading .eyebrow, .interests-inner .eyebrow, .contact-section .eyebrow { margin-bottom: 14px; }
.section-heading h2, .interests-inner h2 { margin-bottom: 10px; font-size: clamp(30px, 4vw, 43px); letter-spacing: -2px; }
.section-heading > p:last-child { margin-bottom: 0; color: var(--muted); font-size: 13px; }
.timeline-card { position: relative; display: grid; grid-template-columns: 180px 1fr; gap: 25px; padding: 27px 28px; border: 1px solid #e8e6df; border-radius: 5px; background: #fbfaf7; }
.timeline-date { color: #77876c; font-size: 10px; font-weight: 700; letter-spacing: .8px; }
.timeline-content h3 { margin-bottom: 6px; font: 700 17px 'Manrope', sans-serif; }
.timeline-content p { margin-bottom: 0; color: var(--muted); font-size: 12px; line-height: 1.7; }
.timeline-content .timeline-place { margin-bottom: 12px; color: #77766f; font-size: 11px; }
.timeline-marker { position: absolute; top: 31px; left: -5px; width: 9px; height: 9px; border: 2px solid var(--paper); border-radius: 50%; background: #88a66a; }
.add-entry { display: inline-flex; gap: 8px; margin-top: 18px; color: #68675f; font-size: 11px; }
.add-entry span { color: var(--green); }
.experience-section { background: #eeeee7; }
.experience-section .timeline-card { border-color: #e1e0d8; background: #f7f6f2; }
.skills-section { padding-bottom: 87px; }
.skills-grid { display: grid; grid-template-columns: repeat(4, 1fr); gap: 13px; }
.skill-card { min-height: 143px; padding: 18px; border: 1px solid #e8e6df; border-radius: 5px; background: #fbfaf7; }
.skill-number { color: #82916f; font-size: 9px; font-weight: 700; }
.skill-card h3 { margin: 24px 0 7px; font: 700 13px 'Manrope', sans-serif; }
.skill-card p { margin-bottom: 0; color: var(--muted); font-size: 10px; }
.skills-hint { margin: 17px 0 0; color: #8a8982; font-size: 10px; }
.interests-section { padding-block: 54px; background: #e8ebdf; }
.interests-inner { display: flex; align-items: center; justify-content: space-between; gap: 24px; }
.interests-inner h2 { margin-bottom: 0; font-size: clamp(27px, 3.5vw, 38px); }
.interests-inner > p { max-width: 330px; margin: 15px 0 0; color: #62685d; font-size: 12px; line-height: 1.8; }
.contact-section { padding-block: 92px 100px; text-align: center; }
.contact-section h2 { margin-bottom: 25px; font-size: clamp(38px, 5vw, 56px); line-height: 1.15; letter-spacing: -3px; }
.site-footer { padding-block: 22px 18px; border-top: 1px solid #e8e6df; }
.footer-inner { min-height: 40px; display: flex; align-items: center; justify-content: space-between; }
.footer-wordmark { font-size: 21px; }
.footer-inner > p { margin: 0; color: #8a8982; font-size: 10px; }
.social-links { display: flex; gap: 8px; }
.social-links a { width: 29px; height: 29px; display: grid; place-items: center; border: 1px solid #deddd5; border-radius: 50%; color: #65655e; transition: all .2s ease; }
.social-links svg { width: 14px; height: 14px; fill: currentColor; }
.social-links a:hover { border-color: var(--green); background: var(--green); color: white; }
.back-to-top { display: block; margin-top: 12px; color: #77766f; text-align: right; font-size: 9px; }

@media (max-width: 760px) {
  .section-wrap, .site-header, .footer-inner, .back-to-top { width: min(100% - 40px, 560px); }
  .site-header { height: auto; min-height: 72px; align-items: flex-start; padding-block: 18px 13px; }
  .main-nav { max-width: calc(100% - 55px); flex-wrap: wrap; justify-content: flex-end; gap: 10px 16px; font-size: 11px; }
  .main-nav .nav-contact { padding: 7px 10px; }
  .hero { min-height: 0; grid-template-columns: 1fr; gap: 42px; padding-block: 60px; }
  .hero-copy { max-width: 560px; }
  .profile-card { width: min(100%, 390px); justify-self: center; }
  .content-section { padding-block: 65px; }
  .skills-grid { grid-template-columns: repeat(2, 1fr); }
  .interests-inner { align-items: flex-start; flex-direction: column; gap: 4px; }
}

@media (max-width: 480px) {
  .section-wrap, .site-header, .footer-inner, .back-to-top { width: calc(100% - 36px); }
  .main-nav { gap: 9px 12px; }
  h1 { font-size: 55px; letter-spacing: -4px; }
  .hero-actions { align-items: flex-start; flex-direction: column; gap: 16px; }
  .hero-meta { align-items: flex-start; flex-direction: column; gap: 8px; margin-top: 27px; }
  .timeline-card { grid-template-columns: 1fr; gap: 12px; padding: 22px; }
  .timeline-marker { top: 24px; }
  .footer-inner { flex-wrap: wrap; gap: 12px; }
  .footer-inner > p { order: 3; width: 100%; }
}

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { scroll-behavior: auto !important; transition-duration: .01ms !important; }
}
</style>

<style scoped>
.sr-only { position:absolute; width:1px; height:1px; padding:0; margin:-1px; overflow:hidden; clip:rect(0,0,0,0); white-space:nowrap; border:0; }
.skip-link { position:absolute; left:12px; top:-100px; z-index:1000; background:#fff; color:#1b4c3c; padding:12px; }
.skip-link:focus { top:12px; }
</style>
