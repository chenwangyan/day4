<template>
    <div>
      <p>{{fullName}}</p>
      <p><input type="text" v-model="firstName"></p>
</div>
</template>

<script>
export default {
  data() {
    return {
      firstName: 'Dawei',
    lastName: 'Lou',
    fullName: ''
    };
  },
  watch: {
    firstName() {
        debugger;
      this.fullName =   ' ' + this.lastName;
    // handler(newName, oldName) {
    //   this.fullName = newName + ' ' + this.lastName;
    // }
    // // 代表在wacth里声明了firstName这个方法之后立即先去执行handler方法，如果设置了false，那么效果和上边例子一样
    // immediate: true
    }
  },
  methods: {
    
  },
  created(){
  }
};
</script>
 
