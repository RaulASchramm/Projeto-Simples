<template>
    <div id="app" class="container">
        <h2 id="titulo">{{ titulo }}</h2>
        <div class="input-group">
            <input @keyup.enter="adicionarTarefa" class="form-control" type="text" v-model="novaTarefa">
            <span class="input-group-btn">
                <button @click="adicionarTarefa" class="btn btn-primary">
                    Adicionar
                </button>
            </span>
        </div>
    
        <ul id="lista">
            <li v-for="(tarefa, index) in tarefas" :key="index" :class="{ 'removed': tarefa.checked }">
                <input v-model="tarefa.checked" type="checkbox">
                <label>{{ tarefa.titulo }}</label>
                <button id="butt" @click="removerTarefa(index)" class="btn btn-sm btn-danger btn-outline">
                    Remover
                </button>
            </li>

        </ul>

        <em> Total de tarefas: </em> <span>{{ totalTarefas}}</span>
        <em> Tarefas concluidas </em> <span>{{ totalTarefasConcluidas}}</span>

        <footer>
            <hr>
            <em>Altere o titulo da sua lista de tarefas</em>
            <input type="text" v-model="titulo">
            <input type="color" name="color" id="colorInput" @change="changeBackgroundBodyColor()">
        </footer>
    </div>
</template>

<script>
export default {
  name: "App",
  data () {
    return {
            titulo: "Minhas tarefas",
            tarefas: [
            ],
            novaTarefa: ''
        }
    },
    methods: {
        adicionarTarefa() {
            this.tarefas.push({
                titulo: this.novaTarefa, checked: false
            })
            this.novaTarefa = ''
        },
        removerTarefa(index) {
            this.tarefas.splice(index, 1)
        },
        changeBackgroundBodyColor() {
            document.body.style.backgroundColor = document.getElementById('colorInput').value;
        }
    },
    computed: {
        totalTarefas() {
            return this.tarefas.length
        },
        totalTarefasConcluidas() {
            const conluidas = this.tarefas.filter(tarefa => tarefa.checked)
            return conluidas.length
        }
    }
};
</script>

<style>
.container{
    width: 40%;
    margin: 20px auto 0px auto;
}

.removed {
    color: gray;
}

.removed label {
    text-decoration: line-through;
}

ul li {
    list-style-type: none;
    font-size: 20px;
}

#titulo {
    text-align: center;
}

#app {
    border: 2px solid black;
    padding: 15px;
    background-color: white; 
}

#lista {
    margin-top: 1.3em;
    margin-left: -1.9em;
}

#butt {
    height: 30px;
}
</style>
