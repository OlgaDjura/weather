<script>
import axios  from 'axios'
export default {
    data() {
        return {
            city: "",
            error: "",
            info: null
        }
    
    },
    computed: {
        cityName() {
            return "<<" + this.city + ">>"
        },
    
    showTemp() {
        return "Температура:" + this.info.main.temp
    },
    showFeelsLike() {
        return "Ощущается, как:" + this.info.main.feels_like

    },
    showMaxTemp() {
        return "Максимальная температура:" + this.info.main.temp_max
    },
    showMinTemp() {
        return "Минимальная температура:" + this.info.main.temp_min
    }
},
    methods: {
        getWeather() {
            if(this.city.trim().length < 2) {
                this.error = "Нужно название более одного символа"
                return false
            }
            this.error = ""

            axios.get(`https://https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=aacfdbed3483377443bbf3bf4213e0a0`)
            .then(res =>(this.info = res.data))
        }
    }

}
</script>

<template>
    <div class="wrapper">
        <h1>Погодное приложение </h1>
        <p>Узнать погоду в {{ city == "" ? "вашем городе" : cityName }}</p>
        <input type="text" v-on:input="this.city= $event.target.value" placeholder="Введите город">
        <button v-if="city !== ''" @click="getWeather()">Получить погоду</button>
        <button disabled v-else>Введите название города</button>
        <p class="error">{{ error }}</p>
        <div v-if="info !== null">
            <p>{{ showTemp }}</p>
            <p>{{ showFeelsLike }}</p>
            <p>{{ showMinTemp }}</p>
            <p>{{ showMaxTemp }}</p>
        </div>
        

    </div>
</template>

<style scoped>
.error {
    color: rgb(123, 41, 41);
}

.wrapper {
    width: 900px;
    height: 500px;
    border-radius: 50px;
    padding: 20px;
    background-color: antiquewhite;
    text-align: center;
}
.wrapper h1 {
    margin-top: 50px;
}
.wrapper p {
    margin-top: 20px;
}

.wrapper input {
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid rgb(47, 42, 42);
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
}

.wrapper input:focus {
    border-bottom-color: pink;
}

.wrapper button {
    background-color: rgb(161, 113, 121);
    color: rgb(79, 44, 49);
    border-radius: 10px;
    border: none;
    padding: 10px 15px;
    margin-left: 15px;
    cursor: pointer;
    transition: transform 500ms ease;
}

.wrapper button:hover {
    transform: scale(1.1) translateY(-5px);
}

.wrapper button:disabled {
    background-color: rgb(223, 98, 119);
    cursor: not-allowed;
}


</style>
