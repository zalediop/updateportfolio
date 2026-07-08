<template>
  <section id="about">
    <div class="container">
      <h2 class="section-title reveal">À propos de <span>moi</span></h2>

      <div class="about-grid">
        <!-- Image -->
        <div class="about-image-wrapper reveal">
          <div class="about-image-frame">
            <img
              :src="imgSrc"
              alt="Saliou Diop - Développeur Web"
              v-if="!imgError"
              @error="imgError = true"
            />
            <div class="about-image-placeholder" v-else>
              <span class="initials">SD</span>
              <p>Saliou Diop</p>
            </div>
          </div>
          <div class="about-accent-card">
            <div class="number">9+</div>
            <div class="label">Projets réalisés</div>
          </div>
        </div>

        <!-- Text -->
        <div class="about-text">
          <h3 class="reveal">Qui suis-je ?</h3>
          <p class="reveal reveal-delay-1">
            Je m'appelle <strong>Saliou Diop</strong>, étudiant en Informatique passionné par le
            développement web et mobile.
            En formation à l'Institut Supérieur de l'Informatique de Dakar, je me spécialise dans les
            technologies modernes du web.
            Sérieux, curieux et motivé, je m'investis pleinement dans mon apprentissage pour devenir un
            développeur Full Stack polyvalent.
          </p>

          <div class="about-info-grid">
            <div class="info-card reveal reveal-delay-1" v-for="card in infoCards" :key="card.title">
              <div class="info-icon"><i :class="card.icon"></i></div>
              <div class="info-content">
                <h4>{{ card.title }}</h4>
                <p>{{ card.value }}</p>
                <span v-if="card.sub">{{ card.sub }}</span>
              </div>
            </div>
          </div>

          <a href="/SALIOU-DIOP-CV.pdf" download class="btn-download reveal">
            <i class="fas fa-file-pdf"></i>
            Télécharger mon CV
            <i class="fas fa-download" style="font-size:0.85rem;"></i>
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const imgError = ref(false)
const imgSrc = '/portfolio.jpg'

const infoCards = [
  { icon: 'fas fa-user-graduate', title: 'Formation',       value: 'Licence en Informatique', sub: 'ISI, Dakar' },
  { icon: 'fas fa-code',          title: 'Spécialisation',  value: 'Développement Full Stack', sub: 'Web & Mobile' },
  { icon: 'fas fa-globe',         title: 'Langues',         value: 'Français · Anglais',       sub: 'Wolof' },
  { icon: 'fas fa-map-marker-alt',title: 'Localisation',    value: 'Dakar, Sénégal',           sub: 'Liberté 6' },
  { icon: 'fas fa-heart',         title: 'Passions',        value: 'Tech · Jeux vidéo',        sub: 'Football' },
  { icon: 'fas fa-envelope',      title: 'Email',           value: 'zalediop577@gmail.com',    sub: null },
]

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) entry.target.classList.add('visible')
    })
  }, { threshold: 0.1 })
  document.querySelectorAll('#about .reveal').forEach(el => observer.observe(el))
})
</script>
