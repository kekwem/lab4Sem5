<script>
    export default{
        emits:['change', 'error'],
        props:{
            maxLength: String,
            isNumber: String,
            minValue: String,
            maxValue: String
        },
        data(){
            return{
                inputValue: '',
                inputClass: '',
                isNumBool: false
            }
        },
        methods:{
            Clear(){
                this.inputValue = ''
            },
            checkLength(){
                if(this.inputValue.length > this.maxLength){
                    return false
                }
                return true
            },
            checkNumber(){
                if(this.isNumber == 'true'){
                    this.isNumBool = true
                }
                else if(this.isNumber == 'false'){
                    this.isNumBool = false
                }
                if(this.isNumBool && this.isNumBool == isNaN(this.inputValue)){
                    return false
                }
                return true
            },
            checkDiapason(){
                if(this.isNumBool){
                    var min = Number.parseInt(this.minValue)
                    var max = Number.parseInt(this.maxValue)
                    var value = Number.parseInt(this.inputValue)
                    if(value < min || value > max){
                        return false
                    }
                }
                return true
            }
        }, 
        watch:{
            inputValue(){
                this.$emit('change', this.inputValue)
                if(!this.checkNumber()){
                    this.inputClass = 'error'
                    this.$emit('error', 'Mozna wpisywac tylko liczby!')
                }
                else if(!this.checkDiapason()){
                    this.inputClass = 'error'
                    this.$emit('error', 'Liczba znajduje sie zewnatrz diapazonu!')
                }
                else if(!this.checkLength()){
                    this.inputClass = 'error'
                    this.$emit('error', 'Dlugosc nie moza byc wieksza niz ' + this.maxLength + '!')
                }
                else{
                    this.inputClass = ''
                }
            }
        }
    }
</script>

<template>
    <div class="main">
        <h3><slot></slot></h3>
        <input :class="inputClass" v-model='inputValue'/>
        <button @click="Clear()">Wyczyszcz pole!</button>
        
    </div>
</template>

<style>
.main{
    border: 2px solid black;
    padding: 10px;
}
.error{
    background-color: rgb(223, 98, 98);
}
</style>