<template>
  <div>
    <p>文件头记录歌曲和歌词的一些基本信息。</p>
    <div class="form">
      <VueFormField
        title="歌曲语言"
        subtitle="歌曲语言用于帮助播放器确定是否显示翻译和注音"
      >
        <VueSelect v-model="lang" placeholder="选择语言">
          <VueSelectButton value="zh" label="中文"/>
          <VueSelectButton value="ja" label="日本語"/>
          <VueSelectButton value="en" label="English"/>
        </VueSelect>
      </VueFormField>
      <VueFormField
        title="歌曲标题"
        subtitle="收录专辑中的正式标题"
      >
        <VueInput v-model="title" placeholder="例：純情エモーショナル (八重ver.)"/>
      </VueFormField>
      <VueFormField
        title="艺术家"
        subtitle="收录专辑中标明的所属艺人，通常为“歌手”"
      >
        <VueInput v-model="artist" placeholder="例：赤﨑千夏"/>
      </VueFormField>
      <VueFormField
        title="专辑"
        subtitle="收录专辑的名称"
      >
        <VueInput v-model="album"
                  placeholder="例：異世界はスマートフォンとともに。キャラクターソングvol.2 (八重&ユミナ)"
        />
      </VueFormField>
      <VueFormField
        title="作词"
        subtitle="歌词作者"
      >
        <VueInput v-model="lyricist" placeholder="例：buzzG"/>
      </VueFormField>
      <VueFormField
        title="作曲"
        subtitle="作曲，指歌曲人声部分旋律的创作者"
      >
        <VueInput v-model="composer" placeholder="例：buzzG"/>
      </VueFormField>
      <VueFormField
        title="编曲"
        subtitle="其他相关创作者，如编曲、录音、混音等"
      >
        <VueInput v-model="arranger" placeholder="例：やしきん"/>
      </VueFormField>
      <VueFormField
        title="歌词贡献者"
        subtitle="本文档的编者，包括分词、时轴、翻译等"
      >
        <VueInput v-model="by" placeholder="例：柚子"/>
      </VueFormField>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { createHelpers } from 'vuex-map-fields'

import { Lyrics } from '@/model'

const { mapFields } = createHelpers({
  getterType: 'getCurrentDocumentField',
  mutationType: 'updateCurrentDocumentField'
})

export default Vue.extend({
  computed: {
    document (): Lyrics {
      return this.$store.getters.currentDocument
    },
    ...mapFields([
      'lang', 'artist', 'title', 'album',
      'lyricist', 'composer', 'arranger', 'by'
    ])
  }
})
</script>

<style lang="stylus" scoped>
.form
  margin 25px 0
  .vue-ui-form-field
    margin 20px 0
</style>
