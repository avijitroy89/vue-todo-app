<template>
    <div class="addtodo">

        <form @submit="addtodo">
            <input type="text" v-model="title"/>
            <button class="btn">Add</button>
        </form>
    </div>
</template>
<script>
export default {
    name: "Addtodo",
    data(){
        return {
            title : ""
        }
    },
    methods:{
        addtodo (e){
            e.preventDefault();
            console.log(this.title);
            this.$emit("addtodo", this.title);
            this.title = "";
        }
    }
}
</script>
<style scoped>

</style>
