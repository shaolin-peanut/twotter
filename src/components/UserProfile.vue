<template>
    <div class="user-profile">
        <div class="user-profile_user-panel">
            <h1 class="user-profile_username">@{{ user.username }}</h1>
            <div class="user-profile_admin-badge" v-if="user.isAdmin">
              Admin
            </div>
            <div class="user-profile_follower_count">
                <strong>Followers: </strong> {{ followers }}
            </div>
        </div>
        <div class="user-profile_twoots-wrapper">
          <TwootItem
          v-for="twoot in user.twoots" 
          :key="twoot.id"
          :username="user.username" 
          :twoot="twoot"
          @like="toggleLike"
          />
        </div>
    </div>
</template>

<script>
import TwootItem from './TwootItem.vue'

export default {
    name: "UserProfile",
    data() {
        return {
            followers: 0,
            user: {
                id: 1,
                username: '_MitchelRomney',
                firstName: 'Mitch',
                lastName: 'Rom',
                email: 'mitchelromney@gmail.com',
                isAdmin: true,
                twoots: [
                    { id: 1, content: "blueberries.. few" },
                    { id: 2, content: "sheep cheese bruv, run the *** numbers" }
                ]
            }
        };
    },
    watch: {
        followers(newFollowerCount, oldFollowerCount) {
            if (oldFollowerCount < newFollowerCount) {
                console.log(`${this.user.username} has gained a follower!`);
            }
        }
    },
    computed: {
        fullName() {
            return `${this.user.firstName} ${this.user.lastName}`;
        }
    },
    methods: {
        followUser() {
            this.followers += 1;
        },
        toggleLike(id) {
          console.log(`Liked tweet #${id}`)
        }
    },
    mounted() {
        console.log("mounted is running....");
        this.followUser();
    },
    components: { TwootItem }
}
</script>

<style>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    width: 100%;
    padding: 50px 5%;
}

.user-profile_user-panel {
    display: flex;
    flex-direction: column;
    margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #DFE3E8;
}

.user-profile_admin-badge {
  background: purple;
  color: white;
  border-radius: 5px;
  margin-right: auto;
  font-weight: bold;
  padding: 0 10px;
}
</style>