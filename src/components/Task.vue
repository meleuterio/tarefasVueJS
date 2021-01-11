<template>
    <div id="task">
        <form @submit.prevent="addTarefa">
            <input type="text" placeholder="Tarefa de hoje?" v-model="tarefa"/>
            <button type="submit"><strong>Adicionar</strong></button>
        </form>

        <item :lista="tarefas" :delete="apagarTask"/>

        <span v-show="tarefas.length > 0">
            Você tem <strong :class="{pend: pendente}"> {{ tarefas.length }} </strong> tarefas pendentes.
        </span>
    </div>
</template>

<script>
import Item from './Item'

export default {
    name: 'Task',
    components: {
        Item
    },
    data() {
        return {
            tarefa: '',
            tarefas: [],
            pendente: false
        }
    },
    methods: {
        addTarefa() {
            if(this.tarefa !== '') {
                this.tarefas.push({
                    text: this.tarefa,
                    key: Date.now()
                })
            } else {
                alert('Digite uma tarefa...')
                return
            }
            this.tarefa = ''
            console.log(this.tarefas)
        },
        apagarTask(key) {
            let filtro = this.tarefas.filter( (item) => { //salvar dentro de filtro, todas tarefas diferentes da key passada
                return (item.key !== key)
            })
            return this.tarefas = filtro
        }
    },
    watch: {
        tarefas() {
            localStorage.setItem('tarefas', JSON.stringify(this.tarefas)) //setando array convertida no localStorage
            this.tarefas.length > 4 ? this.pendente = true : this.pendente = false
        },
    },
    created() { //chamado automaticamente sempre que a instancia do Vue for criada
        const json = localStorage.getItem('tarefas')
        this.tarefas = JSON.parse(json) || []
    }
}
</script>

<style scoped>
    #task {
        max-width: 700px;
        background: #698F3F;
        border-radius: 4px;
        padding: 20px;
        margin: 20px auto;
        box-shadow: 0 0 20px rgba(0,0,0);
    }

    form {
        margin-top: 30px;
        display: flex;
        flex-direction: row;
    }

    form button {
        cursor: pointer;
        background: #E7DECD;
        border: 0;
        border-radius: 4px;
        margin-left: 10px;
        padding: 0 15px;
        display: flex;
        justify-content: center;
        align-items: center;
        color: #0A122A;
    }

    input {
        flex: 1;
        border: 1px solid #eee;
        font-size: 14px;
        border-radius: 4px;
        outline: none;
        padding: 6px 10px;
    }

    .pend {
        color: #9e0e0e;
    }
</style>