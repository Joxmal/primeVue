<template>
  <div class="bg-gray-900 text-white min-h-screen font-sans antialiased">
    <Toast />
    <!-- Header -->
    <Toolbar
      style="background-color: rgba(31, 41, 55, 0.8); border: none; border-radius: 0; padding: 1rem 1.5rem; backdrop-filter: blur(10px); position: sticky; top: 0; z-index: 1000;">
      <template #start>
        <div class="text-2xl font-bold tracking-wider">
          <span class="text-green-400">Porta</span>Folio
        </div>
      </template>
      <template #end>
        <div class="hidden md:flex items-center gap-2 [&> *]:transition-colors [&> *]:text-white  [&>*]:hover:text-green-400">
          <Button label="Sobre Mí" text plain @click="scrollTo('aboutMe')" />
          <Button label="Proyectos" text plain @click="scrollTo('projects')" />
          <Button label="Proceso" text plain @click="scrollTo('process')" />
          <Button label="Testimonios" text plain @click="scrollTo('testimonials')" />
          <Button label="FAQ" text plain @click="scrollTo('faq')" />
          <Button label="Contacto" icon="pi pi-envelope" severity="contrast" @click="contactModalVisible = true" />
        </div>
        <div class="md:hidden flex items-center">
          <Menu ref="menu" :model="toolbarMenu" popup />
          <Button icon="pi pi-bars" class="p-button-text text-white" @click="$refs.menu.toggle($event)" aria-label="Menú" />
        </div>
      </template>
    </Toolbar>

    <!-- Hero Section Portafolio Personal -->
      <main class="container mx-auto px-4 sm:px-6 py-10 sm:py-20 text-center relative overflow-hidden">
        <div class="absolute inset-0 pointer-events-none" style="z-index:0;">
          <div class="w-full h-full bg-gradient-to-br from-green-900 via-blue-900 to-gray-900" style="opacity:0.25;"></div>
        </div>
        <div class="relative z-10 flex flex-col items-center">
          <img src="https://primefaces.org/cdn/primevue/images/avatar/annafali.png" alt="Avatar"
            class="mx-auto mb-6 rounded-full w-24 sm:w-32 h-24 sm:h-32 border-4 border-green-400 shadow-lg" />
          <h1
            class="text-3xl sm:text-5xl md:text-7xl font-extrabold leading-tight mb-4 bg-clip-text text-transparent bg-gradient-to-r from-green-400 via-blue-400 to-blue-500">
            José Montes
          </h1>
          <h2 class="text-lg sm:text-2xl md:text-3xl font-semibold text-blue-300 mb-4">Desarrollador Frontend & UI Designer</h2>
          <p class="text-base sm:text-lg md:text-xl text-gray-200 mb-8 max-w-2xl mx-auto">
            Apasionado por crear experiencias digitales únicas y funcionales. Especializado en Vue, Nuxt y diseño moderno.
          </p>
          <div class="flex justify-center gap-4 mb-8 flex-wrap">
            <a href="https://github.com/joxmal" target="_blank" class="text-green-400 hover:text-blue-400 text-2xl"><i class="pi pi-github"></i></a>
            <a href="mailto:joxmal@email.com" class="text-blue-400 hover:text-green-400 text-2xl"><i class="pi pi-envelope"></i></a>
            <a href="https://linkedin.com/in/joxmal" target="_blank" class="text-green-400 hover:text-blue-400 text-2xl"><i class="pi pi-linkedin"></i></a>
          </div>
          <Terminal welcomeMessage="Portafolio iniciado..." prompt="joxmal@portfolio ~ $" aria-label="Portfolio Terminal"
            style="background-color: rgba(17, 24, 39, 0.8); border: 1px solid #374151;"
            class="w-full sm:w-2/3 mx-auto text-left" />
        </div>
      </main>
    <!-- Sobre mí -->
    <section class="py-16 bg-gradient-to-r from-gray-900 via-blue-950 to-green-900 text-white" ref="aboutMe">
      <div class="container mx-auto px-6 flex flex-col md:flex-row items-center gap-12">
        <div class="md:w-1/2">
          <h2 class="text-4xl font-bold mb-4 text-green-300">Sobre mí</h2>
          <p class="text-lg text-gray-200 mb-4">Soy desarrollador frontend con más de 4 años de experiencia creando
            interfaces modernas y funcionales. Me apasiona el diseño, la animación y la optimización web. Siempre busco
            aprender nuevas tecnologías y mejorar cada proyecto.</p>
          <ul class="list-disc pl-6 text-blue-300">
            <li>+4 años de experiencia en desarrollo web</li>
            <li>Especialista en Vue, Nuxt y Tailwind</li>
            <li>Enfoque en accesibilidad y rendimiento</li>
            <li>Colaborador en proyectos open source</li>
          </ul>
        </div>
        <div class="md:w-1/2 flex justify-center">
          <img src="https://primefaces.org/cdn/primevue/images/galleria/galleria10.jpg" alt="Sobre mí"
            class="rounded-xl shadow-2xl w-full max-w-md" />
        </div>
      </div>
    </section>

    <!-- Galería de Proyectos Personales -->
    <section v-animateonscroll="{ enterClass: 'animate-enter fade-in-10 slide-in-from-t-20 animate-duration-1000' }"
      ref="projects" class="py-20">
      <div class="container mx-auto px-6">
        <div class="text-center mb-12">
          <h2 class="text-4xl font-bold mb-2">Mis Proyectos</h2>
          <p class="text-gray-400">Algunos trabajos y experimentos personales.</p>
        </div>
        <Galleria auto-play :transition-interval="5000" circular :value="projectsData"
          :responsiveOptions="responsiveOptions" :numVisible="5" containerStyle="max-width: 58rem; margin: auto;" class="">
          <template #item="slotProps">
            <div class="bg-gray-900 rounded-lg shadow-lg overflow-hidden ">
              <img
                :src="slotProps.item.itemImageSrc"
                :alt="slotProps.item.alt"
                style="width: 100%; max-height: 50vh; object-fit: contain; display: block; background: #222; border-radius: 0.5rem;"
              />
              <div class="p-4">
                <h3 class="text-xl font-bold text-green-400 mb-2">{{ slotProps.item.title }}</h3>
                <p class="text-gray-300 text-sm mb-2">{{ slotProps.item.description }}</p>
                <!-- Tecnologías aplicadas -->
                <div v-if="slotProps.item.techs" class="flex flex-wrap gap-3 mb-2">
                  <div v-for="tech in slotProps.item.techs" :key="tech.name" class="flex items-center gap-1 bg-gray-800 rounded px-2 py-1">
                    <Icon :name="tech.icon" class="text-xl" />
                    <span class="text-xs text-green-300">{{ tech.name }}</span>
                  </div>
                </div>
                <a v-if="slotProps.item.link" :href="slotProps.item.link" target="_blank"
                  class="text-blue-400 underline mt-2 inline-block">Ver proyecto</a>
              </div>
            </div>
          </template>
          <template #thumbnail="slotProps">
            <img :src="slotProps.item.thumbnailImageSrc" :alt="slotProps.item.alt" style="display: block;" />
          </template>
        </Galleria>
      </div>
    </section>
    <!-- Sección de Habilidades con barras -->
    <section class="py-20 bg-gray-900">
      <div class="container mx-auto px-6">
        <div class="grid grid-cols-1 gap-8 ">
          <div>
            <section class="py-20 bg-gray-900">
              <div class="container mx-auto px-6">
                <div class="text-center mb-12">
                  <h2 class="text-4xl font-bold mb-2 text-green-300">Habilidades</h2>
                  <p class="text-gray-400">Tecnologías y herramientas que domino.</p>
                </div>
                <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6 justify-center">
                  <div class="bg-gray-800 rounded-lg shadow-lg p-6 flex flex-col items-center">
                    <Icon name="material-icon-theme:vue" class="font-bold text-5xl " />
                    <span class="font-bold text-lg">Vue.js</span>
                  </div>
                  <div class="bg-gray-800 rounded-lg shadow-lg p-6 flex flex-col items-center">
                    <Icon name="material-icon-theme:nuxt" class="font-bold text-5xl " />
                    <span class="font-bold text-lg">Nuxt.js</span>
                  </div>
                  <div class="bg-gray-800 rounded-lg shadow-lg p-6 flex flex-col items-center">
                    <Icon name="material-icon-theme:nest" class="font-bold text-5xl " />
                    <span class="font-bold text-lg">NestJS</span>
                  </div>
                  <div class="bg-gray-800 rounded-lg shadow-lg p-6 flex flex-col items-center">
                    <i class="pi pi-node text-4xl text-blue-400 mb-2"></i>
                    <Icon name="material-icon-theme:nodejs" class="font-bold text-5xl " />
                    <span class="font-bold text-lg">Node.js</span>
                  </div>
                  <div class="bg-gray-800 rounded-lg shadow-lg p-6 flex flex-col items-center">
                    <i class="pi pi-palette text-4xl text-purple-400 mb-2"></i>
                    <span class="font-bold text-lg">UI/UX Design</span>
                  </div>
                  <div class="bg-gray-800 rounded-lg shadow-lg p-6 flex flex-col items-center">
                    <Icon name="material-icon-theme:typescript" class="font-bold text-5xl " />
                    <span class="font-bold text-lg">JavaScript/TypeScript</span>
                  </div>
                </div>
              </div>
            </section>
          </div>
        </div>
      </div>
    </section>
    <!-- Educación -->
    <section class="py-16 bg-gradient-to-r from-gray-900 via-blue-950 to-green-900 text-white">
      <div class="container mx-auto px-6">
        <div class="text-center mb-12">
          <h2 class="text-4xl font-bold mb-2 text-blue-300">Educación</h2>
        </div>
        <div class="flex flex-wrap justify-center gap-8">
          <div class="bg-gray-900 rounded-lg shadow-lg p-6 w-72 flex flex-col items-center">
            <i class="pi pi-book text-4xl text-green-400 mb-2"></i>
            <span class="font-bold text-lg mb-1">Licenciatura en Informática</span>
            <span class="text-gray-400 mb-2">Universidad Nacional</span>
            <span class="text-blue-400">2017 - 2021</span>
          </div>
          <div class="bg-gray-900 rounded-lg shadow-lg p-6 w-72 flex flex-col items-center">
            <i class="pi pi-certificate text-4xl text-blue-400 mb-2"></i>
            <span class="font-bold text-lg mb-1">Certificación Vue.js</span>
            <span class="text-gray-400 mb-2">Vue School</span>
            <span class="text-green-400">2022</span>
          </div>
        </div>
      </div>
    </section>

    <!-- Sección de Fondo con Parallax -->
    <section class="parallax-section bg-fixed bg-cover bg-center py-32 relative">
      <div class="absolute inset-0 bg-black opacity-60"></div>
      <div class="container mx-auto px-6 text-center relative z-10">
        <h2 class="text-5xl font-extrabold text-white mb-4">¿Listo para empezar?</h2>
        <p class="text-xl text-gray-300 mb-8">
          Transformemos tu visión en una realidad digital impactante.
        </p>
        <Button label="Contáctanos Hoy" icon="pi pi-arrow-right" iconPos="right" severity="success" size="large"
          @click="contactModalVisible = true" />
      </div>
    </section>

    <!-- Testimonios con Carousel visual -->
    <section
      v-animateonscroll="{ enterClass: 'animate-enter fade-in-10 animate-duration-1000', leaveClass: 'animate-leave fade-out-0' }"
      ref="testimonials" class="bg-gradient-to-r from-gray-900 via-blue-950 to-green-900 py-20">
      <div class="container mx-auto px-6">
        <div class="text-center mb-12">
          <h2 class="text-4xl font-bold mb-2 text-green-300">Testimonios</h2>
        </div>
        <Carousel :value="testimonialsData" :numVisible="1" :numScroll="1" orientation="horizontal" circular
          :autoplayInterval="9000">
          <template #item="slotProps">
            <div class="flex flex-col md:flex-row items-center gap-8 bg-gray-900 rounded-xl shadow-xl p-8">
              <Avatar :image="slotProps.data.avatar" class="p-avatar-xl mb-4 md:mb-0" shape="circle" />
              <div>
                <p class="text-xl italic text-blue-300 mb-4">"{{ slotProps.data.quote }}"</p>
                <h4 class="font-bold text-green-400">{{ slotProps.data.name }}</h4>
                <p class="text-gray-400">{{ slotProps.data.title }}</p>
              </div>
            </div>
          </template>
        </Carousel>
      </div>
    </section>

    <!-- Proceso de Trabajo con Timeline -->
    <section v-animateonscroll="{ enterClass: 'animate-enter fade-in-10 slide-in-from-b-20 animate-duration-1000' }"
      ref="process" class="py-20">
      <div class="container mx-auto px-6">
        <div class="text-center mb-12">
          <h2 class="text-4xl font-bold mb-2">Nuestro Proceso de Trabajo</h2>
          <p class="text-gray-400">De la idea a la realidad en 4 pasos.</p>
        </div>
        <Timeline :value="processSteps" align="alternate" class="customized-timeline">
          <template #marker="slotProps">
            <span class="flex w-8 h-8 items-center justify-center text-white rounded-full z-10 shadow-md"
              :style="{ backgroundColor: slotProps.item.color }">
              <i :class="slotProps.item.icon"></i>
            </span>
          </template>
          <template #content="slotProps">
            <h3 class="text-xl font-bold mb-1">{{ slotProps.item.title }}</h3>
            <p class="text-gray-400">{{ slotProps.item.description }}</p>
          </template>
        </Timeline>
      </div>
    </section>

    <!-- Sección de Preguntas Frecuentes (FAQ) con Accordion -->
    <section v-animateonscroll="{ enterClass: 'animate-enter fade-in-10 slide-in-from-t-20 animate-duration-1000' }"
      ref="faq" class="bg-gray-800 py-20">
      <div class="container mx-auto px-6">
        <div class="text-center mb-12">
          <h2 class="text-4xl font-bold mb-2">Preguntas Frecuentes</h2>
          <p class="text-gray-400">Encuentra respuestas rápidas a tus dudas.</p>
        </div>
        <Accordion :activeIndex="0">
          <AccordionTab v-for="(item, index) in faqData" :key="index" :header="item.question">
            <p class="m-0 text-gray-300">{{ item.answer }}</p>
          </AccordionTab>
        </Accordion>
      </div>
    </section>

    <!-- Footer mejorado -->
    <footer class="container mx-auto px-6 py-8 text-center text-gray-400">
      <div class="flex justify-center gap-6 mb-4">
        <a href="https://github.com/joxmal" target="_blank" class="text-green-400 hover:text-blue-400 text-2xl"><i
            class="pi pi-github"></i></a>
        <a href="mailto:joxmal@email.com" class="text-blue-400 hover:text-green-400 text-2xl"><i
            class="pi pi-envelope"></i></a>
        <a href="https://linkedin.com/in/joxmal" target="_blank" class="text-green-400 hover:text-blue-400 text-2xl"><i
            class="pi pi-linkedin"></i></a>
      </div>
      <p>&copy; 2025 José Montes. Portafolio personal. Todos los derechos reservados.</p>
    </footer>

    <!-- Dialog de Contacto -->
    <Dialog v-model:visible="contactModalVisible" modal header="Hablemos de tu proyecto" :style="{ width: '50vw' }"
      :breakpoints="{ '960px': '75vw', '641px': '100vw' }">
      <div class="flex flex-col gap-6 mt-4">
        <IconField iconPosition="left">
          <InputIcon class="pi pi-user"></InputIcon>
          <InputText placeholder="Nombre" v-model="form.name" class="w-full" />
        </IconField>
        <IconField iconPosition="left">
          <InputIcon class="pi pi-at"></InputIcon>
          <InputText placeholder="Correo Electrónico" v-model="form.email" class="w-full" />
        </IconField>
        <Textarea v-model="form.message" placeholder="Cuéntanos tu idea..." rows="5" class="w-full" />
      </div>
      <template #footer>
        <Button label="Cancelar" text @click="contactModalVisible = false" />
        <Button label="Enviar Mensaje" icon="pi pi-send" @click="submitForm" />
      </template>
    </Dialog>

    <ScrollTop />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Menu from 'primevue/menu';

