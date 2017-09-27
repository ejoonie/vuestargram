<template>
    <div>
        <md-input-container>
            <label>Tag Search</label>
            <md-input @input.native="tagName = $event.target.value" @keydown.native.enter="search"></md-input>
        </md-input-container>

        <md-card v-for="feed in feeds" :key="feed.id">
            <md-card-media>
                <img :src="feed.images.standard_resolution.url">
            </md-card-media>

            <md-card-header v-if="feed.caption">
                <div class="md-title">{{ feed.caption.from.full_name }}</div>
                <div class="md-subhead">{{ feed.caption.from.username }}</div>
            </md-card-header>

            <md-card-content>
                {{ feed.caption.text }}
            </md-card-content>
        </md-card>
    </div>
</template>

<script>
    import jsonp from 'jsonp'

    export default {
        name: 'TagSearch',
        data () {
            return {
                tagName: '',
                feeds: []
            }
        },
        mounted() {
            this.search()
        },
        methods: {
            search() {
                if (this.tagName === '') {
                    return
                }
                console.log('search')
                const token = localStorage.getItem('token')
                this.isLoading = true
                jsonp(`https://api.instagram.com/v1/tags/${this.tagName}/media/recent?access_token=${token}`, null, (_, response) => {
                    this.feeds = response.data
                    this.isLoading = false
                    console.log(response.data)
                })
            }
        }

    }
</script>