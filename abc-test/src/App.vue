<template>
    <div id="app">
        <HeadComponent></HeadComponent>
        <div v-if="screen === 1" class="first-content">
            <div class="date-start">
                <h3>{{text}} {{getDate.start}} по <span>{{getDate.end}}</span></h3>
            </div>
            <CongratsComponent></CongratsComponent>
            <p class="you-are-selected">
                {{selected}}
            </p>
            <GetEurosComponent></GetEurosComponent>
            <div class="footer-box">
                <div class="footer-box__items">
                    <div class="footer-box__items--item first">
                        <h3>{{attentionText}}</h3>
                        <p>{{attentionTextNext}}</p>
                    </div>
                    <div class="footer-box__items--item second">
                        <p>{{importantInformation}}</p>
                    </div>
                </div>
                <button v-on:click="changeScreen()" class="button">
                    {{buttonText}}
                </button>
            </div>
        </div>
        <div v-if="screen === 2" class="second-content">
            <div class="circle-box">
                <div class="circle-box__circle blue">1</div>
                <hr>
                <div class="circle-box__circle gray">2</div>
                <hr>
                <div class="circle-box__circle gray">3</div>
            </div>
            <h2>{{text2}}</h2>
            <div class="buttons-box ">
                <button v-on:click="changeScreen()" class="buttons-box__button">
                    {{buttonYes}}
                </button>
                <button v-on:click="changeScreen()" class="buttons-box__button">
                    {{buttonNo}}
                </button>
                <button v-on:click="changeScreen()" class="buttons-box__button">
                    {{buttonAll}}
                </button>
            </div>
        </div>
        <div v-if="screen === 3" class="third-page-content">
            <CongratsComponent></CongratsComponent>
            <p class="third-page-content__number-text">{{numberRegestrText}}</p>
            <p class="third-page-content__cal-text">{{calMobText}}</p>
            <GetEurosComponent></GetEurosComponent>
            <p class="third-page-content__timer">{{timerText}}<span>{{paseTime}}</span></p>
            <div class="third-page-content__qyt-lim-box">
                <h3 class="third-page-content__qyt-lim-box--h3">{{qytLimH}}</h3>
                <p class="third-page-content__qyt-lim-box--p">{{qytLimP}}</p>
            </div>

            <div class="third-page-content__button">
                <button class="third-page-content__button--button-box">
                    <div class="third-page-content__button--button-box__img-box">
                        <img src="./assets/img/icon_call.svg" alt="call">
                    </div>
                    <span>{{buttText}}</span>
                </button>
            </div>

            <div class="coment-text">
                <p>
                    {{downText}}
                </p>
            </div>
        </div>
    </div>
</template>
<script>
    import GetEurosComponent from './components/GetEurosComponent.vue'
    import HeadComponent from './components/HeadComponent.vue'
    import CongratsComponent from './components/CongratsComponent.vue'

    export default {
        data() {
            return {
                selected: 'Вы были отобраны для участия в финансовом эксперименте:',
                attentionText: 'Внимание:',
                attentionTextNext: 'Сегодня последний день, когда Вам доступна свободная регистрация!:',
                importantInformation: 'Для получения важной информации, просим ответить Вас всего на 3 простых вопроса:',
                buttonText: 'Принять участие',
                text: 'Дата проведения: c ',
                text2: 'Нуждаетесь ли Вы в дополнительных деньгах?',
                buttonYes: 'Да',
                buttonNo: 'Нет',
                buttonAll: 'Затрудняюсь ответить',
                numberRegestrText: 'Ваш номер телефона успешно зарегистрирован!',
                calMobText: 'Позвонив со своего мобильного телефона, вы получите доступ к персональному аудиосообщению:',
                timerText: 'Запись будет удалена через: ',
                qytLimH: 'Количество участников строго ограничено.',
                qytLimP: 'Звоните прямо сейчас, не упустите свой шанс!',
                buttText: 'Звонить и слушать',
                currentTime: 10800,
                timer: null,
                paseTime: '03:00:00',
                startDay: new Date(),
                screen: 1,
                downText: 'Doar pentru adulți. Acesta este un serviciu de divertisment care trebuie acceptat și interpretat ca atare. Accesând serviciul declarați că sunteți de acord cu acești termeni și condiții și că aveți peste 18 ani și aveți acordul titularului cartelei. Cost serviciu: 1.7euro + tva/minut în Orange, Vodafone, Telekom fix și mobil. Program non-stop. Apăsând pe butonul de pe pagina serviciului veți fi redirecționat către căsuța de apelare cu numărul cu suprataxă predefinit. Furnizor: ABCMobile OÜ; Reg № 14710834; Adresa: Estonia, Tallinn, Strada St. Petersburg 71-318, 11415. Support@abcmobile.com. Info serviciu voce: 0318260010, luni-vineri, 9:00-18:00.\n' +
                    '          Affiliate: mobstra.com',
            }
        },
        components: {
            HeadComponent,
            CongratsComponent,
            GetEurosComponent,
        },
        computed: {
            getDate() {
                let limitDay = 5;
                const date = this.startDay;
                const day = date.getDate();
                const month = date.getMonth();
                const year = date.getFullYear();

                const endDay = this.calcDate(limitDay).getDate();
                const endMonth = this.calcDate(limitDay).getMonth();
                const endYear = this.calcDate(limitDay).getFullYear();
                const start = `${this.checkedDate(day)}.${this.checkedDate(month)}.${year}`;
                const end = `${this.checkedDate(endDay)}.${this.checkedDate(endMonth)}.${endYear}`;


                return {start, end};
            },
        },
        methods: {
            checkedDate(item) {
                if (item < 10) {
                    return `0${item}`;
                }
                return item;
            },
            calcDate(takeDays) {
                let d = new Date();
                d.setDate(d.getDate() + takeDays);
                return d
            },
            startTimer() {
                this.timer = setInterval(() => {
                    this.currentTime--;
                    let sec = this.currentTime;
                    let h = sec / 3600 ^ 0;
                    let m = (sec - h * 3600) / 60 ^ 0;
                    let s = sec - h * 3600 - m * 60;
                    this.paseTime = `${this.checkedDate(h)}:${this.checkedDate(m)}:${this.checkedDate(s)}`;
                }, 1000)
            },
            stopTimer() {
                clearTimeout(this.timer)
            },
            changeScreen() {
                document.body.style.backgroundColor = "#FFFFFF";
                return this.screen++

            },
        },
        mounted() {
            this.startTimer()
        },
        destroyed() {
            this.stopTimer()
        },
        watch: {
            currentTime(time) {
                if (time === 0) {
                    this.stopTimer()
                }
            }
        },
    }
</script>
<style lang="scss">
   @import "app.scss";
</style>
