<template>
    <form>
        <input type="text" required  />
    </form>
    <div id="app">{{states}}</div>
     <button  @click="getStates">Get States</button>
</template>

<script>
import axios from 'axios';

export default {
    name: 'app',

    data () {
        return {
            states: ''
        }
    },

    methods: {
        async getStates () {
            try {
                const res = await axios.post(
                    'http://localhost:5000/graphql', {
                        query: '{ states { name } }'
                    });
                    
                this.states = res.data.data.states;

                console.log(this.states);
                
            } catch (e) {
                console.log('err', e)
            }
        }
    }
}
</script>

<style>
form {
    max-width: 700px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}

input {

    display: block;
    padding: 10px 6px;
    width: 100%;
    color: #555;
}
</style>