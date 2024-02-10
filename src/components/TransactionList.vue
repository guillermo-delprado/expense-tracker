<template>
    <h3>History</h3>
    <ul id="list" class="list">
        <li v-for="t in transactions"
        v-bind:key="t.id"
         :class="t.amount < 0 ? 'minus' : 'plus'"
         >
            {{ t.text }} <span>${{ t.amount }}</span> <button 
            class="delete-btn">x</button>
        </li>
        <!--<li class="minus">
           
        </li>

        <li class="plus">
            Cash <span>+$400</span> <button 
            class="delete-btn">x</button>
        </li>
        -->
    </ul>
</template>

<script>
export default {
    data(){
        return{
            transactions: [
                {id: 1, text: 'Netflix', amount: '-19.99'},
                {id: 2, text: 'Salary', amount: '499.99'},
                {id: 3, text: 'Camera', amount: '-1499.99'},
                {id: 4, text: 'Laptop', amount: '-2500.00'}
            ]

        }
    }
}
</script>