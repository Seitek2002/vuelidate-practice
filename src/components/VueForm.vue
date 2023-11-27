<template>
    <form @submit.prevent="submitForm">
        <template v-if="!modal">
            <div class="customer-data">
                <label class="label">Фамилия*:</label>
                <input
                    v-model.trim="formData.surName"
                    type="text"
                    placeholder="Иванов"
                    :class="$v.formData.surName.$error ? 'is-invalid' : ''"
                />
                <p v-if="$v.formData.surName.$dirty && !$v.formData.surName.required" class="warning">
                    Это обязательное поле
                </p>
                <p v-if="$v.formData.surName.$dirty && !$v.formData.surName.minLength">
                    Поле должно содержать больше 3 символов
                </p>
                <p v-if="$v.formData.surName.$dirty && !$v.formData.surName.validChars">
                    Не думаю что фамилия человека может содержать цифры ;)
                </p>
                <label class="label">Имя*:</label>
                <input
                    v-model.trim="formData.name"
                    type="text"
                    placeholder="Иван"
                    :class="$v.formData.name.$error ? 'is-invalid' : ''"
                />
                <p v-if="$v.formData.name.$dirty && !$v.formData.name.required" class="warning">
                    Это обязательное поле
                </p>
                <p v-if="$v.formData.name.$dirty && !$v.formData.name.minLength" class="warning">
                    Поле должно содержать больше 3 символов
                </p>
                <p v-if="$v.formData.name.$dirty && !$v.formData.name.validChars" class="warning">
                    Не думаю что имя человека может содержать цифры ))
                </p>
                <label class="label">Отчество:</label>
                <input v-model.trim="formData.lastName" type="text" placeholder="Иванович" />
                <p v-if="$v.formData.name.$dirty && !$v.formData.name.validChars">
                    Не думаю что отчество человека может содержать цифры XD
                </p>
                <label class="label">Дата рождения*:</label>
                <input
                    v-model.trim="formData.dateOfBirth"
                    type="text"
                    placeholder="ДД.ММ.ГГГГ"
                    :class="$v.formData.dateOfBirth.$error ? 'is-invalid' : ''"
                />
                <p v-if="$v.formData.dateOfBirth.$dirty && !$v.formData.dateOfBirth.required" class="warning">
                    Это обязательное поле
                </p>
                <div v-if="$v.formData.dateOfBirth.$dirty && !$v.formData.dateOfBirth.validChars" class="warning">
                    Пожалуйста введите корректную дату
                </div>
                <label class="label">Номер телефона:</label>
                <input v-model.trim="formData.phoneNumber" type="text" placeholder="Номер телефона" />
                <label class="label">Пол:</label>
                <p>
                    <label>
                        <input v-model="formData.sex" type="radio" value="male" />
                        Мужчина
                    </label>
                    <label>
                        <input v-model="formData.sex" type="radio" value="female" />
                        Женщина
                    </label>
                </p>
                <label class="label">Группа клиентов*:</label>
                <p>
                    <select
                        class="multiselect"
                        v-model="formData.clientsGroup"
                        multiple
                        name="group[]"
                        :class="$v.formData.clientsGroup.$error ? 'is-invalid' : ''"
                    >
                        <option value="VIP">VIP</option>
                        <option value="Проблемные">Проблемные</option>
                        <option value="ОМС">ОМС</option>
                    </select>
                </p>
                <p v-if="$v.formData.clientsGroup.$dirty && !$v.formData.clientsGroup.required" class="warning">
                    Это обязательное поле
                </p>
                <label class="label">Лечащий врач:</label>
                <p>
                    <select class="select" v-model="formData.nurse" name="nurse">
                        <option selected value="Иванов">Иванов</option>
                        <option value="Захаров">Захаров</option>
                        <option value="Чернышева">Чернышева</option>
                    </select>
                </p>
                <p>
                    Не отправлять СМС
                    <input v-model="formData.sendSms" type="checkbox" />
                </p>
            </div>
            <div class="customer-adress">
                <label class="label">Индекс:</label>
                <input v-model.trim="formData.postCode" type="text" />
                <label class="label">Страна:</label>
                <input v-model.trim="formData.country" type="text" />
                <label class="label">Область:</label>
                <input v-model.trim="formData.region" type="text" />
                <label class="label">Город*:</label>
                <input v-model.trim="formData.city" type="text" :class="$v.formData.city.$error ? 'is-invalid' : ''" />
                <p v-if="$v.formData.city.$dirty && !$v.formData.city.required" class="warning">
                    Это обязательное поле
                </p>
                <p v-if="$v.formData.city.$dirty && !$v.formData.city.validChars" class="warning">
                    Пожалуйста, вводите только буквы
                </p>
                <label class="label">Улица:</label>
                <input v-model.trim="formData.street" type="text" />
                <label class="label">Дом:</label>
                <input v-model.trim="formData.homeNumber" type="text" />
            </div>
            <div class="customer-passport">
                <label class="label">Тип документа*:</label>
                <p>
                    <select
                        class="select"
                        v-model.trim="formData.documentType"
                        name="document"
                        :class="$v.formData.documentType.$error ? 'is-invalid' : ''"
                    >
                        <option value="Паспорт">Паспорт</option>
                        <option value="Свидетельство о рождении">Свидетельство о рождении</option>
                        <option value="Вод. удостоверение">Вод. удостоверение</option>
                    </select>
                </p>
                <p v-if="$v.formData.documentType.$dirty && !$v.formData.documentType.required" class="warning">
                    Это обязательное поле
                </p>
                <label class="label">Серия:</label>
                <input v-model.trim="formData.documentSeries" type="text" />
                <label class="label">Номер:</label>
                <input v-model.trim="formData.documentNumber" type="text" />
                <label class="label">Кем выдан:</label>
                <input v-model.trim="formData.documentFrom" type="text" />
                <label class="label">Дата выдачи*:</label>
                <input
                    type="text"
                    placeholder="ДД.ММ.ГГГГ"
                    v-model.trim="formData.documentDate"
                    :class="$v.formData.documentDate.$error ? 'is-invalid' : ''"
                />
                <p v-if="$v.formData.documentDate.$dirty && !$v.formData.documentDate.required" class="warning">
                    Это обязательное поле
                </p>
                <p v-if="$v.formData.documentDate.$dirty && !$v.formData.documentDate.validChars" class="warning">
                    Пожалуйста введите корректную дату
                </p>
            </div>
        </template>
        <div v-else class="modal">
            <SpinnerIcon v-if="pending" />
            <div v-if="submitted">
                <CorrectIcon />
                <p>Клиент успешно создан</p>
            </div>
        </div>
        <button :disabled="pending">Отправить</button>
    </form>
