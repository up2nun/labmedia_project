<template>
    <h2>Список пользователей</h2>
    <div class="container">
        <div class="nav">
            <div class="search">
                <img class="search__icon"
                src="@/assets/icons/search.png"
                >
                <input
                    v-model="searchQuery"
                    @input="filterUsers" 
                    placeholder="Поиск по имени или e-mail" 
                />
            </div>
            <div class="clear"
                @click="clearFilter"
                >
                <img class="clear__icon"
                src="@/assets/icons/clean.png"
                >
                Очистить фильтр
            </div>
        </div>
        <UserTable
            :users="filteredUsers"
            :confirmDelete="confirmDelete"
        />
  
        <UserModal
            v-if="showModal"
            :show="showModal"
            :confirm="deleteUser"
            :close="closeModal"
        />
    </div>
</template>

<script>
import UserTable from './UserTable.vue';
import UserModal from './UserModal.vue';
import axios from 'axios';
    export default {
        components: {
            UserTable,
            UserModal
        },
        data() {
            return {
                users: [],
                searchQuery: '',
                showModal: false,
                userToDelete: null
            }
        },
        computed: {
            filteredUsers() {
            const query = this.searchQuery.toLowerCase()
            return this.users.filter((user) =>
                user.username.toLowerCase().includes(query) ||
                user.email.toLowerCase().includes(query))
            }
        },
        methods: {
            async fetchUsers() {
                try {
                    const response = await axios.get('https://5ebbb8e5f2cfeb001697d05c.mockapi.io/users')
                    this.users = response.data
                } catch (e) {
                    alert ('Ошибка')
                }
            },
            clearFilter() {
                this.searchQuery = ''
            },
            confirmDelete(userId) {
                this.userToDelete = userId
                this.showModal = true
            },
            deleteUser() {
                this.users = this.users.filter((user) => user.id !== this.userToDelete)
                this.closeModal()
            },
            closeModal() {
                this.showModal = false
                this.userToDelete = null
            }
        },
        mounted() {
            this.fetchUsers()
        }
    }
</script>

<style scoped>
h2 {
    color: #333;
    padding: 12px 27px;
}

.container {
    width: 961px;
    height: 102px;
    margin-left: 27px;
}

.nav {
    flex-direction: column;
    align-items: center;
    justify-content: space-between;
    background-color: #fff;
    border-radius: 7px;
    padding: 12px 16px 20px;
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1); 
}

.search {
    display: flex;
    align-items: center;
    background-color: #eceff0;
    border-radius: 4px;
    padding-left: 3px;
    margin-right: 27px;
}

.search__icon {
    height: 24px;
    width: 24px;
}

input {
    width: 901px;
    height: 34px;
    border: none;
    background-color: transparent;
    outline: none;
    padding-left: 5px;
}

input::placeholder {
    color: #9eaab4;
    font-size: 12px;
    font-weight: 500;
}

.clear {
    display: flex;
    align-items: center;
    margin-top: 20px;
    color: #4f4f4f;
    font-size: 12px;
    font-weight: 500;
    cursor: pointer;
    gap: 3px;
}

.clear__icon {
    width: 16px;
    height: 16px;
}

</style>