<!--templateの中身は一つのdivでくくらないとまずい-->
<template>
  <div class="card-body">
    <div class="card-body" style="border-bottom:1px solid black;" v-for="menu in menus">
      <p>タイトル：{{menu.title}}{{user.id}}</p>
      <p><img :src="menu.image" style="width:100px;"></p>
      <p>説明：{{menu.body}}</p>
      <p>価格：{{menu.price}}</p>
      <p>ホスト：<router-link :to="{name:'table', params:{profile:menu.profile_id}}">{{menu.profile.user_name}}</router-link></p>
      <p><router-link :to="{name:'table', params:{profile:menu.profile_id}}"><img :src="menu.profile.profile_image"></router-link></p>
    </div>
  </div>
</template>
<script>
  export default {
    created() {
      this.getMenus();
//      this.getUser();
    },
    data() {
      return {
        menus: [],
      }
    },
    props: {
      user:{
        type: Object,
      }
    },
//    computed: {
//      user_id: function(){
//        return JSON.parse(this.user);
//      }
//    },
    methods: {
      getMenus() {
        axios.get('/api')
        .then(res =>  {
          this.menus = res.data['menus'];
          console.log(this.menus);
        })
      },
//      getUser(){
//        var user=JSON.parse(this.user);
//        console.log(this.user);
//      }
    },
  }
</script>
