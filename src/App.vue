<template>
    <div class="container">
        <UserList/>
    </div>
</template>

<script>
import UserList from './components/UserList.vue'
    export default {
        components: {
            UserList
        }
    }
</script>

<style>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: "Inter", sans-serif;
}

body {
    background-color: #f7f7f7;
}

.container {
    width: 1000px;
    height: 647px;
    margin: auto;
}

</style>