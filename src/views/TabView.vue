<script setup>
  import { ref } from 'vue'

  const active = ref(0)
  const items = ref([
  '吾輩は猫である',
  'セロ弾きのゴーシュ'
  ])

  const activate = (index) => {
        active.value = index;
      }

</script>


<template>
  <h1>タブ</h1>
  <ul class="tab">
    <li class="tab-item" v-for="(item, index) in items" :key="index" :class="{ active: active === index }">
      <a href="#" @click.prevent="activate(index)">{{ item }}</a>
    </li>
  </ul>
  <div class="tab-content">
    <div class="tab-pane" v-show="active === 0">
      <p>吾輩は猫である。名前はまだ無い。</p>
      <p>どこで生れたかとんと見当がつかぬ。何でも薄暗いじめじめした所でニャーニャー泣いていた事だけは記憶している。吾輩はここで始めて人間というものを見た。しかもあとで聞くとそれは書生という人間中で一番獰悪な種族であったそうだ。この書生というのは時々我々を捕えて煮て食うという話である。しかしその当時は何という考もなかったから別段恐しいとも思わなかった。ただ彼の掌に載せられてスーと持ち上げられた時何だかフワフワした感じがあったばかりである。掌の上で少し落ちついて書生の顔を見たのがいわゆる人間というものの見始であろう。この時妙なものだと思った感じが今でも残っている。第一毛をもって装飾されべきはずの顔がつるつるしてまるで薬缶だ。その後ご猫にもだいぶ逢ったがこんな片輪には一度も出会した事がない。のみならず顔の真中があまりに突起している。そうしてその穴の中から時々ぷうぷうと煙けむりを吹く。どうも咽ぽくて実に弱った。これが人間の飲む煙草というものである事はようやくこの頃知った。</p>
    </div>
    <div class="tab-pane" v-show="active === 1">
      <p>ゴーシュは町の活動写真館でセロを弾く係りでした。けれどもあんまり上手でないという評判でした。上手でないどころではなく実は仲間の楽手のなかではいちばん下手でしたから、いつでも楽長にいじめられるのでした。　ひるすぎみんなは楽屋に円くならんで今度の町の音楽会へ出す第六交響曲の練習をしていました。　トランペットは一生けん命歌っています。　ヴァイオリンも二いろ風のように鳴っています。　クラリネットもボーボーとそれに手伝っています。　ゴーシュも口をりんと結んで眼を皿のようにして楽譜を見つめながらもう一心に弾いています。　にわかにぱたっと楽長が両手を鳴らしました。みんなぴたりと曲をやめてしんとしました。楽長がどなりました。</p>
      <p>「セロがおくれた。トォテテ　テテテイ、ここからやり直し。はいっ。」みんなは今の所の少し前の所からやり直しました。ゴーシュは顔をまっ赤にして額に汗を出しながらやっといま云われたところを通りました。ほっと安心しながら、つづけて弾いていますと楽長がまた手をぱっと拍ちました。</p>
    </div>
  </div>
</template>

<style scoped>
    .tab {
      list-style: none;
      border-bottom: 1px solid #ccc;
    }
    .tab-item {
      border: 1px solid transparent;
      border-bottom: none;
      display: inline-block;
      margin: 0 0 -1px;
      border-radius: 4px 4px 0 0;
    }
    .tab-item:hover {
      border-color: #ccc;
    }
    .tab-item a {
      display: block;
      padding: 10px 15px;
    }
    .tab-item.active {
      border-color: #ccc;
      background-color: #fff;
    }
    .tab-item.active a {
      color: #606c76;
    }
  </style>
