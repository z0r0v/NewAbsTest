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
                <button>
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
    @import 'varible.scss';
    body {
        margin: 0;
        background-color: $bg-color-master;
        font-family: $app-font;
    }
    button {
        padding: 0;
        border: none;
        font: inherit;
        color: inherit;
        background-color: transparent;
        cursor: pointer;
    }
    p, h2, h3 {
        margin: 0;
    }
    .first-content {
        width: 100%;
        display: block;
        .cong {
            animation: pulse 1.2s infinite;
            margin: 26px auto 20px auto;
            @include mq(Pro11X) {
                margin: 88px auto 44px auto;
            }
            @include mq(MacBook) {
                margin: 44px auto 33px auto;
            }
        }
        .get-euros {
            margin-top: 20px;
            margin-bottom: 24px;
            @include mq(Pro11X) {
                margin-top: 36px;
                margin-bottom: 82px;
            }
            @include mq(MacBook) {
                margin-top: 28px;
                margin-bottom: 35px;
            }
        }
        .footer-box {
            margin: 0 auto;
            border-radius: 30px 30px 0 0;
            background-color: $main-color-white;
            width: 320px;
            padding-top: 12px;
            padding-bottom: 26px;
            @include mq(Pro11X) {
                width: 375px;
                padding-top: 42px;
                padding-bottom: 46px;
            }
            @include mq(MacBook) {
                width: 320px;
                padding-top: 15px;
                border-radius: 20px 20px 0 0;
            }
        }
        .you-are-selected {
            width: 311px;
            margin: 0 auto;
            @include textLine(16px, 19px, center, $text-color-plum);
        }
        .footer-box__items {
            width: 300px;
            margin: 0 auto;
            .footer-box__items--item {
                position: relative;
                padding-left: 39px;
                border: 1px solid $border-color-grey;
                border-radius: 10px;
                margin-bottom: 9px;
                @include mq(Pro11X) {
                    margin-bottom: 22px;
                }
                @include mq(MacBook) {
                    padding-left: 42px;
                }
                &::before {
                    position: absolute;
                    content: ' ';
                    top: 6px;
                    left: 3px;
                    width: 29px;
                    height: 29px;
                    @include mq(MacBook) {
                        left: 6px;
                    }
                }
                h3, p {
                    font-size: 14px;
                    line-height: 16px;
                }
                h3 {
                    padding-top: 10px;
                    font-weight: bold;
                }
                p {
                    padding-bottom: 12px;
                }
            }
            .first {
                &::before {
                    background: url("./assets/img/icon_attantion.svg");
                }
            }
            .second {
                p {
                    padding-top: 10px;
                    @include mq(MacBook) {
                        padding-top: 8px;
                    }
                }
                &::before {
                    background: url("./assets/img/icon_ money.svg");
                }
            }
        }
        .button {
            position: relative;
            display: block;
            width: 276px;
            height: 48px;
            border-radius: 6px;
            font-weight: 500;
            font-size: 18px;
            box-shadow: 0 2px 0 0 $button-color-shadow;
            background: $button-color-green;
            color: $main-color-white;
            margin: 23px auto 0;
            @include mq(Pro11X) {
                margin: 43px auto 0;
            }
            @include mq(MacBook) {
                margin: 66px auto 4px;
            }
            &::after {
                position: absolute;
                content: ' ';
                width: 24px;
                height: 16px;
                top: 36%;
                right: 0;
                transform: translate(-50%, 0);
                background: url("./assets/img/icon_ arrow.svg");
            }
        }
        .date-start {
            background-color: $main-color-white;
            width: 320px;
            margin: 7px auto;
            @include mq(Pro11X) {
                width: 375px;
                margin: 4px auto;
            }
            @include mq(MacBook) {
                width: 320px;
                margin-top: 7px;
            }
            h3 {
                padding: 3px 0;
                @include textLine(12px, 14px, center, $text-color-blue);
                font-weight: bold;
                span {
                    color: $text-color-green;
                }
            }
        }
    }
    .second-content {
        hr {
            height: 4px;
            width: 100px;
            margin: 9px auto;
            background-color: $bg-color-hr-grey;
            border: none;
        }
        h2 {
            width: 279px;
            @include textLine(18px, 21px, center, $main-color-black);
            font-weight: normal;
            margin: 0 auto 47px auto;
            @include mq(Pro11X) {
                margin: 0 auto 61px auto;
            }
        }
        .circle-box {
            width: 270px;
            display: flex;
            justify-content: space-between;
            margin: 33px auto 51px auto;
            @include mq(Pro11X) {
                margin: 51px auto 71px auto;
            }
            .circle-box__circle {
                @extend %flex-centered;
                width: 22.22px;
                height: 22.22px;
                border-radius: 50% 50%;
                border: 1px solid $border-color-grey;
                color: $main-color-white;
            }
            .blue {
                background: $bg-gradient-blue;
            }
            .gray {
                background: $bg-gradient-grey;
            }
        }
        .buttons-box {
            @extend %flex-centered;
            flex-direction: column;
            &__button {
                width: 259px;
                height: 48px;
                font-weight: 500;
                border-radius: 6px;
                background-color: $bg-color-button-grey;
                margin-bottom: 15px;
                @include mq(Pro11X) {
                    margin-bottom: 22px;
                }
            }
        }
    }
    .third-page-content {
        .cong {
            color: $button-color-green;
            font-size: 25px;
            margin: 18px auto 8px auto;
            @include mq(Pro11X) {
                margin: 72px auto 34px auto;
            }
            @include mq(MacBook) {
                margin-top: 53px;
                margin-bottom: 17px;
            }
        }
        .get-euros {
            color: $main-color-black;
            margin: 18px auto 12px auto;
            @include mq(Pro11X) {
                margin: 36px auto 36px auto;
            }
            @include mq(MacBook) {
                margin: 25px auto 27px auto;
            }
        }
        &__number-text {
            width: 279px;
            margin: 0 auto 38px auto;
            font-weight: bold;
            @include textLine(14px, 16px, center, $button-color-green);
            margin-bottom: 13px;
            @include mq(Pro11X) {
                margin-bottom: 38px;
            }
            @include mq(MacBook) {
                margin-bottom: 32px;
            }
            animation: pulse 1.2s infinite;
        }
        &__cal-text {
            width: 279px;
            margin: 0 auto;
            @include textLine(16px, 19px, center, $main-color-black);
        }
        &__timer {
            width: 279px;
            margin: 0 auto;
            @include textLine(12px, 14px, center, $main-color-red);
        }
        &__qyt-lim-box {
            width: 300px;
            background-color: $bg-color-lite-brown;
            border: 1px solid $border-color-lite-brown;
            border-radius: 10px;
            margin: 18px auto 16px auto;
            @include mq(Pro11X) {
                margin: 43px auto 50px auto;
            }
            @include mq(MacBook) {
                margin: 26px auto 44px auto;
            }
            &--h3 {
                width: 230px;
                margin: 6px auto;
                font-weight: bold;
                @include textLine(16px, 19px, center, $main-color-black);
            }
            &--p {
                padding-bottom: 8px;
                @include textLine(16px, 19px, center, $main-color-black);
            }
        }
        &__button {
            display: flex;
            justify-content: center;
            margin-bottom: 52px;
            animation: pulse 2s infinite;
            button {
                position: relative;
                display: block;
                width: 213.19px;
                height: 63.53px;
                margin-left: 33px;
                background: linear-gradient(345.42deg, #2F9E31 -28.42%, #1A821C 92.44%, #01421F 165%);
                color: $main-color-white;
                border-radius: 10px;
                span {
                    display: block;
                    width: 127px;
                    padding-left: 47px;
                    line-height: 20px;
                    font-size: 22px;
                    font-weight: bold;
                    letter-spacing: 0.8px;
                    text-align: left;
                }
                &::before {
                    position: absolute;
                    width: 50px;
                    height: 50px;
                    top: -3px;
                    left: -33px;
                    content: ' ';
                    background: url("./assets/img/icon_call.svg") no-repeat center,
                    linear-gradient(345.42deg, #2F9E31 -28.42%, #1A821C 92.44%, #01421F 165%);
                    border: 11px solid #278c29;
                    border-radius: 50% 50%;
                    animation: vibrate 1s infinite;
                }
            }
        }
        .coment-text {
            width: 294px;
            height: calc(7px * 3);
            margin: 0 auto;
            padding: 5px;
            font-size: 9px;
            line-height: 14px;
            letter-spacing: 5px;
            overflow: hidden;
            text-align: justify;
            display: -webkit-box;
            -webkit-line-clamp: 3;
            -webkit-box-orient: vertical;
        }
    }
</style>
