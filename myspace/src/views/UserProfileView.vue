<template>
    <ContentBase>
        <div class="row">
            <div class="col-3">
                <UserProfileInfo @follow="follow" @unfollow="unfollow" :user="user"/>
            </div>
            <div class="col-9">
                <UserProfilePosts :posts="posts"/>
            </div>
        </div>
    </ContentBase>
</template>

<script>
import { reactive } from 'vue';
import ContentBase from '../components/ContentBase';
import UserProfileInfo from '../components/UserProfileInfo';
import UserProfilePosts from '../components/UserProfilePosts';

export default {
    name: 'UserProfileView',
    components: {
        ContentBase,
        UserProfileInfo,
        UserProfilePosts,
    },

    setup() {
        const user = reactive({
            username: "lijiahao",
            lastName: "Li",
            firstName: "Jiahao",
            followerCount: 0,
            is_followed: false,
        });

        const posts = reactive({
            count: 3,
            posts: [
                {
                    id: 1,
                    userId: 1,
                    content: "测试1",
                },
                {
                    id: 2,
                    userId: 1,
                    content: "测试2",
                },
                {
                    id: 3,
                    userId: 1,
                    content: "测试3",
                },
            ]
        });
        
        const follow = () => {
            if (user.is_followed) return;
            user.is_followed = true;
            user.followerCount ++ ;
        };

        const unfollow = () => {
            if (!user.is_followed) return;
            user.is_followed = false;
            user.followerCount -- ;
        }

        return {
            user: user, // 如果类似这样key和value的值得一样可以简写为user
            follow,
            unfollow,
            posts,
        }
    }
}
</script>

<style scoped>
</style>