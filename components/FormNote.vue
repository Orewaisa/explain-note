<template>
  <section class="git init ubuntu-regular">
    <div class="explain-note-body">
      <form v-if="!checkForm" class="form" @submit.prevent="checkingForm()">
        <div class="form-body">
          <div class="error">
            <p>{{ error }}</p>
          </div>
          <div class="form-input">
            <label>Дата</label>
            <input type="text" v-model="date" @input="formatDateInput" placeholder="12.04.2024" required>
          </div>
          
          <div class="form-input">
            <label>Пречислите подтверждение</label>
            <input type="text" v-model="confirmation" placeholder="Мой кот может подтвердить..." required>
          </div>
          
          <div class="form-input">
            <label>Текс записки</label>
            <input type="text" v-model="textNote" placeholder="Минимум 20 символов" required>
            <p>{{ sumbolCheck }}</p>
          </div>

          <div class="form-input">
            <label>ФИО заявителя</label>
            <input type="text" v-model="name" placeholder="Максимов Максим Иванович" required>
          </div>
          
          <div class="form-input">
            <label>Должность и место работы</label>
            <input type="text" v-model="placeWork" placeholder="Должность и место работы" required>
          </div>
          
          <div class="form-input">
            <label>ФИО Руководителя</label>
            <input type="text" v-model="nameDirector" placeholder="ФИО Получателя" required>
          </div>
          
          <div class="form-input">
            <label>Руководителю организации</label>
            <input type="text" v-model="nameOrganization" placeholder="Директору ООО 'Ромашка'" required>
          </div>
          
          <button type="submit">Создать записку</button>
        </div>
      </form>

      <div v-if="checkForm" class="explain">
        <div class="head-explain">
          <p>{{ nameOrganization }}</p>
          <p>{{ nameDirector }}</p>
          <p>от {{ name }}</p>
        </div>

        <div class="main-explain">
          <h2>Объяснительная</h2>

          <p>
            {{ textNote }}
          </p>
        </div>

        <div class="footer-explain">
          {{ date }}
        </div>
      </div>
      <button v-if="checkForm" @click="removeForm()">Новая записка</button>
            
    </div>
  </section>
</template>

<style lang="less" scoped>
  .explain-note {
    display: flex;
    justify-content: center;

    & .form {
      padding: 20px 20px;
      background: #e7f1fc;
      display: flex;
      justify-content: center;
      border-radius: 15px;

      & .form-body {

        & .error {
          color: red;
          text-align: center;
        }

        & .form-input {
          margin-bottom: 15px;
          display: flex;
          flex-direction: column;
  
          & > label {
            margin-bottom: 5px;
            color: #1373e5;
          }

          & > input {
            padding: 10px;
            width: 500px;

            @media (max-width: 500px) {
              width: 300px;
            }
            @media (max-width: 400px) {
              width: 200px;
            }
          }

          & > p {
            margin: 0px 10px;
            font-size: 15px;
            opacity: 50%;
          }
        }

        & > button {
          padding: 10px;
          font-size: 15px;
        }
      }
    }
    
    & .explain {
      padding: 10px;
      width: 600px;
      border: 1px solid #000;
      
      @media (max-width: 500px) {
        width: 350px;
      }

      & .head-explain {
        text-align: right;
      }

      & .main-explain {
        & > h2 {
          font-size: 30px;
          text-align: center;
        }

        & > p {
          margin-top: 40px;
          margin-bottom: 100px;
          padding: 0px 10px;
          overflow-wrap: break-word;
        }

        @media (max-width: 500px) {
          
          & > p {
            margin-bottom: 50px;
            margin-top: 10px;
            padding: 0px 20px;
            text-align: left;
          }

          & > h2 {
            font-size: 25px;
            text-align: center;
          }
        }
      }

      & .footer-explain {
        text-align: left;
      }
    }
  }
</style>

<script setup>
  const checkForm = ref(false);
  const date = ref("");
  const sumbolCheck = ref()
  const confirmation = ref("");
  const textNote = ref("");
  const name = ref("");
  const placeWork = ref("");
  const nameDirector = ref("");
  const nameOrganization = ref("");
  const error = ref("");


  function checkingForm() {
    console.log(date.value.length);
    if(date.value.length < 10) {
      error.value = "Дата не в правильном виде.\n00.00.0000";
      return;
    } else if(textNote.value.length < 20) {
      error.value = "Текст должен иметь минимум 20 символов!";
      return;
    }
    return submitForm();
  }

  function formatDateInput(event) {
      let value = event.target.value.replace(/[^0-9.]+/g, '');
      
      if (value.length === 2) {
        value = value + '.' ;
      }
      if (value.length === 5) {
        value = value + '.';
      }
      if (value.length > 10) {
        value = null;
      }
      
      date.value = value;
  }

  function submitForm() {
    checkForm.value = !checkForm.value;
  }

  function removeForm() {
    location.reload()
  }

  watch(textNote, newText => {
    sumbolCheck.value = newText.length;
  })
</script>