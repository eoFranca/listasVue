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
    {
        id: 10,
        nome: 'Meia',
        preco: 9.90,
        quantidade: 1
    }
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
</script>




<template>
    <ul>
        <h1>Produtos</h1>
        <li v-for="(item, index) in produtos ">
            {{ item.nome }} - R${{ item.preco }} <button @click="addToCart(index)">add</button>

        </li>
    </ul>

    <div class="carrinho">
        <ul>
            <h1>Carrinho</h1>
            <li v-for="(item, index) in carrinho.items"> {{ item.nome }} - {{ item.valorTotal.toFixed(2) }}
                <button @click="incrementar(index)">+</button>
                {{ item.quantidade }}
                <button @click="decrementar(index)">-</button>
                <button @click="remover(index)">Remover</button>
            </li>
        </ul>
     <div class="valortotal">
         <h4>valor Total:{{ carrinho.total }}</h4>
    </div>
        
    </div>
</template>     


<style scoped>

li{
    padding: 20%;
    border: 1px solid black;
    list-style: none;
    display: grid;
    width: 250px;
    margin-top: 10px;
    background-color: floralwhite;
    
}
.valortotal{
    padding: 5%;
    border: 1px solid black;
    margin-left: 40px;
    margin-top: 10px;
    background-color: floralwhite;
   
}
</style>


