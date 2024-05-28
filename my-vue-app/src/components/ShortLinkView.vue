<script setup lang="ts">
import CrossIcon from '../assets/cross.svg';

interface ShortLinkViewProps {
    shortLink : ShortLink;
}
</script>

<template>
    <div class="short-link-view">
        <div class="links-data">
            <a class="links-data-default" href="https://localhost.com/sK8qlw">https://localhost.com/sK8qlw</a>
            <a class="links-data-short" href="https://metanit.com/">https://metanit.com/</a>
        </div>
        <div class="short-link-menu">
            <p class="short-link-menu-date">27/05/2024 16:21 (UTC +03:00)</p>
            <button class="delete-button" type="button"><CrossIcon class="delete-button-icon"/></button>
        </div>
    </div>
</template>

<style>
.short-link-view {
    display: flex;
    justify-content: space-between;
    background-color: #fff;
    border-bottom: 1px solid #E7EBF3;
    padding: 20px 0px
}
.links-data {
    display: flex;
    flex-direction: column;
}
.short-link-menu {
    display: flex;
}
.short-link-delete {
    background-color: #ffffff00;
    border: 0;
    
}
.delete-button {
    border: none;
    background: none;
    padding: 0;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    max-height: 20px;
    padding-left: 15px;
}
.delete-button:hover {
    cursor: pointer;
}
.delete-button-icon:hover path{
    fill: #B31010;
    padding: 0px;
    margin: 0px
}
.short-link-menu-date, .links-data-default, .links-data-short{
    font-size: 12px;
    font-family: Inter;
    font-weight: 400;
    line-height: 14px;
    letter-spacing: 1%;
    color: #1A243F;
    text-decoration: none;
    margin-top: 1%;
}
.links-data-short{
    padding-top: 5px;
}
.links-data-default{
    font-size: 14px;
    font-weight: 500;
    line-height: 18px;
    color: #2E2BCA;
}
</style>