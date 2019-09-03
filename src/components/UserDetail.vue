<template>
    <div class="wcol-md-6">
        <h3>Child Component 1</h3>
        <p>Ben User.vue isimli Parent Component'in içerisindeki bir Child componentim</p>
        <p>Kullanıcı adi : {{ name }}</p>
        <p>Tersten Kullanıcı adi : {{ switchName() }}</p>
        <p>kullanici yaşı : {{ age}}</p>
        <button @click="sendToParent">Veriyi Parent'a gönder</button>
    </div>
</template>

<script>
    import {eventBus} from "../main";

    export default {
        props: {
            name: {
                type: String,
                default: "burgazli.com"
            },
            age: String
        },

        methods: {
            switchName() {
                return this.name.split("").reverse().join("");
            },
            sendToParent() {
                this.$emit("data", "emir burgazli");
            }
        },
        created() {
            eventBus.$on("ageWasEdited", (age) => {
                this.age = age;
            })
        }
    }
</script>

<style scoped>
    div {
        background-color: lightcoral;
        padding: 20px;
        border: 1px solid #666;
        display: inline-block;
    }
</style>
