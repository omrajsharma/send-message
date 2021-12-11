<template>
    <div class="container">
        <header>Save a message</header>
        <!-- Form -->
        <form @submit.prevent="addMessage">
            <!-- Input Name -->
            <div class="inputField">
                <label for="name"> Your Name </label> <br>
                <input type="text" name="name" id="name" v-model.trim="inputName" autofocus>
            </div>

            <!-- Input Complement -->
            <div class="inputField">
                <label for="complement"> Message for me </label> <br>
                <!-- <input type="text" name="message" id="message" v-model.trim="inputMessage"> -->
                <textarea name="message" id="message" cols="30" rows="3" v-model.trim="inputMessage"></textarea>
            </div>

            <!-- Errors -->
            <div class="error" v-if="invalidInput">
                <!-- Empty Input -->
                <p> <strong> Can't submit : </strong> Don't put the input field empty. </p>
            </div>
            <div class="error" v-if="error">
                <p> <strong>Error :</strong> {{error}} </p>
            </div>

            <!-- Submit -->
            <button>Send</button>
        </form>
    </div>

<!-- <hr/> -->
</template>

<script>
export default {
    data() {
        return {
            inputName: '',
            inputMessage: '',
            invalidInput: false,
            error: null
        };
    },
    methods: {
        addMessage() {
            if(this.inputName === '' || this.inputMessage === '') {
                this.invalidInput = true;
                return ;
            }

            this.error = null;

            // Post Request
            fetch('https://complement-me-default-rtdb.asia-southeast1.firebasedatabase.app/message.json', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    name: this.inputName,
                    message: this.inputMessage
                })
            }).then(response => {
                if(response.ok){
                    console.log('Data Saved Successfully!');
                } else {
                    throw new Error('Unable to save data!!!');
                }
            }).catch( error => {
                this.error = error.message;
            });
            this.inputName = '';
            this.inputMessage = '';
        }
    },
}
</script>

<style scoped>
header {
    font-size: 2rem;
    font-weight: 600;
    margin-bottom: 15px;
    padding: 2vh;
    color: white;
    text-shadow: 2px 4px 4px rgba(0,0,0,0.2),
                 0px -5px 10px rgba(255,255,255,0.15);
                 
}
.inputField {
    margin-bottom: 15px;
}
.inputField label {
    color: white;
    font-size: 1.2rem;
}
.inputField input, textarea {
    background: transparent;
    border: none;
    background-color: rgba(255, 255, 255, .15);  
    backdrop-filter: blur(5px);
    width: 80%;
    border-radius: 20px;
    padding: 5px;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 10px 50px;
    outline: none;
}

.error p {
    color: rgb(231, 231, 231);
}
.error strong {
    color: rgb(255, 104, 104);
}

button {
    background-color: transparent;
    border: none;
    color: white;
    background-color: rgba(255, 255, 255, .15);  
    backdrop-filter: blur(5px);
    padding: 10px 20px;
    border-radius: 20px;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 10px 50px;
    cursor: pointer;
}

hr {
    margin: 15px 0px 20px 0;
}
</style>