const toolbarMenu = [
  { label: 'Sobre Mí', command: () => scrollTo('aboutMe') },
  { label: 'Proyectos', command: () => scrollTo('projects') },
  { label: 'Proceso', command: () => scrollTo('process') },
  { label: 'Testimonios', command: () => scrollTo('testimonials') },
  { label: 'FAQ', command: () => scrollTo('faq') },
  { label: 'Contacto', icon: 'pi pi-envelope', command: () => contactModalVisible.value = true },
];
import { useToast } from "primevue/usetoast";

const toast = useToast();
const contactModalVisible = ref(false);
const form = ref({ name: '', email: '', message: '' });

// Refs para el scroll
const aboutMe = ref(null);
const projects = ref(null);
const process = ref(null);
const testimonials = ref(null);
const faq = ref(null);
const sectionRefs = { projects, process, testimonials, faq, aboutMe };

// Datos para el Proceso (Timeline)
const processSteps = ref([
  { title: '1. Descubrimiento', description: 'Analizamos tus ideas y definimos los objetivos del proyecto.', icon: 'pi pi-search', color: '#9333ea' },
  { title: '2. Diseño UI/UX', description: 'Creamos prototipos y un diseño visual centrado en la experiencia de usuario.', icon: 'pi pi-palette', color: '#db2777' },
  { title: '3. Desarrollo', description: 'Construimos la aplicación con tecnología de punta, limpia y escalable.', icon: 'pi pi-code', color: '#16a34a' },
  { title: '4. Despliegue', description: 'Lanzamos el proyecto y monitorizamos su rendimiento para asegurar el éxito.', icon: 'pi pi-rocket', color: '#fb923c' }
]);

