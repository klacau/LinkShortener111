<script setup lang="ts">
import Button from './Button.vue';
import InputField from './InputField.vue';
import NavigationBar from './NavigationBar.vue';
import {ref} from 'vue';
const inputLink = ref('');
</script>

<template>
<div class="main-page">
    <NavigationBar />
    <div class="main-page-content">
        
        <div class="main-page-form-wrapper">
            <div class="main-page-form">
                <h2 class="heading-2 main-page-form__heading">Вставьте ссылку для сокращения</h2>
                <div class="main-page-form-elements">
                    <InputField class="main-page__input-field" :text="inputLink" @change="(value) => inputLink = value" />
                    <Button label="Сократить" @click = "() => console.log(inputLink)" />
                </div>
            </div>
        </div>
    </div>
</div>
</template>

<style>
.main-page {
    background-color: #A6BBE3;
    height: 100%;
    display: flex;
    flex-direction: column;
}

.main-page-content {
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    align-items: stretch;
    justify-content: space-around;

}

.main-page-form-wrapper {
    display: flex;
    margin-top: -5%;
    justify-content: space-around;
    padding: 0px 24px;
}

.main-page-form {
    max-width: 520px;
    flex-grow: 1;
    display: flex;
    flex-direction: column;
    align-items: stretch;
}

.main-page-form-elements {
    display: flex;
    margin-top: 36px;
    justify-content: space-between;

}

.main-page__input-field {
    flex-grow: 1;
    margin-right: 12px;
}

.main-page-form__heading {
    text-align: center;
}
</style>
