<template>
  <div :class="['container wrap', {loading}]">
    <div class="row justify-content-center">
      <div class="col-md-auto">
        <h1 class="text-center">dados pessoais</h1>
        <form @submit.prevent="sendForm()" :class="[{submited}]">
          <div class="row mb">
            <div class="col-12 col-md">
              <div :class="['control-wrap', {'error': !formData.rg}]">
                <input v-model="formData.rg" type="text" class="form-control">
                <label >número do RG</label>
              </div>
            </div>
            <div class="col-12 col-md">
              <div :class="['control-wrap', {'error': !formData.data}]">
                <input
                  v-model="formData.data"
                  v-mask="'##/##/####'"
                  type="text"
                  class="form-control"
                >
                <label >data de emissão </label>
              </div>
            </div>
            <div class="col-12 col-md">
              <div :class="['control-wrap no-dot', {'error': !formData.orgao}]">
                <select v-model="formData.orgao" class="form-control">
                  <option
                    v-for="{value, label} in orgaos"
                    :key="value"
                    :value="value">
                    {{ label }}
                  </option>
                </select>
                <label >orgão expedidor</label>
              </div>
            </div>
          </div>
          <div class="row align-items-center justify-content-center mb">
            <div class="col-12 col-md-auto ">
              <label >Sexo</label>
            </div>
            <div class="col-6 col-md-auto">
              <label :class="['control-wrap custom-radio', {'error': !formData.sexo}]">
                <input type="radio" value="Masculino" v-model="formData.sexo" >
                <div class="form-control">
                  Masculino
                </div>
              </label>
            </div>
            <div class="col-6 col-md-auto">
              <label :class="['control-wrap custom-radio no-dot', {'error': !formData.sexo}]">
                <input type="radio" value="Feminino" v-model="formData.sexo" >
                <div class="form-control">
                  Feminino
                </div>
              </label>
            </div>
          </div>
          <div class="row align-items-center justify-content-center">
            <div class="col-auto ">
              <button type="submit" class="send" :disabled="submited && !validForm">
                continuar
              </button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import swal from 'sweetalert2'

export default {
  name: 'PersonalData',
  props: {
    active: {
      type: Number,
      default: 0
    }
  },
  data() {
    return {
      orgaos: [],
      loading: false,
      submited: false,
      validForm: false,
      formData: {
        rg: '',
        data: '',
        orgao: '',
        sexo: ''
      }
    }
  },
  watch: {
    formData: {
      handler(val) {
        this.validForm = this.validateForm(val)
      },
      deep: true
    }
  },
  mounted() {
    axios.get('/emissor.json').then(({ data }) => {
      this.orgaos = data.orgao_emissor
    })
  },
  methods: {
    sendForm() {
      if (this.validForm) {
        // fake ajax call
        this.loading = true
        setTimeout(() => {
          swal(
            'OK',
            'Dados enviados com sucesso',
            'success'
          )
          this.formData = {
            rg: '',
            data: '',
            orgao: '',
            sexo: ''
          }
          this.submited = false
          this.loading = false
        })
      }
      this.submited = true
    },
    validateForm(formData) {
      for (const value of Object.values(formData)) {
        if (!value) return false
      }
      return true
    }
  }
}
</script>

<style lang="scss" scoped>
@import '~@/scss/variables';
@import '~@/scss/mixins';

.send{
  background-color: $green;
  color: $milk;
  text-transform: uppercase;
  font-size: 21px;
  padding: 10px 50px;
  border: 0;
  cursor: pointer;
  &[disabled]{
    background-color: $bone;
  }
  &::after{
    content: '';
    display: inline-block;
    vertical-align: middle;
    margin-left: 30px;
    width: 0;
    height: 0;
    border-top: 10px solid transparent;
    border-bottom: 10px solid transparent;
    border-left: 10px solid $milk;
    position: relative;
    top: -2px;
  }
}
.row.mb{
  margin-bottom: 30px;
}
.wrap{
  padding-top: 40px;
  padding-bottom: 40px;
  position: relative;
  z-index: 0;
  &.loading{
    > *{
      opacity: 0.2;
    }
    &::after{
      content: 'AGUARDE';
      color: $choco;
      font-size: 25px;
      display: block;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
    }
  }
}
.control-wrap{
  display: flex;
  flex-direction: column;
  position: relative;
  z-index: 0;
  &::after{
    display: block;
    content: '';
    width: 5px;
    height: 3px;
    background-color: $choco;
    position: absolute;
    left: 100%;
    bottom: 24px;
    margin-left: 13px;
    @include small-device{
      display: none;
    }
  }
  &:last-child{
    &.no-dot::after{
      display: none;
    }
  }
  label{
    order: 0;
    @include small-device{
      margin-top: 20px;
    }
  }
  .form-control{
    order: 1;
  }
}
h1{
  color: $choco;
  font-size: 34px;
  text-transform: uppercase;
  font-weight: 900;
  letter-spacing: 2px;
  text-align: center;
  margin-bottom: 40px;
}
label{
  font-size: 13px;
  color: $choco;
  text-transform: uppercase;
  font-weight: bold;
  transition: all 150ms;
}
.form-control{
  background-color: transparent;
  border: 3px solid $choco;
  border-radius: 1px;
  font-size: 21px;
  color: $choco;
  font-weight: bold;
  text-transform: uppercase;
  padding-top: 8px;
  padding-bottom: 8px;
  padding-left: 25px;
  padding-right: 25px;
  height: auto;
  max-width: 220px;
  @include small-device{
    max-width: none;
  }
  &:focus{
    box-shadow: none;
    border-color: $blue;
    color: $blue;
    & + label{
      color: $blue;
    }
  }
}
.submited{
  .error{
    .form-control{
      border-color: red;
      color: red;
      & + label{
        color: red;
      }
    }
  }
}
.custom-radio{
  cursor: pointer;
  input{
    display: none;
    &:checked + .form-control{
      border-color: $blue;
      color: $blue;
    }
  }
}
select{
  option{
    font-size: 16px;
  }
}
</style>
