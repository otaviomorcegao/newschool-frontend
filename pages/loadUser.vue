<template>
  <div class="body__loading">
    <div class="gooey">
      <span class="dot"></span>
      <div class="dots">
        <span></span>
        <span></span>
        <span></span>
      </div>
    </div>
    <div id="text">
      <p>Carregando seus dados...</p>
    </div>
  </div>
</template>

<router>
    {
        path : '/loading/:route',
        props: true
    }
</router>

<script>
import { mapActions } from "vuex";
import auth from "~/services/http/auth";

export default {
  mounted() {
    const { status, token } = auth.isTokenValid();
    if (status) {
      this.loadInfoUser({ token, route: this.route });
    } else {
      localStorage.clear();
      // eslint-disable-next-line no-undef
      $nuxt._router.push("/login");
    }
  },
  methods: {
    ...mapActions("user", ["loadInfoUser"])
  },
  props: ["route"],
  
};
</script>

<style lang="scss" scoped>
.body__loading {
  position: absolute;
  width: 100%;
  height: 100%;
  background: white;
}
#text {
  position: absolute;
  top: 55%;
  width: 100%;
  display: flex;
  justify-content: center;

  p {
    color: #6600cc;
    font-weight: 500;
    font-size: medium;
  }
}
.gooey {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 142px;
  height: 40px;
  margin: -20px 0 0 -71px;
  background: transparent;
}
.gooey .dot {
  position: absolute;
  width: 16px;
  height: 16px;
  top: 12px;
  left: 15px;
  background: #000;
  border-radius: 50%;
  transform: translateX(0);
  animation: dot 2.8s infinite;
}
.gooey .dots {
  transform: translateX(0);
  margin-top: 12px;
  margin-left: 31px;
  animation: dots 2.8s infinite;
}
.gooey .dots span {
  display: block;
  float: left;
  width: 16px;
  height: 16px;
  margin-left: 16px;
  background: #000;
  border-radius: 50%;
}
@-moz-keyframes dot {
  50% {
    transform: translateX(96px);
  }
}
@-webkit-keyframes dot {
  50% {
    transform: translateX(96px);
  }
}
@-o-keyframes dot {
  50% {
    transform: translateX(96px);
  }
}
@keyframes dot {
  50% {
    transform: translateX(96px);
  }
}
@-moz-keyframes dots {
  50% {
    transform: translateX(-31px);
  }
}
@-webkit-keyframes dots {
  50% {
    transform: translateX(-31px);
  }
}
@-o-keyframes dots {
  50% {
    transform: translateX(-31px);
  }
}
@keyframes dots {
  50% {
    transform: translateX(-31px);
  }
}
</style>