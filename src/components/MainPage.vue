<template>
    <div>
        <div>this is template body {{ msg }}</div>
        <button @click="callLara">Hello</button>

    </div>
</template>
<script>
    export default{
        data(){
            return{
                msg:'hello vue'
            }
        },
        methods: {
            callLara() {
                this.$http.get('http://localhost:8000/people')
                    .then(response => {
                        console.log(response.body)
                    })
            }
        }
    }
</script>
