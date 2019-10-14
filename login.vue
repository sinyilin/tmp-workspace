<template>
  <v-app id="login">
    <h4 class="white--text">Web Name</h4>
    <v-content>
      <v-container fluid fill-height>
        <v-layout align-center justify-center>
          <v-flex xs12 sm8 md4 lg4>
            <v-card class="elevation-1 pa-3">
              <v-card-text>
                <div class="layout column align-center">
                  <!-- <img src="../static/m.png" alt="Vue Material Admin" width="120" height="120"> -->
                  <h1 class="flex my-4 primary--text">Smart Charlie</h1>
                </div>
                <v-form>
                  <v-text-field append-icon="person" name="login" label="帳號" type="text"
                                v-model="model.username" :rules="[rules.required]"></v-text-field>
                  <v-text-field append-icon="lock" name="password" label="密碼" id="password" type="password"
                                v-model="model.password" :rules="[rules.required]"></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-spacer></v-spacer>
                <v-spacer></v-spacer>
                <v-spacer></v-spacer>
                <v-btn block color="primary" @click="login" :loading="loading">登入</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
  import VueCookies from 'vue-cookies';

  export default {
    layout: 'default',
    data: () => ({
      loading: false,
      model: {
        username: '',
        password: '',
        role: ''
      },
      rules: {
        required: (value) => !!value || 'Required.',
        email: (value) => {
          const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
          return pattern.test(value) || 'Invalid e-mail.';
        }
      }    
    }),

    methods: {
      login() {
        console.log(this.model.username);
        if(this.model.username == 'CB0002' && this.model.password == 'zaqwsx'){
          this.model.role = 'agent';
          VueCookies.set('user',this.model);
          this.loading = true;
          setTimeout(() => {
            this.$router.push('/customer');
          }, 1000);
        }else if(this.model.username == 'CB0003' && this.model.password == 'zaqwsx'){
          this.model.role = 'supervisor';
          VueCookies.set('user',this.model);
          this.loading = true;
          setTimeout(() => {
            this.$router.push('/customer');
          }, 1000);
        }else{
          alert('帳密錯誤');        
        }
      }
    },
    mounted(){
      VueCookies.set('user',{});
    }

  };
</script>
<style scoped lang="css">
  #login {
    height: 50%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    content: "";
    z-index: 0;
    background-color:rgb(69, 168, 184);
  }
</style>


