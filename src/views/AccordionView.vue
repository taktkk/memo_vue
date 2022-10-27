<script setup>
  import AccordionMenu from '@/components/AccordionMenu.vue';

</script>


<template>
  <AccordionMenu>
      <template v-slot:title>Chapter1-1</template>
      <template class="details" v-slot:detail>
        <h3>UI / UX</h3>
        <p>ページ遷移が必要ない。リアルタイムでのフィードバックが必要なサイトが増えてきた</p>
      </template>
    </AccordionMenu>
    <AccordionMenu>
      <template v-slot:title>Chapter1-2</template>
      <template class="details" v-slot:detail>
        <h3>jQueryとの違い</h3>
        <p>jQueryはDOMを外部から触るライブラリ</p>
        <p>Vue.jsはデータ（ViewModel）を管理することで仮想DOMを描画するライブラリ</p>
      </template>
    </AccordionMenu>
    <AccordionMenu>
      <template v-slot:title>Chapter1-3</template>
      <template class="details" v-slot:detail>
        <h3>React.jsとの違い</h3>
        <p>データによって仮想DOMを描画する点は一緒</p>
        <p>HTMLをそのままテンプレートとして利用できる</p>
        <p>つまりコンパイルも不要</p>
        <button>もっと読む</button>
      </template>
    </AccordionMenu>
</template>

<style scoped>
    AccordionMenu {
      overflow: hidden;
      transition: .3s ease-in-out;
    }

    AccordionMenu:nth-child(1) {
      background: rgb(240, 145, 140);
    }

    AccordionMenu:nth-child(2) {
      background: rgb(230, 187, 155);
    }

    AccordionMenu:nth-child(3) {
      background: rgb(126, 206, 144);
    }

    .details {
      padding: 10px;
    }

    .rotation-enter, .rotation-leave-to {
      transform: rotateX(180deg)
    }
  </style>