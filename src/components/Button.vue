<template>
    <form class="container"
          @submit.prevent='sendEmail'>
        <div class="col-sm-10 mb-3">
            <label class="form-label">Send Email to: </label>
            <input class='form-control'
                type="text" 
                v-model="state.email.address" 
                placeholder="youremail">
            <span class="form-text"
                v-if="v$.email.address.$error">
                {{ v$.email.address.$errors[0].$message }}
            </span>
        </div>
        <div class="col-sm-10 mb-3">
            <label class="form-label">Set timer: </label>
            <input class="form-control"
                type="text" 
                v-model="timer" 
                placeholder="ativate time, by default is 30s">
            <span class="form-text">
                ativate timer, by default is 30s.
            </span>
        </div>
        <div class="col-sm-10 mb-3">
            <label class="form-label">Title: </label>
            <input class='form-control'
                type="text" 
                placeholder="email title" 
                v-model="state.email.title">
            <span class="form-text" 
                v-if="v$.email.title.$error">
                {{ v$.email.title.$errors[0].$message }}
            </span>
        </div>
        <div class="col-sm-10 mb-3">
            <label class="form-label">Content: </label>
            <textarea class="form-control" 
                type="text" 
                placeholder="email content"
                v-model="state.email.content"></textarea>
            <span class="form-text"
                v-if="v$.email.content.$error">
                {{ v$.email.content.$errors[0].$message }}
            </span>
        </div>
        <button class="btn btn-primary"
            :disabled="timerActive">Email me!</button>
    </form> 
    
</template>

<script>
import useVuelidate from '@vuelidate/core'
import { required, email, minLength } from '@vuelidate/validators'
import { reactive, computed} from 'vue'
export default {
    name: 'Button',
    setup() {
        const state = reactive({
            email: {
                address: "",
                title: "",
                content: ""
            }
        })

        const rules = computed(() => {
            return {
                email: {
                    address: { required, email },
                    title: { required },
                    content: { required, minLenght: minLength(7) }
                }
            }
        })

        const v$ = useVuelidate(rules, state)

        return {
            state,
            v$,
        }
    },
    data() {
        return {
            timer: 30, // ms
            timerActive: false,
        }
    },
    methods: {
        // submit email
        sendEmail() {
            // check fields
            this.v$.$validate()
            if (this.v$.$error) {
                console.log(this.v$.$errors)
            } else if (!this.timerActive) {
                this.timerActive = !this.timerActive
                console.log(this.state, this.timer, this.timerActive)
                setTimeout(() => {
                    console.log(`${this.timer} later...`)
                    this.timerActive = false
                }, this.timer * 1000)      
            }  
        }
    }
}
</script>

<style>

</style>