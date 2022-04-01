<script setup>
import { onMounted, ref } from "vue";
import axios from "axios";
import anime from "animejs";

const advice = ref(
  "It is easy to sit up and take notice, what's difficult is getting up and taking action."
);
const adviceId = ref("117");

function getAdvice() {
  axios
    .get("https://api.adviceslip.com/advice")
    .then((res) => {
      advice.value = res.data.slip.advice;
      adviceId.value = res.data.slip.id;
    })
    .catch((err) => {
      console.error(err);
    });
}

onMounted(() => {
  const btn = document.querySelector("#btn");

  btn.addEventListener("click", () => {
    anime.remove(btn);
    anime({
      targets: btn,
      rotate: ["0", "360"],
      scale: [0.9, 1],
    });
  });
});
</script>

<template>
  <div
    class="min-h-screen bg-darkBlue flex flex-col justify-center items-center"
  >
    <div
      class="relative w-[375px] md:w-[33.75rem] h-auto bg-darkGrayishBlue rounded-[14px] flex flex-col items-center py-12 px-2 md:px-10 shadow-2xl transition-all duration-300 ease-in-out"
    >
      <!-- ADVICE ID -->
      <div
        class="font-manrope font-bold text-neonGreen uppercase space-x-2 tracking-[0.24em] text-xs"
      >
        <span>Advice</span>
        <span>#{{ adviceId }}</span>
      </div>

      <!-- ADVICE -->
      <div class="text-center mt-9">
        <q
          id="advice"
          class="font-manrope text-lightCyan text-[1.75rem] font-extrabold select-auto"
          >{{ advice }}
        </q>
      </div>

      <!-- DIVIDER -->
      <div class="mt-12 mb-10">
        <div class="inline md:hidden">
          <svg
            class=""
            width="295"
            height="16"
            xmlns="http://www.w3.org/2000/svg"
          >
            <g fill="none" fill-rule="evenodd">
              <path fill="#4F5D74" d="M0 8h122v1H0zM173 8h122v1H173z" />
              <g transform="translate(138)" fill="#CEE3E9">
                <rect width="6" height="16" rx="3" />
                <rect x="14" width="6" height="16" rx="3" />
              </g>
            </g>
          </svg>
        </div>

        <div class="hidden md:inline">
          <svg width="444" height="16" xmlns="http://www.w3.org/2000/svg">
            <g fill="none" fill-rule="evenodd">
              <path fill="#4F5D74" d="M0 8h196v1H0zM248 8h196v1H248z" />
              <g transform="translate(212)" fill="#CEE3E9">
                <rect width="6" height="16" rx="3" />
                <rect x="14" width="6" height="16" rx="3" />
              </g>
            </g>
          </svg>
        </div>
      </div>

      <!-- DICE -->
      <button
        @click="getAdvice"
        id="btn"
        class="btn absolute -bottom-8 select-none group"
        aria-label="button"
      >
        <div
          class="absolute inset-0 w-16 h-16 bg-neonGreen rounded-full group-hover:blur-lg transition-all duration-300 ease-in-out"
        ></div>
        <div
          class="bg-neonGreen relative w-16 h-16 flex justify-center items-center rounded-full"
        >
          <svg
            class=""
            width="24"
            height="24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M20 0H4a4.005 4.005 0 0 0-4 4v16a4.005 4.005 0 0 0 4 4h16a4.005 4.005 0 0 0 4-4V4a4.005 4.005 0 0 0-4-4ZM7.5 18a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm4.5 4.5a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Zm0-9a1.5 1.5 0 1 1 0-3 1.5 1.5 0 0 1 0 3Z"
              fill="#202733"
            />
          </svg>
        </div>
      </button>
    </div>

    <!-- ATTRIBUTION -->
    <div
      class="mt-48 text-lightCyan font-manrope flex flex-col justify-center items-center space-y-4"
    >
      <div>
        Challenge by
        <a
          class="text-neonGreen"
          href="https://www.frontendmentor.io?ref=challenge"
          target="_blank"
          >Frontend Mentor</a
        >.
      </div>
      <div>
        Coded by
        <a
          class="text-neonGreen"
          href="https://github.com/disguy-droid"
          target="_blank"
          >Monish</a
        >.
      </div>
    </div>
  </div>
</template>

<style></style>
