<template>
    <Header/>
    <div class="container">
        <Balance :total="+total"/>
        <IncomeExpenses :income="+income" :expenses="+expenses"/>
        <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
        <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
    </div>
</template>
<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import {useToast} from 'vue-toastification'

import { ref, computed } from 'vue';

const toast = useToast();

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

const income = computed(() => {
    return transactions.value
    .filter((t) => t.amount > 0)
    .reduce((acc, t) =>{
        return acc + t.amount;
    }, 0)
    .toFixed(2);
});

const expenses = computed(() => {
    return transactions.value
    .filter((t) => t.amount < 0)
    .reduce((acc, t) =>{
        return acc + t.amount;
    }, 0)
    .toFixed(2);
});

//add transaction

const handleTransactionSubmitted = (transactionData) => {
    transactions.value.push({
        id: generateUniqueId(),
        text: transactionData.text,
        amount: transactionData.amount,

    });

    toast.success('Transaction added')
}

const generateUniqueId = () => {
    return Math.floor(Math.random() * 1000000);
}

const handleTransactionDeleted = (id) => {
   // console.log(id)
    transactions.value = transactions.value.filter(
        (transaction ) => transaction.id !== id);

    toast.success('transaction deleted')
}
</script>