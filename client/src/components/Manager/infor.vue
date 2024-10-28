<template>
    <div>
        <h1>User Info</h1>
        <div v-if="user">
            <p>Username: {{ user.username }}</p>
            <p>Email: {{ user.email }}</p>
        </div>
        <div v-else>
            <p>Loading...</p>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            user: null,
        };
    },
    created() {
        this.fetchUserInfo();
    },
    methods: {
        async fetchUserInfo() {
            try {
                const response = await axios.get(`http://localhost:3001/api/users/${this.$route.params.id}`);
                this.user = response.data;
            } catch (error) {
                console.error('Error fetching user info:', error);
            }
        },
    },
};
</script>
