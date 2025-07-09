<template>
    <div class="myheader h-screen flex justify-center items-center">
        <div class="w-100 md:w-1/2 flex flex-col gap-y-10">
            <div class="text-5xl md:text-6xl font-bold text-white text-center text-shadow-lg">
                ¿Qué es el Ser Humano? - versión Paracas
            </div>
            <div class="text-2xl font-bold text-white text-center text-shadow-lg">
                Por la artista <span class="text-emerald-600 bg-white">Shoko Yamamoto</span> 
            </div>
            
            <div class="flex justify-center items-center">
                <div v-if="!countdownFinished" class="flex gap-6 text-white font-mono">
                    <div class="text-center">
                        <div class="text-3xl md:text-8xl font-bold text-shadow-md">
                            {{ days }}
                        </div>
                        <div>
                            Días
                        </div>
                    </div>
                    <div class="text-center">
                        <div class="text-3xl md:text-8xl text-shadow-lg">
                            {{ hours }}
                        </div>
                        <div>
                            Horas
                        </div>
                    </div>
                    <div class="text-center">
                        <div class="text-3xl md:text-8xl">
                            {{ minutes }}
                        </div>
                        <div>
                            Minutos
                        </div>
                    </div>
                    <div class="text-center">
                        <div class="text-3xl md:text-8xl    ">
                            {{ seconds }}
                        </div>
                        <div>
                            Segundos
                        </div>
                    </div>
                </div>
                <div v-else>
                    <p class="action-message">¡Es hora! La exposición ha comenzado.</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
// Fecha y hora objetivo (11 de julio de 2025, 12:00 PM)
const targetDate = new Date('2025-07-11T12:00:00');

// Referencias reactivas para los valores de la cuenta regresiva
const days = ref(0);
const hours = ref(0);
const minutes = ref(0);
const seconds = ref(0);
const countdownInterval = ref(null);

// Computed property para saber si la cuenta regresiva ha terminado
const countdownFinished = computed(() => {
  return days.value === 0 && hours.value === 0 && minutes.value === 0 && seconds.value === 0;
});

// Función para calcular y actualizar la cuenta regresiva
const updateCountdown = () => {
  const now = new Date().getTime();
  const distance = targetDate.getTime() - now;

  // Si la cuenta regresiva ha terminado o ya pasó la fecha
  if (distance < 0) {
    clearInterval(countdownInterval.value);
    days.value = 0;
    hours.value = 0;
    minutes.value = 0;
    seconds.value = 0;
    executeAction(); // Ejecutar la acción
    return;
  }

  // Calcular días, horas, minutos y segundos
  days.value = Math.floor(distance / (1000 * 60 * 60 * 24));
  hours.value = Math.floor((distance % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
  minutes.value = Math.floor((distance % (1000 * 60 * 60)) / (1000 * 60));
  seconds.value = Math.floor((distance % (1000 * 60)) / 1000);
};

// Función para ejecutar la acción cuando la cuenta regresiva termina
const executeAction = () => {
  console.log('¡La cuenta regresiva ha terminado! Se ejecuta la acción.');
  // Aquí puedes poner cualquier código que quieras ejecutar, por ejemplo:
  // alert('¡Es el día del evento!');
  // window.location.href = '/pagina-del-evento';
};

// Configurar el intervalo cuando el componente se monta
onMounted(() => {
  updateCountdown(); // Llamada inicial para mostrar el tiempo al cargar
  countdownInterval.value = setInterval(updateCountdown, 1000);
});

// Limpiar el intervalo cuando el componente se desmonta para evitar fugas de memoria
onUnmounted(() => {
  clearInterval(countdownInterval.value);
});
</script>

<style scoped>
.myheader {
    background-image: url('assets/images/header.png');
    background-color: rgba(0, 0, 0, 0.9);
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}
@media (max-width: 600px) {
  .myheader {
    background-position:  70% center;
  }
} 
</style>