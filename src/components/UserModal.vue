<template>
    <div class="modal">
        <div class="modal-content">
            <p>Вы уверены, что хотите удалить этого пользователя?</p>
            <div class="btns">
                <button class="confirm"
                    @click="confirm"
                    >
                    Да
                </button>
                <button class="close"
                    @click="close"
                    >
                    Нет
                </button>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            show: {
                type: Boolean,
                required: true
            },
            confirm: {
                type: Function,
                required: true
            },
            close: {
                type: Function,
                required: true
            }
        }
    }
</script>

<style scoped>
.modal {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
}
  
.modal-content {
    background-color: #fff;
    padding: 36px;
    border-radius: 8px;
}

p {
    font-size: 12px;
    font-weight: 400;
    margin-bottom: 27px;
}

.btns {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}
.confirm {
    font-size: 12px;
    font-weight: 500;
    border: none;
    padding: 6px 36px;
    border-radius: 3px;
    color: #828282;
    background-color: #e0e0e0;
    cursor: pointer;
}

.close {
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