</template>

<script>
import CorrectIcon from './CorrectIcon.vue'
import SpinnerIcon from './SpinnerIcon.vue'
import { validationMixin } from 'vuelidate'
import { required, minLength, helpers } from 'vuelidate/lib/validators'

export default {
    mixins: [validationMixin],
    components: {
        CorrectIcon,
        SpinnerIcon,
    },
    data() {
        return {
            formData: {
                surName: '',
                name: '',
                lastName: '',
                dateOfBirth: '',
                phoneNumber: '',
                sex: '',
                clientsGroup: [],
                nurse: '',
                sendSms: false,
                postCode: '',
                country: '',
                region: '',
                city: '',
                street: '',
                homeNumber: '',
                documentType: '',
                documentSeries: '',
                documentNumber: '',
                documentFrom: '',
                documentDate: '',
            },
            modal: false,
            pending: false,
            submitted: false,
        }
    },
    validations: {
        formData: {
            surName: { required, minLength: minLength(3), validChars: helpers.regex(this, /^[a-zA-Zа-яА-Я]*$/) },
            name: { required, minLength: minLength(3), validChars: helpers.regex(this, /^[a-zA-Zа-яА-Я]*$/) },
            lastName: { minLength: minLength(3), validChars: helpers.regex(this, /^[a-zA-Zа-яА-Я]*$/) },
            dateOfBirth: { required, validChars: value => /^(\d{2}).(\d{2}).(\d{4})$/.test(value) },
            clientsGroup: { required },
            city: { required, minLength: minLength(2), validChars: helpers.regex(this, /^[a-zA-Zа-яА-Я]*$/) },
            documentType: { required },
            documentDate: { required, validChars: value => /^(\d{2}).(\d{2}).(\d{4})$/.test(value) },
        },
    },
    methods: {
        submitForm() {
            this.pending = true
            this.modal = true
            this.submitted = false
            this.$v.formData.$touch()

            if (!this.$v.formData.$error) {
                setTimeout(() => {
                    console.log('Валидация прошла успешно')

                    this.pending = false
                    this.submitted = true

                    setTimeout(() => {
                        this.submitted = false
                        this.modal = false
                    }, 2000)
                }, 3000)
            } else {
                this.pending = false
                this.modal = false
                this.submitted = false
            }
        },
    },
}
</script>

