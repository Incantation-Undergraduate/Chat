<script >
import { reactive } from 'vue'

export default {
  setup() {
    //   登陆注册
    const shopShow = false;
    function  GoRE(){
      this.shopShow = !this.shopShow;
      if (this.shopShow === true){
        var Login = document.getElementsByClassName('Login-body-container')[0];
        var Register = document.getElementsByClassName('registered-container')[0];
        Login.style.display = 'none';
        Register.style.display = 'block';
      }
    }
  function GoLogin(){
    var Login = document.getElementsByClassName('Login-body-container')[0];
    Login.style.display = 'block';
    var Register = document.getElementsByClassName('registered-container')[0];
    Register.style.display = 'none';

  }

    const handleSubmit = ({values, errors}) => {
      console.log('values:', values, '\nerrors:', errors)
    }

    const form = reactive({
      name: '',
      password: '',
      password2: '',
      email: '',
    });

    const rules = {
      name: [
        {
          required: true,
          message:'name is required',
        },
      ],
      password: [
        {
          required: true,
          message:'password is required',
        },
      ],
      password2: [
        {
          required: true,
          message:'密码必填',
        },
        {
          validator: (value, cb) => {
            if (value !== form.password) {
              cb('再次填写密码')
            } else {
              cb()
            }
          }
        }
      ],
      email: [
        {
          type: 'email',
          required: true,
        }
      ],
    }

    return {
      form,
      rules,
      shopShow,
      handleSubmit,
      GoRE,
      GoLogin

    }
  },
}
</script>

<template>
  <div class="Login-body">
    <div  class="Login-body-container" >
<!--      头像部分 以及登录选择部分-->
      <div class="Login-body-container-top">
          <div class="Login-body-container-top-icon">
<!--            头像-->
            <div class="Login-body-container-top-icon-avatar">
              <a-space class="Avtor" size="large">
                <a-avatar :size="80">Arco</a-avatar>
              </a-space>
              <p>名字</p>
            </div>
<!--            登录选项-->
            <div class="Login-body-container-top-icon-login">
              <ul>
                <li>
                  <icon-qq :size="32" :style="{fontSize:'32px'}" :stroke-width="2"/>
                </li>
                <li>
                  <icon-wechat :size="32" :style="{fontSize:'32px'}" :stroke-width="2"/>
                </li>
              </ul>
            </div>
          </div>
      </div>
      <a-divider :size="1"/>
<!--  登录框部分-->
      <div class="Login-body-container-bottom">
        <a-form :model="form" class="Login-bottom" @submit="handleSubmit">
          <a-form-item field="name" >
            <a-input
              class="user-name"
              placeholder="请输入用户名"
            />
          </a-form-item>
          <a-form-item field="passwd">
            <a-input-password
              class="user-passwd"
              style="color: #1c0b0b"
              placeholder="请输入密码"
            />
          </a-form-item>
          <a-form-item>
            <a-button style="width:100%;height: 55px;border-radius: 10px " html-type="submit">Submit</a-button>
          </a-form-item>
        </a-form>
<!--  注册   忘记密码-->
          <div class="regin">
            <p>
              <a href="#" style="color: #a6a6a6">
                忘记密码
              </a>
            </p>
            <p class="REGin" >
              <a href="#" style="color: #a6a6a6" @click="GoRE"  >
                注册
              </a>
            </p>
          </div>
      </div>
    </div>
<!-- registered   -->
    <div v-show="shopShow" class="registered-container">
      <a-form ref="formRef" :rules="rules" :model="form" :style="{width:'98%'}" @submit="handleSubmit">
        <a-form-item field="name"   :style="{width:'98%'}">
          <a-input style="height:55px;border-radius: 10px;background: rgba(255,255,255,0.5);backdrop-filter: blur(15)"
                   v-model="form.name" placeholder="请输入用户名" />
        </a-form-item>
        <a-form-item field="email" :style="{width:'98%'}">
          <a-input style="height:55px;border-radius: 10px;background: rgba(255,255,255,0.5);backdrop-filter: blur(15)"
                   v-model="form.email" placeholder="请输入邮箱" />
        </a-form-item>
        <a-form-item field="password"  validate-trigger="blur" :style="{width:'98%'}">
          <a-input-password style="height:55px;border-radius: 10px;background: rgba(255,255,255,0.5);backdrop-filter: blur(15)"
                            v-model="form.password" placeholder="请输入密码" />
        </a-form-item>
        <a-form-item field="password2"   :style="{width:'98%'}">
          <a-input-password style="height:55px;border-radius: 10px;background: rgba(255,255,255,0.5);backdrop-filter: blur(15)"
                            v-model="form.password2" placeholder="请确认密码" />
        </a-form-item>

        <a-form-item>
          <a-space>
            <a-button html-type="submit" style="width:340px;height: 55px;border-radius: 10px">Submit</a-button>
          </a-space>
        </a-form-item>
        <a-form-item>
          <p class="GoLogin" >
            <a href="#" @click="GoLogin">
              去登陆
            </a>
          </p>
        </a-form-item>
      </a-form>
    </div>
  </div>
</template>

<style scoped>
.Login-body{
  background-image: url("../assets/image/BackCover.png");
  height: 100%;
  width: 100%;
  background-size: cover;
  left: 0;
  top: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
}
.Login-body-container {
  width: 450px;
  height: 550px;
  display: block;

}
.Login-body-container-top{
  width: 100%;
  height: 275px;

}
.Login-body-container-bottom{
  width: 100%;
  height: 275px;

}
.Login-bottom{
  margin-left: -10%;
}
/*登录*/
.user-name{
  height: 55px;
  border-radius: 10px;
  margin-top: 10px;
  backdrop-filter: blur(15px);
  background: rgba(225, 225, 225, 0.5);
}
.user-passwd{
  height: 55px;
  color: #090808;
  border-radius: 10px;
  margin-top: 10px;
  backdrop-filter: blur(15px);
  background: rgba(255, 255, 255, 0.5);
}
/*去登录*/
.GoLogin{
  color: white;
}

/*注册*/
.regin{
  width: 100%;
  height: 2rem;
  display: flex;
}

/*头像*/
.Login-body-container-top-icon{
  width: 100%;
  height: 200px;
  border-radius: 0.2rem;

}
.Login-body-container-top-icon-avatar{
  width: 100%;
  height: 100%;
}
.Login-body-container-top-icon-avatar p{
  color: #1c0b0b;
  margin-top: 15%;
  font-size: 18px;
  margin-left: 45.5%;
}
.Avtor{
  position: relative;
  left: 40%;
  top: 20%;
}

.Login-body-container-top-icon-login{
  width: 90%;
  height: 75px;
  margin: 0 auto;

}
.Login-body-container-top-icon-login ul{
  width: 90%;
  display: flex;
  margin: 0 auto;
  list-style: none;
}

.Login-body-container-top-icon-login ul li{
  width: 15px;
  height: 70px;
  margin: 2px;
  flex: 1;
  text-align: center;
  line-height: 90px;
  border-radius: 15px;
  background: #122f4d;
}
/*注册*/
.registered-container{
  width: 450px;
  height: 550px;
  position: absolute;
  left: 30%;
  top: 20%;
  color: #b05e5e;
}
</style>