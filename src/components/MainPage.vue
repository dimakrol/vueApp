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
                msg:'hello vue',
                postData: {
                    grant_type: 'password',
                    client_id: 2,
                    client_secret: 'PWP90Q5LH7Igjqbnqtd668XmeEq1ID3fxTE37yF3',
                    username: 'dima.krol@mail.ru',
                    password: '123123',
                    scope: ''
                }
            }
        },
        methods: {
            callLara() {
                this.$http.post('http://localhost:8000/oauth/token', this.postData)
                    .then(response => {
                        console.log(response)
                    })
            }
        }
    }
</script>
