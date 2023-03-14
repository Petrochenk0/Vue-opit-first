<script>

export default{
    data(){
        return{
            city:"",
            error:"",
            info:"",
        }
     
    },
    
    computed:{
        cityName(){
            return "<" + this.city + ">"
        },
        showTemper(){
            return this.info.data;
        }
    },
    
    methods:{
        getPogoda(){
            if(this.city.trim().length < 2){
                this.error = "Некоректные данные о городе :)"
                return false;
            }

            this.error = "";

            axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${city}&units=metric&appid=c26ada43d3fe3ed31de025a21409680f`)
                .then(res =>(this.info = res.data) )
        }
    }
}

</script>

<template>
    <div class="wrapper">
        <h1>Погодное приложение</h1>
        <p>Узнать погоду в {{ city == "" ? "вашем городе" : cityName}}</p>
        <input type="text" v-model="city" placeholder="Введите свой город">
        <button v-if="city !=''" @click="getPogoda()">Узнать погоду</button>
        <button disabled v-else>Введите название города</button>
        <p class="errorClass">{{error}}</p>
        <div v-show="info !=null" >
            <p>{{ showTemper }}</p>
        </div>
         
    </div>
</template>

<style scoped>
    .errorClass{
        color:rgb(140, 31, 31);
    }
    .wrapper{
        width:800px;
        height:400px;
        border-radius:40px;
        background-color:#1F0F24;
        padding:30px;
        color:#fff;
        text-align:center;
    }
    .wrapper h1{
        margin-top:50px;
    }
    .wrapper p{
        margin-top:15px;
    }
    .wrapper input{
        margin-top:20px;
        border:0;
        border-bottom:2px solid black;
        background: transparent;
        color:#fcfcfc;
        font-size: 14px;
        padding:6px;
        outline: none;
    }
    .wrapper input:focus{
       border-bottom-color: #6e2d7d;
    }
    .wrapper input:hover{
       border-bottom-color: #6e2d7d;
    }
    .wrapper button:disabled{
        background-color: rgb(144, 127, 70);
        cursor: not-allowed;
    }
    .wrapper button{
        background-color: rgb(202, 160, 24);
        color:white;
        border-radius: 10px;
        border:2px solid rgb(209, 144, 33);
        padding:13px;
        margin-left:15px;
        cursor: pointer;
        transition: transform 500ms ease;
    }
    
    .wrapper button:hover{
        transform: scale(1.1) translateY(-5px);
    }
</style>