// Datos para FAQ
const faqData = ref([
  { question: '¿Qué servicios ofrecen?', answer: 'Ofrecemos desarrollo web a medida, diseño UI/UX, consultoría tecnológica y optimización de rendimiento.' },
  { question: '¿Cuál es su proceso de trabajo?', answer: 'Nuestro proceso incluye descubrimiento, diseño, desarrollo y despliegue, asegurando una colaboración constante.' },
  { question: '¿Pueden trabajar con mi presupuesto?', answer: 'Nos adaptamos a diferentes presupuestos y ofrecemos soluciones flexibles para satisfacer tus necesidades.' },
  { question: '¿Cómo puedo solicitar una cotización?', answer: 'Puedes contactarnos a través del formulario de contacto en esta página o enviarnos un correo electrónico directamente.' }
]);

// Datos para la Galería de Proyectos Personales
const projectsData = ref([
  {
    itemImageSrc: '/proyects/project1.webp',
    thumbnailImageSrc: '/proyects/project1_trumb.webp',
    alt: 'Sass',
    title: 'Sass y SGI',
    description: 'Software de gestión integral para pequeñas empresas en la que pueden ver cuentas por cobrar y pagar, inventarios, clientes, proveedores, enviar notificaciones por correo, etc.',
    link: 'https://github.com/joxmal/portfolio',
    techs: [
      { name: 'Nuxt', icon: 'material-icon-theme:nuxt' },
      { name: 'Pocketbase', icon: 'simple-icons:pocketbase' },
      { name: 'Node.js', icon: 'material-icon-theme:nodejs' }
    ]
  },
  {
    itemImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria2.jpg',
    thumbnailImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria2s.jpg',
    alt: 'App de Tareas',
    title: 'App de Tareas',
    description: 'Aplicación para gestión de tareas con Vue y Tailwind.',
    link: 'https://github.com/joxmal/todo-app'
  },
  {
    itemImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria3.jpg',
    thumbnailImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria3s.jpg',
    alt: 'Landing Page',
    title: 'Landing Page',
    description: 'Página de presentación para startups, diseño responsivo.',
    link: 'https://github.com/joxmal/landing-page'
  },
  {
    itemImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria4.jpg',
    thumbnailImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria4s.jpg',
    alt: 'Dashboard Admin',
    title: 'Dashboard Admin',
    description: 'Panel administrativo con gráficos y gestión de usuarios.',
    link: 'https://github.com/joxmal/dashboard-admin'
  },
  {
    itemImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria5.jpg',
    thumbnailImageSrc: 'https://primefaces.org/cdn/primevue/images/galleria/galleria5s.jpg',
    alt: 'Blog Personal',
    title: 'Blog Personal',
    description: 'Blog técnico sobre desarrollo web y diseño.',
    link: 'https://github.com/joxmal/blog'
  }
]);
const responsiveOptions = ref([
  { breakpoint: '1024px', numVisible: 3 },
  { breakpoint: '768px', numVisible: 2 },
  { breakpoint: '560px', numVisible: 1 }
]);

