<script>
    import { getModalStore } from "@skeletonlabs/skeleton";
    import { atcb_action } from "add-to-calendar-button";
    import ModalButtonsComponent from "$lib/components/modals/ModalButtonsComponent.svelte";
    import jQuery from "jquery";
    import greetings from "$lib/images/greetings-2.jpg";
    import majlisBertandang from "$lib/images/majlis-bertandang.jpg";
    import locationButton from "$lib/images/location-button.png";
    import calendarButton from "$lib/images/calendar-button.png";
  
    const modalStore = getModalStore();
  
    const modal = {
      type: "confirm",
      title: "Assalamualaikum dan Salam Sejahtera",
      image: greetings,
      body: "Buka kad jemputan?",
      buttonTextConfirm: "Ya",
      buttonTextCancel: "Kembali",
      response: (r) => {
        if (r) {
          playAudio();
  
          // const defaults = {
          //   spread: 360,
          //   ticks: 100,
          //   gravity: 0,
          //   decay: 0.94,
          //   startVelocity: 30,
          //   shapes: ["heart"],
          //   colors: ["FFC0CB", "FF69B4", "FF1493", "C71585"],
          // };
  
          // function shoot() {
          //   confetti({
          //     ...defaults,
          //     particleCount: 50,
          //     scalar: 2,
          //   });
  
          //   confetti({
          //     ...defaults,
          //     particleCount: 25,
          //     scalar: 3,
          //   });
  
          //   confetti({
          //     ...defaults,
          //     particleCount: 15,
          //     scalar: 4,
          //   });
          // };
  
          // setTimeout(shoot, 0);
          // setTimeout(shoot, 100);
          // setTimeout(shoot, 200);
  
          jQuery(".main-content").show();
        } else {
          location.reload();
        }
      },
    };
  
    modalStore.trigger(modal);
  
    const modalButtonsComponent = {
      // Pass a reference to your custom component
      ref: ModalButtonsComponent,
      // Add the component properties as key/value pairs
      props: { title: "bg-red-500" },
      // Provide a template literal for the default component slot
      slot: "<p>Skeleton</p>",
    };
  
    const buttonsModal = {
      type: "component",
      // Pass the component directly:
      component: modalButtonsComponent,
      disableAutoFocus: true,
    };
  
    const config = {
      name: "Majlis Pernikahan: Ummar & Puteri",
      description:
        "Laman Puteri, No. 2, Jalan Siswa Jaya 1, 86400 Parit Raja Batu Pahat, Johor",
      location: "1.856679194198063, 103.09936551324559",
      startDate: "2024-09-20",
      startTime: "15:00",
      endTime: "18:00",
      options: ["Google|Save to Google Calendar", "Apple|Save to Calendar"],
      timeZone: "currentBrowser",
    };
  
    function handleCalendarButtonClicked(event) {
      atcb_action(config, event.target);
    }
  
    function handleLocationButtonClicked() {
      modalStore.trigger(buttonsModal);
      document.activeElement.blur();
    }
  
    function playAudio() {
      var audio = document.getElementById("maher");
      audio.play();
    }
  
    function pauseAudio() {
      var audio = document.getElementById("maher");
      audio.pause();
    }
  </script>
  
  <div
    class="main-content grid h-screen place-items-center p-4"
    style="display: none;"
  >
    <audio id="maher">
      <source src="/PHbZ9SXHJwA_audio.mp3" type="audio/mpeg" />
    </audio>
    <p>
      <button class="btn-icon" on:click={playAudio}>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"
          />
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M15.91 11.672a.375.375 0 0 1 0 .656l-5.603 3.113a.375.375 0 0 1-.557-.328V8.887c0-.286.307-.466.557-.327l5.603 3.112Z"
          />
        </svg>
      </button>
      <button class="btn-icon" on:click={pauseAudio}>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          fill="none"
          viewBox="0 0 24 24"
          stroke-width="1.5"
          stroke="currentColor"
          class="w-6 h-6"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            d="M14.25 9v6m-4.5 0V9M21 12a9 9 0 1 1-18 0 9 9 0 0 1 18 0Z"
          />
        </svg>
      </button>
    </p>
    <div class="buttons-container">
      <img
        id="majlis-bertandang-img"
        src={majlisBertandang}
        alt="Wedding Card"
        class="wedding-card shadow-xl"
      />
      <div class="buttons">
        <button
          id="calendar-button"
          class="btn rounded-full"
          on:click={handleCalendarButtonClicked}
        >
          <img src={calendarButton} alt="View location" />
        </button>
        <button
          id="location-button"
          class="btn rounded-full"
          on:click={handleLocationButtonClicked}
        >
          <img src={locationButton} alt="Save to calendar" />
        </button>
      </div>
    </div>
  </div>
  
  <style lang="postcss">
    :global(body) {
      background: url("$lib/images/global-background.jpeg") no-repeat center
        center fixed;
      -webkit-background-size: cover;
      -moz-background-size: cover;
      -o-background-size: cover;
      background-size: cover;
    }
    /* .wedding-card {
      animation: reveal 3s linear forwards;
      max-height: 90vh;
      max-width: 90vw;
    } */
    @keyframes reveal {
      to {
        opacity: 1;
      }
      from {
        opacity: 0;
      }
    }
    #calendar-button {
      image-rendering: crisp-edges;
    }
    #location-button {
      image-rendering: crisp-edges;
    }
    #majlis-bertandang-img {
      max-height: 90vh;
      max-width: 90vw;
    }
    .buttons-container {
      position: relative;
      animation: reveal 3s linear forwards;
      max-height: 90vh;
      max-width: 90vw;
      margin: 0 auto;
    }
    .buttons {
      position: absolute;
      top: 55%; /* Adjust this value to move the buttons higher or lower */
      left: 50%;
      transform: translate(-50%, -50%);
      display: flex;
      gap: 10px; /* Adjust the gap between the buttons */
    }
    .btn {
      display: flex;
      align-items: center;
      justify-content: center;
      width: 90px; /* Set a fixed width for the buttons */
      height: 90px; /* Set a fixed height for the buttons */
      transition: transform 0.3s ease; /* Add transition for smooth scaling */
    }
  
    .btn:active {
      transform: scale(
        0.95
      ); /* Optional: Add a slight scale down effect on click */
    }
    .wedding-card {
      display: block;
      margin: 0 auto;
    }
  </style>
  