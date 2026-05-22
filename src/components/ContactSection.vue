<script setup lang="ts">
import { ref, onMounted, reactive } from 'vue'

const sectionRef = ref<HTMLElement | null>(null)
const submitted = ref(false)
const loading = ref(false)

const form = reactive({
  name: '',
  email: '',
  phone: '',
  subject: '',
  checkin: '',
  checkout: '',
  message: '',
})

const errors = reactive({ name: '', email: '', message: '' })

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((e) => {
        if (e.isIntersecting) {
          e.target.querySelectorAll('.reveal').forEach((el) => el.classList.add('visible'))
          observer.unobserve(e.target)
        }
      })
    },
    { threshold: 0.1 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})

const validate = (): boolean => {
  let valid = true
  errors.name = ''; errors.email = ''; errors.message = ''
  if (!form.name.trim()) { errors.name = 'El nombre es obligatorio'; valid = false }
  if (!form.email.trim() || !/^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(form.email)) { errors.email = 'Introduce un email válido'; valid = false }
  if (!form.message.trim() || form.message.length < 10) { errors.message = 'El mensaje debe tener al menos 10 caracteres'; valid = false }
  return valid
}

const handleSubmit = async () => {
  if (!validate()) return
  loading.value = true
  // Conecta aquí con Formspree, EmailJS o tu backend
  await new Promise((r) => setTimeout(r, 1200))
  loading.value = false
  submitted.value = true
}
</script>

<template>
  <section id="contacto" class="contact" ref="sectionRef">
    <div class="container contact-grid">
      <div class="contact-info">
        <span class="section-label reveal">Contacto</span>
        <h2 class="section-title reveal reveal-delay-1">¿Planeas tu visita?</h2>
        <div class="divider reveal reveal-delay-1"></div>
        <p class="section-subtitle reveal reveal-delay-2">
          Escríbenos para consultar disponibilidad, organizar un evento especial
          o simplemente resolver cualquier duda. Te respondemos en menos de 24 horas.
        </p>

        <div class="contact-details reveal reveal-delay-3">
          <div class="detail-item">
            <span class="detail-icon">📞</span>
            <a href="tel:+34000000000">+34 000 000 000</a>
          </div>
          <div class="detail-item">
            <span class="detail-icon">✉️</span>
            <a href="mailto:info@cansegura.com">info@cansegura.com</a>
          </div>
          <div class="detail-item">
            <span class="detail-icon">📍</span>
            <span>Carretera de Can Segura, s/n · Cataluña</span>
          </div>
        </div>

        <div class="social-links reveal reveal-delay-4">
          <a href="#" class="social-link" aria-label="Instagram">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <rect x="2" y="2" width="20" height="20" rx="5"/>
              <circle cx="12" cy="12" r="4"/>
              <circle cx="17.5" cy="6.5" r="1" fill="currentColor" stroke="none"/>
            </svg>
            @cansegurahotel
          </a>
          <a href="#" class="social-link" aria-label="Facebook">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5">
              <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"/>
            </svg>
            Can Segura Hotel
          </a>
        </div>
      </div>

      <div class="contact-form-wrap reveal reveal-delay-2">
        <Transition name="fade" mode="out-in">
          <div v-if="submitted" class="success-state">
            <div class="success-icon">✓</div>
            <h3>¡Mensaje recibido!</h3>
            <p>Gracias por contactarnos. Te responderemos lo antes posible.</p>
          </div>

          <form v-else class="contact-form" @submit.prevent="handleSubmit">
            <div class="form-row">
              <div class="form-group" :class="{ error: errors.name }">
                <label for="name">Nombre *</label>
                <input id="name" v-model="form.name" type="text" placeholder="Tu nombre" autocomplete="name" />
                <span v-if="errors.name" class="error-msg">{{ errors.name }}</span>
              </div>
              <div class="form-group" :class="{ error: errors.email }">
                <label for="email">Email *</label>
                <input id="email" v-model="form.email" type="email" placeholder="tu@email.com" autocomplete="email" />
                <span v-if="errors.email" class="error-msg">{{ errors.email }}</span>
              </div>
            </div>

            <div class="form-row">
              <div class="form-group">
                <label for="phone">Teléfono</label>
                <input id="phone" v-model="form.phone" type="tel" placeholder="+34 000 000 000" />
              </div>
              <div class="form-group">
                <label for="subject">Motivo de consulta</label>
                <select id="subject" v-model="form.subject">
                  <option value="" disabled>Selecciona una opción</option>
                  <option value="alojamiento">Reserva de alojamiento</option>
                  <option value="restaurante">Restaurante</option>
                  <option value="evento">Evento / celebración</option>
                  <option value="grupo">Grupo</option>
                  <option value="otro">Otro</option>
                </select>
              </div>
            </div>

            <div class="form-row">
              <div class="form-group">
                <label for="checkin">Fecha de llegada</label>
                <input id="checkin" v-model="form.checkin" type="date" />
              </div>
              <div class="form-group">
                <label for="checkout">Fecha de salida</label>
                <input id="checkout" v-model="form.checkout" type="date" />
              </div>
            </div>

            <div class="form-group" :class="{ error: errors.message }">
              <label for="message">Mensaje *</label>
              <textarea id="message" v-model="form.message" rows="4" placeholder="Cuéntanos qué necesitas..."></textarea>
              <span v-if="errors.message" class="error-msg">{{ errors.message }}</span>
            </div>

            <button type="submit" class="submit-btn" :disabled="loading">
              <span v-if="loading" class="spinner"></span>
              <span v-else>Enviar consulta</span>
            </button>
          </form>
        </Transition>
      </div>
    </div>
  </section>