// Datos para Testimonios
const testimonialsData = ref([
  { name: 'Ana García', title: 'CEO de TechCorp', avatar: 'https://primefaces.org/cdn/primevue/images/avatar/annafali.png', quote: 'El resultado final superó todas nuestras expectativas. Profesionalismo y calidad de principio a fin.' },
  { name: 'Carlos Rodríguez', title: 'Fundador de Innovatech', avatar: 'https://primefaces.org/cdn/primevue/images/avatar/bernardodominic.png', quote: 'Un equipo increíblemente talentoso que entiende las necesidades del cliente y entrega resultados excepcionales.' }
]);

// Lógica del Terminal
onMounted(() => {
  // Aquí podrías añadir lógica para interactuar con el terminal si fuera necesario
});

const scrollTo = (section) => {
  sectionRefs[section].value.scrollIntoView({ behavior: 'smooth' });
};

const submitForm = () => {
  if (form.value.name && form.value.email && form.value.message) {
    toast.add({ severity: 'success', summary: '¡Enviado!', detail: 'Gracias por contactarnos. Te responderemos pronto.', life: 3000 });
    contactModalVisible.value = false;
    form.value = { name: '', email: '', message: '' };
  } else {
    toast.add({ severity: 'warn', summary: 'Campos incompletos', detail: 'Por favor, rellena todos los campos.', life: 3000 });
  }
};
</script>

