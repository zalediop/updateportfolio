<template>
  <section id="contact">
    <div class="container">
      <h2 class="section-title reveal">Contactez-<span>moi</span></h2>

      <div class="contact-grid">
        <!-- Left: Info -->
        <div class="contact-info">
          <h3 class="reveal">Parlons de votre projet</h3>
          <p class="reveal reveal-delay-1">
            Vous avez un projet en tête ou souhaitez discuter d'une opportunité ?
            N'hésitez pas à me contacter. Je suis ouvert aux stages, alternances et collaborations.
          </p>

          <a href="mailto:zalediop577@gmail.com" class="contact-item reveal reveal-delay-1" id="contact-email">
            <div class="contact-item-icon"><i class="fas fa-envelope"></i></div>
            <div class="contact-item-text">
              <h4>Email</h4>
              <p>zalediop577@gmail.com</p>
            </div>
          </a>

          <a href="https://wa.me/221773964246" target="_blank" rel="noopener" class="contact-item reveal reveal-delay-2" id="contact-phone">
            <div class="contact-item-icon">
              <i class="fab fa-whatsapp"></i>
            </div>
            <div class="contact-item-text">
              <h4>WhatsApp</h4>
              <p>+221 77 396 42 46</p>
            </div>
          </a>

          <div class="contact-item reveal reveal-delay-3" id="contact-location">
            <div class="contact-item-icon"><i class="fas fa-map-marker-alt"></i></div>
            <div class="contact-item-text">
              <h4>Localisation</h4>
              <p>Dakar, Liberté 6 — Sénégal</p>
            </div>
          </div>

          <div class="social-links reveal reveal-delay-4">
            <h4>Retrouvez-moi sur</h4>
            <div class="social-icons">
              <a href="https://github.com/zalediop" class="social-icon" target="_blank" rel="noopener noreferrer" aria-label="GitHub" id="social-github">
                <i class="fab fa-github"></i>
              </a>
              <a href="https://wa.me/221773964246" class="social-icon whatsapp-icon" target="_blank" rel="noopener noreferrer" aria-label="WhatsApp" id="social-whatsapp">
                <i class="fab fa-whatsapp"></i>
              </a>
              <a href="https://www.linkedin.com/in/saliou-diop-595799397/" class="social-icon" target="_blank" rel="noopener noreferrer" aria-label="LinkedIn" id="social-linkedin">
                <i class="fab fa-linkedin-in"></i>
              </a>
              <a href="https://www.instagram.com/_shaalihu_/" class="social-icon" target="_blank" rel="noopener noreferrer" aria-label="Instagram" id="social-instagram">
                <i class="fab fa-instagram"></i>
              </a>
              <a href="mailto:zalediop577@gmail.com" class="social-icon" aria-label="Email" id="social-email">
                <i class="fas fa-envelope"></i>
              </a>
            </div>
          </div>
        </div>

        <!-- Right: Form -->
        <div class="contact-form-card reveal reveal-delay-2">
          <div class="whatsapp-form-header">
            <i class="fab fa-whatsapp" style="color: #25d366; font-size: 1.4rem;"></i>
            <span>Votre message sera envoyé via <strong>WhatsApp</strong></span>
          </div>

          <form id="contact-form" novalidate @submit.prevent="handleSubmit">
            <div class="form-row">
              <div class="form-group">
                <label for="prenom">Prénom</label>
                <input type="text" id="prenom" name="prenom" placeholder="Votre prénom" autocomplete="given-name" v-model="form.prenom" required />
              </div>
              <div class="form-group">
                <label for="nom">Nom</label>
                <input type="text" id="nom" name="nom" placeholder="Votre nom" autocomplete="family-name" v-model="form.nom" required />
              </div>
            </div>

            <div class="form-group">
              <label for="message">Message</label>
              <textarea
                id="message"
                name="message"
                placeholder="Parlez-moi de votre projet..."
                v-model="form.message"
                required
                style="min-height: 180px;"
              ></textarea>
            </div>

            <button type="submit" class="btn-submit" id="submit-btn">
              <i class="fab fa-whatsapp"></i>
              Envoyer via WhatsApp
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const WHATSAPP_NUMBER = '221773964246'
const form = ref({ prenom: '', nom: '', message: '' })

function handleSubmit() {
  if (!form.value.prenom || !form.value.nom || !form.value.message.trim()) {
    alert('Veuillez remplir tous les champs.')
    return
  }

  const fullName = `${form.value.prenom} ${form.value.nom}`
  const text = `👋 Bonjour Saliou !\n\n📛 *De :* ${fullName}\n\n💬 *Message :*\n${form.value.message}`
  const url = `https://wa.me/${WHATSAPP_NUMBER}?text=${encodeURIComponent(text)}`
  window.open(url, '_blank', 'noopener,noreferrer')

  form.value = { prenom: '', nom: '', message: '' }
}

onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible') })
  }, { threshold: 0.1 })
  document.querySelectorAll('#contact .reveal').forEach(el => observer.observe(el))
})
</script>

<style scoped>
.whatsapp-form-header {
  display: flex;
  align-items: center;
  gap: 10px;
  padding: 12px 16px;
  background: rgba(37, 211, 102, 0.08);
  border: 1px solid rgba(37, 211, 102, 0.25);
  border-radius: var(--radius-sm);
  margin-bottom: 24px;
  font-size: 0.9rem;
  color: var(--text-secondary);
}

/* WhatsApp social icon stays green */
.whatsapp-icon {
  background: linear-gradient(135deg, #25d366, #128c7e) !important;
  color: white !important;
  border-color: transparent !important;
}
</style>
