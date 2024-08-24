<template>
  <aside class="sidebar" data-sidebar>
    <div class="sidebar-info">
      <figure class="avatar-box">
        <img src="~/assets/images/my-avatar.png" alt="Om Kharche" width="80" />
      </figure>

      <div class="info-content">
        <h1 class="name" title="Om Kharche">Om Kharche</h1>

        <p class="title">Full Stack Developer</p>
      </div>

      <button class="info_more-btn" data-sidebar-btn>
        <span>Show Contacts</span>

        <ion-icon name="chevron-down"></ion-icon>
      </button>
    </div>

    <div class="sidebar-info_more">
      <div class="separator"></div>

      <ul class="contacts-list">
        <li class="contact-item">
          <div class="icon-box">
            <ion-icon name="mail-outline"></ion-icon>
          </div>

          <div class="contact-info">
            <p class="contact-title">Email</p>

            <a href="mailto:omtestmail@gmail.com" class="contact-link"
              >omtestmail@gmail.com</a
            >
          </div>
        </li>

        <li class="contact-item">
          <div class="icon-box">
            <ion-icon name="phone-portrait-outline"></ion-icon>
          </div>

          <div class="contact-info">
            <p class="contact-title">Phone</p>

            <a href="tel:+12133522795" class="contact-link">+91 935960743</a>
          </div>
        </li>

        <li class="contact-item">
          <div class="icon-box">
            <ion-icon name="calendar-outline"></ion-icon>
          </div>

          <div class="contact-info">
            <p class="contact-title">Birthday</p>

            <time datetime="1982-06-23">2 March, 2003</time>
          </div>
        </li>

        <li class="contact-item">
          <div class="icon-box">
            <ion-icon name="location-outline"></ion-icon>
          </div>

          <div class="contact-info">
            <p class="contact-title">Location</p>

            <address>Pune, India</address>
          </div>
        </li>
      </ul>

      <div class="separator"></div>

      <ul class="social-list">
        <li class="social-item">
          <a href="#" class="social-link">
            <ion-icon name="logo-facebook"></ion-icon>
          </a>
        </li>

        <li class="social-item">
          <a href="#" class="social-link">
            <ion-icon name="logo-twitter"></ion-icon>
          </a>
        </li>

        <li class="social-item">
          <a href="#" class="social-link">
            <ion-icon name="logo-instagram"></ion-icon>
          </a>
        </li>
      </ul>
    </div>
  </aside>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";

// Reactive data
const testimonials = ref([
  // Your testimonials data
]);

const selectOptions = ref(["Option 1", "Option 2", "Option 3"]);
const filterButtons = ref(["All", "Category 1", "Category 2"]);
const formInputs = ref(["name", "email", "message"]);

const formData = ref({
  name: "",
  email: "",
  message: "",
});

const navLinks = ref(["Home", "About", "Contact"]);
const pages = ref(["home", "about", "contact"]);

// Methods
const elementToggleFunc = (elem: HTMLElement) => {
  elem.classList.toggle("active");
};

const testimonialsModalFunc = (
  modalContainer: HTMLElement,
  overlay: HTMLElement
) => {
  modalContainer.classList.toggle("active");
  overlay.classList.toggle("active");
};

const filterFunc = (
  selectedValue: string,
  filterItems: NodeListOf<HTMLElement>
) => {
  filterItems.forEach((item) => {
    if (selectedValue === "all" || selectedValue === item.dataset.category) {
      item.classList.add("active");
    } else {
      item.classList.remove("active");
    }
  });
};