<style>
/* Estilos personalizados para mejorar la integración y el diseño */
body {
  background-color: #111827;
  color: #f9fafb;
}

.bg-grid-pattern {
  background-image: linear-gradient(rgba(255, 255, 255, 0.05) 1px, transparent 1px), linear-gradient(90deg, rgba(255, 255, 255, 0.05) 1px, transparent 1px);
  background-size: 2rem 2rem;
}

/* Personalización del Terminal */
.p-terminal {
  min-height: 12rem;
}

.p-terminal-command {
  color: #a78bfa;
  /* purple-400 */
}

/* Personalización del Diálogo */
.p-dialog .p-dialog-header,
.p-dialog .p-dialog-content,
.p-dialog .p-dialog-footer {
  background-color: #1f2937;
  color: #ffffff;
  border: 1px solid #374151;
}

.p-dialog .p-dialog-header-icon {
  color: #ffffff !important;
}

.p-inputtext,
.p-textarea {
  background-color: #374151;
  color: #ffffff;
  border: 1px solid #4b5563;
}

.p-float-label>label {
  color: #9ca3af;
}

/* Estilos para el ScrollTop */
.p-scrolltop.p-link {
  background-color: rgba(167, 139, 250, 0.8);
  /* purple-400 con opacidad */
  backdrop-filter: blur(5px);
}

