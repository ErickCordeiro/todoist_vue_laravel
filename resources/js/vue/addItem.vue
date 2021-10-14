<template>
  <div class="addItem">
    <input type="text" v-model="item.description" />
    <font-awesome-icon 
        icon="plus-square"
        @click="addItem()"
        :class="[item.description ? 'active': 'inactive', 'plus']" />
  </div>
</template>

<script>
export default {
    data: function(){
        return{
            item: {
                description: ""
            }
        }
    },
    methods: {
        addItem() {
            if( this.item.description == ''){
                return;
            }

            axios.post('api/item/store', {
                item:this.item
            }).then(response => {
                if(response.status == 201){
                    this.item.description = "";
                    this.$emit("reloadlist");
                }
            }).catch(error => {
                console.log(error)
            });
        }
    }
};
</script>

<style scoped>
.addItem {
  display: flex;
  justify-content: center;
  align-items: center;
}
input{
    background: #f7f7f7;
    border: none;
    outline: none;
    padding: 5px;
    margin-right: 10px;
    width: 100%;
}

.plus{
    font-size: 20px;
    cursor: pointer;
}

.active{
    color: #00ce25;
}

.inactive{
    color: #999999;
}
</style>