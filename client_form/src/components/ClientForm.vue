<template>
  <form class="form" @submit.prevent="submitHandler">
      <h1>Клиент</h1>
      <div class="wrapper">
          <div class="wrapper_elem">
                <div class="form-atribute">
                <div class="form-group">
                    <label for="surname">Ваша фамилия</label>
                    <input @blur="$v.formData.surname.$touch()"
                            :class="{'is-invalid': $v.formData.surname.$error}"
                            v-model="formData.surname"
                            type="text" class="form-input" id="surname">
                    <div v-if="!$v.formData.surname.required && $v.formData.surname.$error" class="invalid-text">
                        Поле обязательно для заполнения!
                    </div>
                    <div v-if="!$v.formData.surname.maxLength" class="invalid-text">
                        Должно быть менее 20 символов!
                    </div>
                    <div v-if="!$v.formData.surname.alphaText" class="invalid-text">
                        Вводите только русские буквы!
                    </div>
                </div>
                <div class="form-group">
                    <label for="name">Ваше имя</label>
                    <input @blur="$v.formData.name.$touch()"
                            :class="{'is-invalid': $v.formData.name.$error}"
                            v-model="formData.name"
                            type="text" class="form-input" id="name">
                    <div v-if="!$v.formData.name.required && $v.formData.name.$error" class="invalid-text">
                        Поле обязательно для заполнения!
                    </div>
                    <div v-if="!$v.formData.name.maxLength" class="invalid-text">
                        Должно быть менее 10 символов!
                    </div>
                    <div v-if="!$v.formData.name.alphaText" class="invalid-text">
                        Вводите только русские буквы!
                    </div>
                </div>
                <div class="form-group">
                    <label for="secname">Ваше отчество</label>
                    <input @blur="$v.formData.secname.$touch()"
                            :class="{'is-invalid': $v.formData.secname.$error}"
                            v-model="formData.secname"
                            type="text" class="form-input" id="secname">
                    <div v-if="!$v.formData.secname.maxLength" class="invalid-text">
                        Должно быть менее 15 символов!
                    </div>
                    <div v-if="!$v.formData.secname.alphaText" class="invalid-text">
                        Вводите только русские буквы!
                    </div>
                </div>
                <div class="form-group">
                    <label for="dateofbirth">Дата рождения</label>
                    <input @blur="$v.formData.dateofbirth.$touch()"
                            :class="{'is-invalid': $v.formData.dateofbirth.$error}"
                            v-model="formData.dateofbirth"
                            type="text" class="form-input" id="dateofbirth" placeholder="ДД/ММ/ГГГГ">
                    <div v-if="!$v.formData.dateofbirth.required && $v.formData.dateofbirth.$error" class="invalid-text">
                        Поле обязательно для заполнения!
                    </div>
                    <div v-if="!$v.formData.dateofbirth.alpha && $v.formData.dateofbirth.$error" class="invalid-text">
                        Вводите дату в формате ДД/ММ/ГГГГ!
                    </div>
                </div>
                <div class="form-group">
                    <label for="phone">Телефон</label>
                    <input @blur="$v.formData.phone.$touch()"
                            :class="{'is-invalid': $v.formData.phone.$error}"
                            v-model="formData.phone"
                            type="text" class="form-input" id="phone" placeholder="7">
                    <div v-if="!$v.formData.phone.required && $v.formData.phone.$error" class="invalid-text">
                        Поле обязательно для заполнения!
                    </div>
                    <div v-if="!$v.formData.phone.minLength" class="invalid-text">
                        Максимум 11 символов!
                    </div>
                    <div v-if="!$v.formData.phone.maxLength" class="invalid-text">
                        Должно быть не больше 11 символов!
                    </div>
                    <div v-if="!$v.formData.phone.alpha && $v.formData.phone.required" class="invalid-text">
                        Номер должен начинаться с 7!
                    </div>
                </div>
                <div class="form-group">
                    <label for="sex">Пол</label>
                    <select name="" id="sex" v-model="formData.sex" class="select">
                        <option value="male">Мужской</option>
                        <option value="female">Женский</option>
                    </select>
                </div>
                <div class="form-group">
                    <label for="group_client">Группа клиентов</label>
                    <select name="" id="group_client" v-model="formData.groupClient" multiple @blur="$v.formData.groupClient.$touch()" class="select_mult">
                        <option value="VIP">VIP</option>
                        <option value="Проблемные">Проблемные</option>
                        <option value="ОМС">ОМС</option>
                    </select>
                    <div v-if="!$v.formData.groupClient.required && $v.formData.groupClient.$error" class="invalid-text">
                        Выберите значения!
                    </div>
                </div>
                <div class="form-group">
                    <label for="doctor">Лечащий врач</label>
                    <select name="" id="doctor" v-model="formData.doctor" class="select">
                        <option value="Иванов">Иванов</option>
                        <option value="Захаров">Захаров</option>
                        <option value="Чернышева">Чернышева</option>
                    </select>
                    
                </div>
                <div class="form-group">
                    <label for="sms">Не отправлять СМС</label>
                    <input type="checkbox" id="sms" v-model="formData.sms">
                </div>
            </div>
            <div class="form-adres">
                <h2>Адрес</h2>
                <div class="form-group">
                    <label for="index">Индекс</label>
                    <input v-model="formAdres.index"
                            type="text" class="form-input" id="index">
                    <div v-if="!$v.formAdres.index.maxLength" class="invalid-text">
                        Должно быть 6 символов!
                    </div>
                    <div v-if="!$v.formAdres.index.alphaNumbers" class="invalid-text">
                        Только цифры!
                    </div>
                </div>
                <div class="form-group">
                    <label for="country">Страна</label>
                    <input v-model="formAdres.country"
                            type="text" class="form-input" id="country">
                        <div v-if="!$v.formAdres.country.alphaText" class="invalid-text">
                        Вводите только русские буквы!
                        </div>
                </div>
                <div class="form-group">
                    <label for="region">Область</label>
                    <input v-model="formAdres.region"
                            type="text" class="form-input" id="region">
                        <div v-if="!$v.formAdres.region.alphaText" class="invalid-text">
                        Вводите только русские буквы!
                        </div>
                </div>
                <div class="form-group">
                    <label for="city">Город</label>
                    <input @blur="$v.formAdres.city.$touch()"
                            :class="{'is-invalid': $v.formAdres.city.$error}"
                            v-model="formAdres.city"
                            type="text" class="form-input" id="city">
                        <div v-if="!$v.formAdres.city.required && $v.formAdres.city.$error" class="invalid-text">
                        Обязательное поле для заполнения!
                        </div>
                        <div v-if="!$v.formAdres.city.alphaText" class="invalid-text">
                        Вводите только русские буквы!
                        </div>
                </div>
                <div class="form-group">
                    <label for="street">Улица</label>
                    <input v-model="formAdres.street"
                            type="text" class="form-input" id="street">
                        <div v-if="!$v.formAdres.street.alphaText" class="invalid-text">
                        Вводите только русские буквы!
                        </div>
                </div>
                <div class="form-group">
                    <label for="building">Дом</label>
                    <input v-model="formAdres.building"
                            type="text" class="form-input" id="building">
                        <div v-if="!$v.formAdres.building.alphaNumbers" class="invalid-text">
                        Вводите только цифры!
                        </div>
                </div>
            </div>
            <div class="form-pasport">
                <h2>Паспорт</h2>
                <div class="form-group">
                    <label for="type_doc">Тип документа</label>
                    <select name="" id="type_doc" v-model="formPasport.type_doc" @blur="$v.formPasport.type_doc.$touch()" class="select">
                        <option value="Паспорт">Паспорт</option>
                        <option value="Свидетельство о рождении">Свидетельство о рождении</option>
                        <option value="Вод. удостоверение">Вод. удостоверение</option>
                    </select>
                    <div v-if="!$v.formPasport.type_doc.required && $v.formPasport.type_doc.$error" class="invalid-text">
                        Выберите значение!
                    </div>
                </div>
                <div class="form-group">
                    <label for="series">Серия</label>
                    <input v-model="formPasport.series"
                            type="text" class="form-input" id="series">
                        <div v-if="!$v.formPasport.series.minLength" class="invalid-text">
                        Минимум 4 цифры!
                        </div>
                        <div v-if="!$v.formPasport.series.maxLength" class="invalid-text">
                        Максимум 4 цифры!
                        </div>
                        <div v-if="!$v.formPasport.series.alphaNumbers" class="invalid-text">
                        Вводите только цифры!
                        </div>
                </div>
                <div class="form-group">
                    <label for="number">Номер</label>
                    <input v-model="formPasport.number"
                            type="text" class="form-input" id="number">
                        <div v-if="!$v.formPasport.number.minLength" class="invalid-text">
                        Минимум 6 цифр!
                        </div>
                        <div v-if="!$v.formPasport.number.maxLength" class="invalid-text">
                        Максимум 6 цифр!
                        </div>
                        <div v-if="!$v.formPasport.number.alphaNumbers" class="invalid-text">
                        Вводите только цифры!
                        </div>
                </div>
                <div class="form-group">
                    <label for="issued">Кем выдан</label>
                    <input v-model="formPasport.issued"
                            type="text" class="form-input" id="issued">
                        <div v-if="!$v.formPasport.issued.alphaText" class="invalid-text">
                        Вводите только русские буквы!
                        </div>
                </div>
                <div class="form-group">
                    <label for="data_issued">Дата выдачи</label>
                    <input @blur="$v.formPasport.data_issued.$touch()"
                            :class="{'is-invalid': $v.formPasport.data_issued.$error}"
                            v-model="formPasport.data_issued"
                            type="text" class="form-input" id="data_issued" placeholder="ДД/ММ/ГГГГ">
                    <div v-if="!$v.formPasport.data_issued.required && $v.formPasport.data_issued.$error" class="invalid-text">
                        Обязательное поле для заполнения
                    </div>
                    <div v-if="!$v.formPasport.data_issued.alpha && $v.formPasport.data_issued.$error" class="invalid-text">
                        Вводите дату в формате ДД/ММ/ГГГГ!
                    </div>
                </div>
            </div>
          </div>
          <button type="submit" class="btn">Создать клиента</button>
        </div> 
  </form>