/* Personalización del Timeline */
.customized-timeline .p-timeline-event:nth-child(even) {
  flex-direction: row-reverse;
}

.customized-timeline .p-timeline-event-content,
.customized-timeline .p-timeline-event-opposite {
  flex-basis: 45%;
}

.customized-timeline .p-timeline-event-connector {
  width: 2px;
  background: #4b5563;
}

/* Estilos para la sección Parallax */
.parallax-section {
  background-image: url('https://primefaces.org/cdn/primevue/images/galleria/galleria10.jpg');
  /* Puedes cambiar esta imagen */
}

/* Personalización del Accordion */
.p-accordion .p-accordiontab {
  margin-bottom: 1rem;
  border: 1px solid #374151;
  border-radius: 0.5rem;
  overflow: hidden;
}

.p-accordion .p-accordiontab-header {
  background-color: #1f2937;
  color: #ffffff;
  padding: 1rem 1.5rem;
  border-bottom: 1px solid #374151;
}

.p-accordion .p-accordiontab-header:not(.p-highlight):not(.p-disabled):hover {
  background-color: #374151;
}

.p-accordion .p-accordiontab-content {
  background-color: #111827;
  color: #e5e7eb;
  padding: 1rem 1.5rem;
}

.p-accordion .p-accordiontab-header-action {
  color: #ffffff;
}
</style>
