<script>
import  Component  from './Component.vue';
export default{
    components:{
        Component
    },
    methods:{
      ComponentError(str){
        alert(str)
      }
    }
}
</script>

<template>
    <div class="form">
        <Component @error="ComponentError" is-number="false" max-length="10">Imie</Component>
        <Component @error="ComponentError" is-number="false" max-length="15">Nazwisko</Component>
        <Component @error="ComponentError" is-number="true" min-value="18">Wiek</Component>
        <Component @error="ComponentError" is-number="true">Waga</Component>
        <Component @error="ComponentError" is-number="false">Miejscowosc</Component>
    </div>
</template>

<style>
.form{
    flex: auto;
}
</style>