</template>

<script>
import {required, maxLength, minLength, helpers} from 'vuelidate/lib/validators'
const alphaText = helpers.regex('alphaText', /^[а-яёА-ЯЁ]*$/),
    alphaNumbers = helpers.regex('Numbers', /[0-9]{1,10}/)

export default {
    data() {
        return {
            formData: {
                name: '',
                lastname: '',
                secondname: '',
                phone: '',
                sex: '',
                groupClient: [],
                doctor: '',
                sms: false
            },
            formAdres: {
                index: '',
                country: '',
                region: '',
                city: '',
                street: '',
                building: ''
            },
            formPasport: {
                type_doc: '',
                series: '',
                number: '',
                issued: '',
                data_issued: ''
            }
        }
    },
    validations: {
        formData: {
            name: {
                required,
                maxLength: maxLength(10),
                alphaText
            },
            surname: {
                required,
                maxLength: maxLength(20),
                alphaText
            },
            secname: {
                maxLength: maxLength(15),
                alphaText
            },
            phone: {
                required,
                minLength: minLength(11),
                maxLength: maxLength(11),
                alpha: val => /(7)\d{1,10}/.test(val)
            },
            dateofbirth: {
                required,
                alpha: val => /(\d{1,2}\/\d{1,2}\/\d{4})/.test(val)
            },
            groupClient: {
                required
            }
        },
        formAdres: {
            index: {
                maxLength: maxLength(6),
                alphaNumbers
            },
            country: {
                alphaText
            },
            region: {
                alphaText
            },
            city: {
                required,
                alphaText
            },
            street: {
                alphaText
            },
            building: {
                alphaNumbers
            }
        },
        formPasport: {
            type_doc: {
                required
            },
            series: {
                maxLength: maxLength(4),
                minLength: minLength(4),
                alphaNumbers
            },
            number: {
                maxLength: maxLength(6),
                minLength: minLength(6),
                alphaNumbers
            },
            issued: {
                alphaText
            },
            data_issued: {
                required,
                alpha: val => /(\d{1,2}\/\d{1,2}\/\d{4})/.test(val)
            }
        }
        
    },
    methods: {
        submitHandler() {
       if (this.$v.$invalid) {
            this.$v.$touch()
            return
        }
        console.log('Клиент успешно создан!');
        alert('Клиент успешно создан!')
        for (let item in this.formData) {
            if (typeof this.formData[item] === "object") {
                this.formData[item] = []
            } else {
                this.formData[item] = ''
            }
        }
        for (let item in this.formAdres) {
            this.formAdres[item] = ''
        }
        for (let item in this.formPasport) {
            this.formPasport[item] = ''
        }
        
        this.$v.$reset()
        } 
    },
    mounted() {
        if (this.formData.male === true) {
            this.formData.female = false
        } else {
            this.formData.female = true
        }
    }

}
</script>

