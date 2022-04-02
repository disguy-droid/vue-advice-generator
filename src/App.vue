<script setup>
import { onMounted, reactive, ref } from "vue";
import axios from "axios";
import anime from "animejs";

let randomAdvice = reactive({
  advice:
    "It is easy to sit up and take notice, what's difficult is getting up and taking action.",
  adviceID: "117",
  id: "",
});

onMounted(() => {
  const API_URL = `https://api.adviceslip.com/advice/`;

  // BUTTON ANIMATION
  const btn = document.querySelector("#btn");
  btn.addEventListener("click", () => {
    let index = Math.floor(Math.random() * 200);
    randomAdvice.id = index;

    axios
      .get(`${API_URL}${randomAdvice.id}`)
      .then((res) => {
        randomAdvice.advice = res.data.slip.advice;
        randomAdvice.adviceID = res.data.slip.id;
      })
      .catch((err) => {
        console.error(err);
      });

    anime.remove(btn);
    anime({
      targets: btn,
      rotate: ["0", "360"],
      scale: [0.8, 1],
    });
  });
});
</script>

<template>
  <div
    class="min-h-screen bg-darkBlue flex flex-col justify-center items-center"
  >
    <main
      class="relative w-[375px] md:w-[33.75rem] h-auto bg-darkGrayishBlue rounded-[14px] flex flex-col items-center py-12 px-2 md:px-10 shadow-2xl transition-all duration-300 ease-in-out"
    >
      <!-- ADVICE ID -->
      <p
        class="font-manrope font-bold text-neonGreen uppercase space-x-2 tracking-[0.24em] text-xs"
      >
        <span>Advice</span>
        <span>#{{ randomAdvice.adviceID }}</span>
      </p>

      <!-- ADVICE -->
      <p class="text-center mt-6">
        <q
          id="advice"
          class="font-manrope text-lightCyan text-[1.75rem] font-extrabold select-auto"
          >{{ randomAdvice.advice }}
        </q>
      </p>

      <!-- DIVIDER -->
      <svg
        class="inline md:hidden my-8"
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

      <svg
        class="hidden md:inline my-8"
        width="444"
        height="16"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g fill="none" fill-rule="evenodd">
          <path fill="#4F5D74" d="M0 8h196v1H0zM248 8h196v1H248z" />
          <g transform="translate(212)" fill="#CEE3E9">
            <rect width="6" height="16" rx="3" />
            <rect x="14" width="6" height="16" rx="3" />
          </g>
        </g>
      </svg>

      <!-- DICE -->
      <button
        id="btn"
        class="btn absolute -bottom-8 select-none group"
        aria-label="button"
      >
        <span
          class="absolute inset-0 w-16 h-16 bg-neonGreen rounded-full group-hover:blur-lg transition-all duration-300 ease-in-out"
        ></span>
        <span
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
        </span>
      </button>
    </main>

    <!-- ATTRIBUTION -->
    <footer
      class="absolute bottom-4 md:bottom-24 text-lightCyan font-manrope flex flex-col justify-center items-center space-y-4"
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
    </footer>
  </div>
</template>

<style></style>
