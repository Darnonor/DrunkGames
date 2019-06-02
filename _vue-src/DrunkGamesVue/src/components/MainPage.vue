<template>
    <div class="container">
        <div class="logo">
            <span>
                АлкоИгрища
            </span>
        </div>
        <b-form-input placeholder="Игрок 1"></b-form-input>
        <b-form-input placeholder="Игрок 2"></b-form-input>
        <b-form-input placeholder="Игрок 3"></b-form-input>
    </div>
</template>

<script>
export default {
    name: 'MainPage',
    props: {
        //msg: String
    }
}
</script>

<style>
.logo
{
    font-family: 'Lobster', cursive;
    /*font-family: 'El Messiri', sans-serif;*/
    font-size: 52px;
    color: white;
    margin-top: 35px;
    margin-bottom: 35px;
}

.container
{
    padding: 15px;
    text-align: center;
}

.form-control
{
    margin-bottom: 15px;
    border-radius: 0;
    border: 0;
    background-color:initial;
    color:white;
    margin-left: auto;
    margin-right: auto;
    width:70%;
}
</style>
