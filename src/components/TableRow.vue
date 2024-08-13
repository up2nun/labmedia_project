<template>
    <tr>
        <td class="username">{{ user.username }}</td>
        <td class="email">{{ user.email }}</td>
        <td class="registration_date">{{ user.registration_date }}</td>
        <td class="rating">{{ user.rating }}</td>
        <td>
            <img class="delete"
                src="../assets/icons/cancel.png"
                @click="confirmDelete(user.id)"
            >
        </td>
    </tr>
</template>

<script>
    export default {
        props: {
            user: {
                type: Object,
                required: true
            },
            confirmDelete: {
                type: Function,
                required: true
            }
        }
    }
</script>

<style scoped>
.username {
    padding-left: 16px;
    color: #0cb4f1;
    font-size: 12px;
    font-weight: 500;
}

.email,
.registration_date,
.rating {
    padding: 16px;
    color: #acacac;
    font-size: 12px;
    font-weight: 500;
}

.delete {
    cursor: pointer;
    width: 16px;
    height: 16px;
    color: #000;
    margin-right: 6px;
}
</style>