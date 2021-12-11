<template>
    <div class="container">
        <div v-for="message in messages" :key="message.name">
            <p> <strong> {{message.name}} : </strong> {{message.message}} </p>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            messages: []
        };
    },
    methods: {
        // Load messages
        loadMessages() {
            fetch('https://complement-me-default-rtdb.asia-southeast1.firebasedatabase.app/message.json')
            .then(response => {
                if(response.ok){
                    return response.json();
                }
            }).then ( data => {
                const messagesLoaded = [];
                for (const id in data){
                    messagesLoaded.push({name : data[id].name, message : data[id].message})                                        
                }
                this.messages = messagesLoaded;
            })
        }
    },
    mounted() {
        this.loadMessages();
    }

}
</script>

<style scoped>
div {
    text-align: left;
}
p {
    font-size: 0.8rem;
    color: #444
}
p strong {
    color: rgb(240, 240, 240);
}


</style>