</template>

<style scoped>
.contact {
  padding: 8rem 0;
  background: var(--bg-primary);
  position: relative;
}
.contact::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 1px;
  background: linear-gradient(to right, transparent, var(--border-accent), transparent);
}

.contact-grid {
  display: grid;
  grid-template-columns: 1fr 1.4fr;
  gap: 6rem;
  align-items: start;
}

.contact-details {
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  gap: 0.85rem;
}
.detail-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  font-size: 0.9rem;
  color: var(--text-muted);
}
.detail-icon { font-size: 1.1rem; }
.detail-item a { color: var(--accent); transition: color var(--transition); }
.detail-item a:hover { color: var(--accent-dark); }

.social-links {
  margin-top: 2rem;
  display: flex;
  flex-direction: column;
  gap: 0.85rem;
  padding-top: 1.5rem;
  border-top: 1px solid var(--border);
}
.social-link {
  display: flex;
  align-items: center;
  gap: 0.7rem;
  font-size: 0.875rem;
  color: var(--text-muted);
  transition: color var(--transition);
}
.social-link:hover { color: var(--accent); }

.contact-form-wrap {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  padding: 2.5rem;
  box-shadow: var(--shadow-card);
}

.contact-form { display: flex; flex-direction: column; gap: 1.1rem; }

.form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 1.1rem; }

.form-group { display: flex; flex-direction: column; gap: 0.45rem; }

label {
  font-size: 0.75rem;
  font-weight: 600;
  letter-spacing: 0.06em;
  text-transform: uppercase;
  color: var(--text-muted);
}

input, select, textarea {
  background: var(--bg-primary);
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  padding: 0.75rem 1rem;
  font-family: var(--font-sans);
  font-size: 0.9rem;
  color: var(--text-primary);
  transition: border-color var(--transition);
  outline: none;
  width: 100%;
}
input::placeholder, textarea::placeholder { color: var(--text-faint); }
input:focus, select:focus, textarea:focus { border-color: var(--accent); }
select { appearance: none; cursor: pointer; }
textarea { resize: vertical; min-height: 100px; }

.form-group.error input,
.form-group.error textarea { border-color: #c0523a; }
.error-msg { font-size: 0.75rem; color: #c0523a; }

.submit-btn {
  font-size: 0.85rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #fff;
  background: var(--accent);
  padding: 1rem 2rem;
  border-radius: var(--radius-sm);
  margin-top: 0.5rem;
  transition: background var(--transition), transform 0.2s;
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 52px;
}
.submit-btn:hover:not(:disabled) { background: var(--accent-dark); transform: translateY(-2px); }
.submit-btn:disabled { opacity: 0.65; cursor: not-allowed; }

.spinner {
  width: 18px; height: 18px;
  border: 2px solid rgba(255,255,255,0.3);
  border-top-color: #fff;
  border-radius: 50%;
  animation: spin 0.7s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }

.success-state {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  padding: 3rem 1rem;
  gap: 1rem;
}
.success-icon {
  width: 64px; height: 64px;
  border-radius: 50%;
  background: var(--accent);
  color: #fff;
  font-size: 1.8rem;
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: 700;
}
.success-state h3 { font-family: var(--font-serif); font-size: 1.5rem; color: var(--text-primary); }
.success-state p { color: var(--text-muted); font-size: 0.95rem; }

.fade-enter-active, .fade-leave-active { transition: opacity 0.35s ease; }
.fade-enter-from, .fade-leave-to { opacity: 0; }

@media (max-width: 900px) {
  .contact-grid { grid-template-columns: 1fr; gap: 3rem; }
  .form-row { grid-template-columns: 1fr; }
}
</style>