<style lang="scss">
    .wrapper {
        width: 60%;
        height: 100%;
        border-radius: 10px;
        border: solid 1px #111;
        margin: 0 auto;
        padding: 50px;
        background-color: #FFF5EE;
    }
    .wrapper_elem {
        display: flex;
        justify-content: space-around;
        width: 100%;
    }
    .form-group {
        display: flex;
        flex-direction: column;
        // width: 20%;
        justify-content: start;
        align-items: start;
        margin: 20px;
    }
    .form-input {
        width: 200px;
        height: 30px;
        border-radius: 10px;
    }
    .discr-wrap {
        display: flex;
        justify-content: start;
        padding: 10px 0 10px 50px;
    }
    .is-invalid {
        border: solid 2px red;
    }
    .valid {
        border: solid 2px green;
    }
    .invalid-text {
        color: red;
        font-size: 12px;
    }
    .select {
        width: 200px;
        height: 30px;
        border-radius: 10px;
        &_mult {
            width: 200px;
            height: 60px;
        }
    }
    .form-pasport {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .form-adres {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .form-atribute {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .btn {
        width: 200px;
        height: 100px;
        background-color: red;
        border: 0px;
        border-radius: 20px 5px 20px 5px;
        font-size: 20px;
        color: honeydew;
    }
    @media screen and (max-width: 1200px) and (min-width: 961px){
        .wrapper_elem {
            display: flex;
            flex-wrap: wrap;
        }
        .form-input {
            width: 150px;
            height: 30px;
            border-radius: 10px;
        }
    }
    @media screen and (max-width: 960px) and (min-width: 721px){
        .wrapper_elem {
            display: flex;
            flex-direction: column;
            align-items: center;
            flex-wrap: wrap;
        }
        .form-input {
            width: 250px;
            height: 30px;
            border-radius: 10px;
        }
    }
    @media screen and (max-width: 720px) and (min-width: 576px) {
        .wrapper {
            width: 60%;
            height: 100%;
            border-radius: 10px;
            border: solid 1px #111;
            margin: 0 auto;
            padding: 50px;
            background-color: #FFA07A;
        }
        .wrapper_elem {
            display: flex;
            flex-direction: column;
            align-items: center;
            flex-wrap: wrap;
        }    
    }
    @media screen and (max-width: 577px) {
        .wrapper {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }
        .wrapper_elem {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            flex-wrap: wrap;
        }   
        .form-input {
            width: 200px;
            height: 30px;
            border-radius: 10px;
        } 
    }

</style>