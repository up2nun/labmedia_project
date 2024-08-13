<template>
    <div class="sort">
        <p class="sort__name"
            >
            Сортировка:
        </p>
        <p class="sort__date"
            @click="sortBy('registration_date')"
            :class="{'sort--active': isActiveSort('registration_date')}"
            >
            Дата регистрации
        </p>
        <p class="sort__rating"
            @click="sortBy('rating')"
            :class="{'sort--active': isActiveSort('rating')}"
            >
            Рейтинг
        </p>
    </div>
    <table>
        <thead>
            <tr>
                <th>Имя пользователя</th>
                <th>Email</th>
                <th>Дата регистрации</th>
                <th>Рейтинг</th>
            </tr>
        </thead>
        <tbody>
            <TableRow 
                v-for="user in paginatedUsers" 
                :key="user.id" 
                :user="user" 
                :confirmDelete="confirmDelete" 
            />
        </tbody>
    </table>
    <div class="pagination">
        <button class="prev__btn"
            @click="prevPage" :disabled="pagination.currentPage === 1"
            >
            Назад
        </button>
        <button class="next__btn"
            @click="nextPage" :disabled="pagination.currentPage === totalPages"
            >
            Вперед
        </button>
      </div>
</template>

<script>
import TableRow from './TableRow.vue';
    export default {
        components: {
            TableRow
        },
        props: {
            users: {
                type: Array,
                required: true
            },
            confirmDelete: {
                type: Function,
                required: true
            }
        },
        data() {
            return {
                pagination: {
                    currentPage: 1,
                    perPage: 7
                },
                sortKey: '',
                sortOrder: 1
            };
        },
        computed: {
            sortedUsers() {
                return [...this.users].sort((a, b) => {
                    let result = 0
                    if (a[this.sortKey] < b[this.sortKey]) result = -1
                    if (a[this.sortKey] > b[this.sortKey]) result = 1
                    return result * this.sortOrder
                })
            },
            paginatedUsers() {
                const start = (this.pagination.currentPage - 1) * this.pagination.perPage
                const end = start + this.pagination.perPage
                return this.sortedUsers.slice(start, end)
            },
            totalPages() {
                return Math.ceil(this.users.length / this.pagination.perPage);
            }   
        },
        methods: {
            sortBy(key) {
                if (this.sortKey === key) {
                    this.sortOrder *= -1
                } else {
                    this.sortKey = key;
                    this.sortOrder = 1
                }
            },
            isActiveSort(key) {
                return this.sortKey === key
            },
            prevPage() {
                if (this.pagination.currentPage > 1) {
                    this.pagination.currentPage--
                }
            },
            nextPage() {
                if (this.pagination.currentPage < this.totalPages) {
                    this.pagination.currentPage++
                }
            }
        }
    }
</script>

<style scoped>
.sort {
    display: flex;
    align-items: center;
    margin-top: 70px;
    gap: 8px;
}
.sort__name {
    color: #9eaab4;
    font-size: 10px;
    font-weight: 500;
}

.sort__date,
.sort__rating {
    color: #9eaab4;
    font-size: 10px;
    font-weight: 500;
    cursor: pointer;
    border-bottom: 1px dashed #9eaab4;
}

.sort__date.sort--active,
.sort__rating.sort--active {
    color: #333;
    border-bottom: 1px dashed #333;
}

table {
    width: 961px;
    height: 384px;
    background-color: #fff;
    margin-top: 15px;
    border-radius: 7px;
    border-collapse: collapse;
}

thead {
    align-items: center;
    justify-content: center;
}

tr {
    border-bottom: 1px solid #f7f7f7;
}

th {
    padding: 16px;
    text-align: left;
    font-size: 10px;
    font-weight: 500;
    color: #9eaab4;
    cursor: default;
}

.pagination {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    margin-top: 15px;
    gap: 10px;
}

.prev__btn {
    font-size: 12px;
    font-weight: 500;
    border: none;
    padding: 6px 36px;
    border-radius: 3px;
    color: #828282;
    background-color: #e0e0e0;
    cursor: pointer;
}
.prev__btn:disabled {
    color: #b1b1b1;
    background-color: #ececec;
    cursor: default;
}

.next__btn {
    font-size: 12px;
    font-weight: 500;
    border: none;
    padding: 6px 36px;
    border-radius: 3px;
    color: #fff;
    background-color: #0cb4f1;
    cursor: pointer;
}

</style>