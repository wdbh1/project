<script setup>

import {ref} from "vue";

const name = ref('');
const question = ref('');
const phone = ref('');
const email = ref('');
const succes = ref(false);

async function onSubmit() {
  console.log(
      name.value,
      question.value,
      phone.value,
      email.value
  )
  const botToken = '6773456485:AAEywyvb02_3mNSqvH6dsxfvxU8egO6Vpn8';
  const chatId = '-1001990675974'
  const text = 'Новое сообщение:%0A%0A' +
      `Вопрос:%0A ${question.value}` +
      `Имя:%0A ${name.value}` +
      `Телефон:%0A ${phone.value}` +
      `Эл. почта: ${email.value}`;
  await fetch(`https://api.telegram.org/bot${botToken}/sendMessage?chat_id=${chatId}&text=${text}`)
      .then((response) => {
        if (response.status === 200) {
          succes.value = true;
        }
      })
      .catch(() => {
        succes.value = false;
        console.log(error)
      })
  const nassage = succes.value ? 'Отправлено' : 'Произошла ошибка, попробуйте позже!';
  alert(nassage);
  name.value = '';
      question.value = '';
      phone.value = '';
      email.value = '';
}
</script>

<template>
  <section class="feedback">
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-xl-6">
          <div class="feedback__text">
            <h2>Остались вопросы?</h2>
            <p>Свяжитесь с нами!</p>
          </div>
        </div>
        <div class="col-9 col-xl-6">
          <form class="form" method="post" @submit.prevent="onSubmit">
            <label class="mb-3">
                <textarea placeholder="Введите ваш вопрос" title="Ваш вопрос"
                          v-model='question'
                          required></textarea>
            </label>
            <div class="form__group">
              <label>
                <input type="text" placeholder="Ваше имя" title="Ваше имя"
                       v-model='name'
                       required>
              </label>
              <label>
                <input type="tel"
                       placeholder="+7(___)___-____"
                       pattern="[0-9]{11}"
                       maxlength="11"
                       title="Номер телефона"
                       v-model='phone'
                       required>
              </label>
              <label>
                <input type="email" placeholder="Электронная почта" title="Ваша электронная почта"
                       v-model='email'
                       required>
              </label>
            </div>
            <button class="button-primery" type="submit">Отправить</button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>

</style>