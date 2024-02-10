<template>
    <Header/>
    <div class="container">
        <Balance :total="total"/>
        <IncomeExpenses/>
        <TransactionList :transactions="transactions"/>
        <AddTransaction/>
    </div>
</template>
<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref, computed } from 'vue';

const transactions = ref([
    {id: 1, text: 'Netflix', amount: -19.99},
    {id: 2, text: 'Salary', amount: 499.99},
    {id: 3, text: 'Camera', amount: -1499.99},
    {id: 4, text: 'Laptop', amount: -2500.00}
]
);

const total = computed(() => {
    return transactions.value.reduce((acc, t) =>{
        return acc + t.amount;
    }, 0);
});

</script>