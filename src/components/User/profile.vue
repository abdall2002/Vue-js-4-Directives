<template>
    <div class="user_profile">
        <h3>User Profile</h3>
        <ul>
            <li>
                <span>Name: </span>{{ name }}
            </li>
            <li>
                <span>Also Known: </span>{{ alsoKnownAs }}
            </li>
            <li>
                <span>LastName: </span>{{ userLastname }}
            </li>
            <li>
                <span>Age: </span>{{ userAge }}
            </li>
        </ul>
        <h3>Parents</h3>
        <ul>
            <li v-for="(key,value,index) in userParents"  :key="index">
                <span>{{ key }}:</span> {{ value }}
            </li>
        </ul>
        <hr/>
        <button @click="updateLastname">Change from the child</button>
        <hr/>
        <button @click="sayHello">Say Hello</button>
        <hr/>
        <button @click="updateAge(50)">Update Age</button>
    </div>
</template>

<script setup>
const emit = defineEmits (['update-lastname', 'say-Hello']) 
const props = defineProps({
    alsoKnownAs: {
        type: String,
        required: true,
        default: 'N/A'
    },
    userLastname: {
        type: String,
        validator(value){
            if (value === 'Jones'){
                return true
            } else {
                return false
            }
        }
    },
    userAge: [Number, String],
    userParents: Object,
    updateAge: Function
    })
    const name = 'Steve'

    const updateLastname = () => {
        emit('update-lastname', 'Mickel')
        // props.userLastname = 'Mickel'
    }
    const sayHello = () => {
        emit('say-Hello')
    }
</script>

<style scoped>
    span{
        font-weight: 800;
    }
    .user_profile{
        border: 1px solid #2196F3;
        padding: 10px;
    }

</style>