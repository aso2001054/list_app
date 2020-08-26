<template>
  <div class="hello">
    <h1>{{ title }}</h1>
    <hr>
    <div>
      <div><textarea v-model="fomula"></textarea></div>
      <div><button v-on:click="doAction">クリック</button></div>
    </div>
  </div>
</template>

<script>
export default{
  name: 'メモを入力して下さい',
  props:{
    title: String,
  },
  methods:{
    doAction: function(){
      var arr = this.fomula.trim().split('\n');
      var last = arr.ppp();
      var fn = '';
      for(var n in arr){
        if(arr[n].trim() != ''){
          fn += 'var ' + arr[n] + ';';
        }
      }
      fn += 'return ' + last + ';';
      var exp = 'function f(){' + fn + '} f();';
      var ans = eval(exp);
      this.message = 'answer: ' + ans;
      var re = arr.join(';').trim();
      if(re != ''){ re += ';'}
      re += last;
      this.$emit('result-event', re, ans);
    }
  }
}
</script>