onMounted(() => {
  const sidebarBtn = document.querySelector(
    "[data-sidebar-btn]"
  ) as HTMLElement;
  const sidebar = document.querySelector("[data-sidebar]") as HTMLElement;
  const testimonialsItem = document.querySelectorAll(
    "[data-testimonials-item]"
  ) as NodeListOf<HTMLElement>;
  const modalCloseBtn = document.querySelector(
    "[data-modal-close-btn]"
  ) as HTMLElement;
  const overlay = document.querySelector("[data-overlay]") as HTMLElement;
  const select = document.querySelector("[data-select]") as HTMLElement;
  const selectItems = document.querySelectorAll(
    "[data-select-item]"
  ) as NodeListOf<HTMLElement>;
  const filterBtn = document.querySelectorAll(
    "[data-filter-btn]"
  ) as NodeListOf<HTMLElement>;
  const form = document.querySelector("[data-form]") as HTMLFormElement;
  const formInputs = document.querySelectorAll(
    "[data-form-input]"
  ) as NodeListOf<HTMLInputElement>;
  const formBtn = document.querySelector(
    "[data-form-btn]"
  ) as HTMLButtonElement;
  const navigationLinks = document.querySelectorAll(
    "[data-nav-link]"
  ) as NodeListOf<HTMLElement>;
  const pages = document.querySelectorAll(
    "[data-page]"
  ) as NodeListOf<HTMLElement>;

  // Sidebar toggle
  sidebarBtn.addEventListener("click", () => elementToggleFunc(sidebar));

  // Testimonials modal
  testimonialsItem.forEach((item) => {
    item.addEventListener("click", () => {
      const modalImg = document.querySelector(
        "[data-modal-img]"
      ) as HTMLImageElement;
      const modalTitle = document.querySelector(
        "[data-modal-title]"
      ) as HTMLElement;
      const modalText = document.querySelector(
        "[data-modal-text]"
      ) as HTMLElement;

      modalImg.src = (
        item.querySelector("[data-testimonials-avatar]") as HTMLImageElement
      ).src;
      modalImg.alt = (
        item.querySelector("[data-testimonials-avatar]") as HTMLImageElement
      ).alt;
      modalTitle.innerHTML = (
        item.querySelector("[data-testimonials-title]") as HTMLElement
      ).innerHTML;
      modalText.innerHTML = (
        item.querySelector("[data-testimonials-text]") as HTMLElement
      ).innerHTML;

      testimonialsModalFunc(modalImg, overlay);
    });
  });

  // Close modal
  modalCloseBtn.addEventListener("click", () =>
    testimonialsModalFunc(modalCloseBtn, overlay)
  );
  overlay.addEventListener("click", () =>
    testimonialsModalFunc(modalCloseBtn, overlay)
  );

  // Custom select toggle
  select.addEventListener("click", () => elementToggleFunc(select));

  // Select item click
  selectItems.forEach((item) => {
    item.addEventListener("click", () => {
      const selectedValue = item.innerText.toLowerCase();
      const selectValue = document.querySelector(
        "[data-selecct-value]"
      ) as HTMLElement;
      const filterItems = document.querySelectorAll(
        "[data-filter-item]"
      ) as NodeListOf<HTMLElement>;

      selectValue.innerText = item.innerText;
      elementToggleFunc(select);
      filterFunc(selectedValue, filterItems);
    });
  });

  // Filter button click
  filterBtn.forEach((btn) => {
    btn.addEventListener("click", () => {
      const selectedValue = btn.innerText.toLowerCase();
      const selectValue = document.querySelector(
        "[data-selecct-value]"
      ) as HTMLElement;
      const filterItems = document.querySelectorAll(
        "[data-filter-item]"
      ) as NodeListOf<HTMLElement>;

      selectValue.innerText = btn.innerText;
      filterFunc(selectedValue, filterItems);

      btn.classList.add("active");
    });
  });

  // Form validation
  formInputs.forEach((input) => {
    input.addEventListener("input", () => {
      if (form.checkValidity()) {
        formBtn.removeAttribute("disabled");
      } else {
        formBtn.setAttribute("disabled", "");
      }
    });
  });

  // Page navigation
  navigationLinks.forEach((link, index) => {
    link.addEventListener("click", () => {
      pages.forEach((page, pageIndex) => {
        if (link.innerHTML.toLowerCase() === page.dataset.page) {
          page.classList.add("active");
          navigationLinks[pageIndex].classList.add("active");
          window.scrollTo(0, 0);
        } else {
          page.classList.remove("active");
          navigationLinks[pageIndex].classList.remove("active");
        }
      });
    });
  });
});
</script>

<style></style>
