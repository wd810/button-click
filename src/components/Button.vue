<template>
    <form class="container">
        <p>{{ email.address }}</p>
        <div class="col-sm-10">
            <label>Send Email to: </label>
            <input type="text" v-model="email.address" placeholder="youremail">
        </div>
        <div class="col-sm-10">
            <label>Set timer: </label>
            <input type="text" v-model="timer" placeholder="ativate time, by default is 30s">
        </div>
        <div class="col-sm-10">
            <label>Title: </label>
            <input type="text" placeholder="email title" required>
        </div>
        <div class="col-sm-10">
            <label>Content: </label>
            <textarea type="text" placeholder="email content"></textarea>
        </div>
        <button :disabled="timerActive" @click="sendEmail">Email me!</button>
    </form>
    
    
</template>

<script>
export default {
    name: 'Button',
    data() {
        let email = {
            address: "",
            title: "",
            content: ""
        }
        return {
            timer: 3, // ms
            timerActive: false,
            email
        }
    },
    methods: {
        sendEmail(e) {
            console.log(e)
            // check fields
            if (!this.timerActive) {
                this.timerActive = !this.timerActive
                console.log(this.email, this.timer, this.timerActive)
                setTimeout(() => {
                    console.log(`${this.timer} later...`)
                    this.timerActive = false
                }, this.timer * 1000)      
            } else {
                console.log("timer is active, click is disabled")
                
            }
            
        }
    }
}
</script>

<style>

</style>