<style scoped lang="scss">
form {
    max-width: 480px;
    margin: 0 auto;
    text-align: left;
}
input[type='text'] {
    display: block;
    margin: 10px 0;
    width: 100%;
    box-sizing: border-box;
    padding: 10px;
    border: 1px solid #ccc;

    &.is-invalid {
        border: 1px solid red;
    }
}
input[type='checkbox'] {
    display: inline;
}
textarea {
    height: 160px;
}
.label {
    display: inline-block;
    margin-top: 30px;
    position: relative;
    font-size: 20px;
    color: #fff;
    margin-bottom: 10px;
    padding: 2px 0;
}

.label::before {
    content: '';
    display: block;
    width: 100%;
    height: 100%;
    background: #ff8800;
    position: absolute;
    top: 0;
    z-index: -1;
    padding-right: 40px;
    left: -30px;
    transform: rotateZ(-1deg);
}
button {
    display: block;
    margin-top: 30px;
    background: #ff8800;
    border: none;
    color: #fff;
    padding: 8px 16px;
    font-size: 18px;
    cursor: pointer;
}
button:disabled {
    opacity: 0.3;
    cursor: wait;
}
.pill {
    display: inline-block;
    margin: 10px 10px 0 0;
    color: #444;
    background: #ddd;
    padding: 8px;
    border-radius: 20px;
    cursor: pointer;
    font-size: 14px;
}
.select {
    display: block;
    width: 100%;
    padding: 0.375rem 2.25rem 0.375rem 0.75rem;
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #212529;
    background-color: #fff;
    background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 16 16'%3e%3cpath fill='none' stroke='%23343a40' stroke-linecap='round' stroke-linejoin='round' stroke-width='2' d='M2 5l6 6 6-6'/%3e%3c/svg%3e");
    background-repeat: no-repeat;
    background-position: right 0.75rem center;
    background-size: 16px 12px;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
    appearance: none;

    &:focus {
        outline: 0;
    }
}
.multiselect {
    display: block;
    width: 100%;
    padding: 0.375rem 2.25rem 0.375rem 0.75rem;
    -moz-padding-start: calc(0.75rem - 3px);
    font-size: 1rem;
    font-weight: 400;
    line-height: 1.5;
    color: #212529;
    background-color: #fff;
    background-repeat: no-repeat;
    background-position: right 0.75rem center;
    background-size: 16px 12px;
    border: 1px solid #ced4da;
    border-radius: 0.25rem;
    transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;

    &:focus {
        outline: 0;
    }
}
.warning {
    color: red;
}
select {
    option {
        font-weight: normal;
        display: block;
        min-height: 1.2em;
        padding: 0px 2px 1px;
        white-space: nowrap;
    }
}

.modal {
    width: 500px;
    height: 500px;
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;

    p {
        font-size: 30px;
    }
}
</style>
