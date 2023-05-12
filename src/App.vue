<script setup>
import { ref } from 'vue'
const produtos = ref([

    {
        id: 1,
        nome: 'Camiseta',
        preco: 49.90,
        quantidade: 1
    },
    {
        id: 2,
        nome: 'Calça',
        preco: 99.90,
        quantidade: 1
    },
    {
        id: 3,
        nome: 'Meia',
        preco: 9.90,
        quantidade: 1
    },
    {
        id: 4,
        nome: 'Sapato',
        preco: 199.90,
        quantidade: 1
    },
    {
        id: 5,
        nome: 'Boné',
        preco: 29.90,
        quantidade: 1
    },
    {
        id: 6,
        nome: 'Óculos',
        preco: 99.90,
        quantidade: 1
    },
    {
        id: 7,
        nome: 'Relógio',
        preco: 299.90,
        quantidade: 1
    },
    {
        id: 8,
        nome: 'Bermuda',
        preco: 79.90,
        quantidade: 1
    },
    {
        id: 9,
        nome: 'Cueca',
        preco: 19.90,
        quantidade: 1
    },
   
])

//---------------------------------------------------------------

const carrinho = ref({
    items:[],
    total: 0,
})

function incrementar(index) {
    // carrinho.value[index].quantidade++
    carrinho.value.total -= carrinho.value.items[index].valorTotal
    carrinho.value.items[index].valorTotal = carrinho.value.items[index].preco * ++carrinho.value.items[index].quantidade
    carrinho.value.total += carrinho.value.items[index].valorTotal
}
function decrementar(index) {
    if (carrinho.value.items[index].quantidade > 1) {
        carrinho.value.total -= carrinho.value.items[index].valorTotal
        carrinho.value.items[index].valorTotal = carrinho.value.items[index].preco * --carrinho.value.items[index].quantidade
        carrinho.value.total += carrinho.value.items[index].valorTotal
    }
}
function remover(index){
    carrinho.value.total =  carrinho.value.total - carrinho.value.items[index].valorTotal
    carrinho.value.items.splice(index,1)

}

function addToCart(index) {
    carrinho.value.items.push({
        id: carrinho.value.length + 1,
        nome: produtos.value[index].nome,
        preco: produtos.value[index].preco,
        quantidade: 1,
        valorTotal: produtos.value[index].preco * 1
    })
    carrinho.value.total += produtos.value[index].preco * 1
}
let valorTotal = ref('')
function valorTtl ( ){
valorTotal = carrinho.value[index].preco + carrinho.value[index].preco
}

const mostrar_produto = ref(true)
const mostrar = ref(true)

function mostrar_car(){
    mostrar.value = true

}



</script>




<template>
    <header>
         <h1>Loja</h1>
    </header>
    <div class="produtos" v-if="mostrar">

        <h1>Produtos</h1>
        <ul>
            <li v-for="(item, index) in produtos ">
                {{ item.nome }} - R${{ item.preco }} <button @click="addToCart(index)">Add</button>
                
            </li>
        </ul>
        <button @click="mostrar = !mostrar">Carrinho</button>
    </div>
    <div class="carrinho" v-else>
            <h1>Carrinho</h1>
            <ul>
            
            <li v-for="(item, index) in carrinho.items"> {{ item.nome }} - {{ item.valorTotal.toFixed(2) }}
                <button @click="incrementar(index)">+</button>
                {{ item.quantidade }}
                <button @click="decrementar(index)">-</button>
                <button @click="remover(index)">Remover</button>
            </li>
        </ul>
        <button @click="mostrar = !mostrar">Produtos</button>
    </div>
    
    <footer>
    
        <h4>Total da compra: {{ carrinho.total.toFixed(2) }}</h4>
    </footer> 
    
</template>     


<style scoped>

header{
    background-color: black;
    width: 100%;
    padding: 1%;
    height: 100px;
    color: aliceblue;
    display: flex;  
    align-items: center;
    justify-content: center
}

button{
    border: 0;
    font-size: larger;
    background-color: black;
    color: aliceblue;
    border-radius: 8%;

}
.produtos{
    display: flex;
    align-items: baseline;
    justify-content: center;
}
ul{
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
}

li{
    padding: 10%;
    border: 1px solid black;
    width: 100px;
    height: 30px;
    list-style: none;
    margin-top: 10px;
    background-color: floralwhite;
    
}
footer{
    margin-top: 100px;
    padding: 2%;
    width: 100%;
    background-color: black;
    color: aliceblue;
    display: flex;
    justify-content: center;
    
}

.valortotal{
    padding: 5%;
    border: 1px solid black;
    background-color: floralwhite;
   
}
</style>


