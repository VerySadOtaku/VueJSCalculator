<template>
    <div class="calculator">
        <div class="display">{{ current || 0 }}</div>
        <div v-on:click="clear" class="btn">C</div>
        <div v-on:click="sign" class="btn">+/-</div>
        <div v-on:click="percent" class="btn">%</div>
        <div v-on:click="divide" class="btn command">/</div>
        <div v-on:click="append(7)" class="btn">7</div>
        <div v-on:click="append(8)" class="btn">8</div>
        <div v-on:click="append(9)" class="btn">9</div>
        <div v-on:click="multiply" class="btn command">*</div>
        <div v-on:click="append(4)" class="btn">4</div>
        <div v-on:click="append(5)" class="btn">5</div>
        <div v-on:click="append(6)" class="btn">6</div>
        <div v-on:click="subtract" class="btn command">-</div>
        <div v-on:click="append(1)" class="btn">1</div>
        <div v-on:click="append(2)" class="btn">2</div>
        <div v-on:click="append(3)" class="btn">3</div>
        <div v-on:click="add" class="btn command">+</div>
        <div v-on:click="append(0)" class="btn zero">0</div>
        <div v-on:click="dot" class="btn">.</div>
        <div v-on:click="equal" class="btn command">=</div>

    </div>
</template>

<script>
export default {
    data(){
        return{
            previous: null,
            current: '123',
            operator: null,
            operatorClicked: false
        }
    },
    methods: {
        clear(){
            this.current = '';
        },
        sign(){
            this.current = this.current.charAt(0) === '-' ?
                this.current.slice(1) : `-${this.current}`;
        },
        percent(){
            this.current = `${parseFloat(this.current) / 100}`
        },
        dot(){
            if(this.current.indexOf('.') === -1){
                this.append('.');
            }
        },
        append(number){
            if(this.operatorClicked){
                this.current = '';
                this.operatorClicked = false;
            }
            this.current = `${this.current}${number}`;
        },
        setPrevious(){
            this.previous = this.current;
            this.operatorClicked = true;
        },
        divide(){
            this.operator = (a, b) => a / b;
            this.setPrevious();
        },
        multiply(){
            this.operator = (a, b) => a * b;
            this.setPrevious();
        },
        subtract(){
            this.operator = (a, b) => a - b;
            this.setPrevious();
        },
        add(){
            this.operator = (a, b) => a + b;
            this.setPrevious();
        },
        equal(){
            this.current = `${this.operator(
                parseFloat(this.previous),
                parseFloat(this.current)
            )}`;
            this.previous = null;
        }

    }

}

</script>

<style scoped>

    *{
        box-sizing: border-box;
        margin: 0;
        padding: 0;
    }
    .calculator{
        max-width: 250px;
        font-size: 40px;
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-auto-rows: minmax(50px, auto);
        text-align: center;
    }

    .display{
        word-wrap: break-word;
        grid-column: 1 / 5;
        background-color: #12232E;
        color: #EEFBFB;
    }
    .btn{
        background-color:#EEFBFB;
        color: #12232E;
        border: 1px solid #12232E;
    }
    .zero{
        grid-column: 1 / 3;
    }
    .command{
        background-color: #007CC7;
    }
</style>