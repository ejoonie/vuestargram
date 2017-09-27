<template>
    <div>
        <template v-if="!isLoading">
            <feed v-for="feed in feeds" :key="feed.id"
                  :image-url="feed.images.standard_resolution.url"
                  :full-name="feed.caption.from.full_name"
                  :user-name="feed.caption.from.username"
                  :contents="feed.caption.text"></feed>
        </template>
        <template v-else>
            <md-progress class="" md-indeterminate></md-progress>
        </template>
    </div>
</template>


<script>
    import jsonp from 'jsonp'
    import Feed from './Feed'
    //    import MdProgress from "../../node_modules/vue-material/src/components/mdProgress/mdProgress.vue";

    export default {
//        components: {MdProgress},
        name: 'MyFeed',
        data() {
            return {
                isLoading: false,
                feeds: []
            }
        },
        mounted() {
            const token = localStorage.getItem('token')
            this.isLoading = true
            jsonp(`https://api.instagram.com/v1/users/self/media/recent?access_token=${token}`, null, (_, response) => {
                this.feeds = response.data
                this.isLoading = false
                console.log(response.data)
            })
        },
        components: {
            Feed
        }
    }
</script>