<template>
    <div class="p-4 border m-2">
        <router-link :to="`/post/${id}`" class="text-left hover:text-black-70 underline text-black">{{ content }}</router-link>
        <div class="mt-2 text-right text-cs">Posted on {{ datePublished | moment("calendar") }}
            <AuthorLine :authorId="authorId" :noUserData="noUserData" />
        </div>
    </div>
</template>

<script>
    import AuthorLine from './AuthorLine.vue'

    export default {
        name: 'ListPost',
        components: {
            AuthorLine
        },
        props: {
            id: {
                required: true,
                type: Number
            },
            content: {
                required: true,
                type: String
            },
            authorId: {
                required: true,
                type: Number
            },
            datePublished: {
                required: true,
                type: String
            },
            noUserData: {
                required: false,
                default: false,
                type: Boolean
            },
        },
        data() {
            return {
                displayName: false,
                name: false
            }
        },
        async created() {
            if (this.noUserData) {
                return;
            }
            try {
                const res = await this.axios.get(`http://localhost:3000/users/${this.authorId}`);

                this.displayName = res.data.displayName;
                this.name = res.data.name;
            } catch(e) {
                console.error(e);
            }
        }
    }
</script>