<template>
  <div>
    <split-pane>
      <component-tree
        v-if="defer(2)"
        slot="left"
        :instances="instances"
      />
      <component-inspector
        v-if="defer(3)"
        slot="right"
        :target="inspectedInstance"
        :loading="loading"
      />
    </split-pane>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import Defer from '@front/mixins/defer'

import SplitPane from '@front/components/SplitPane.vue'
import ComponentTree from './ComponentTree.vue'
import ComponentInspector from './ComponentInspector.vue'

const superDef = {
  data () {
    return {
      foo: 'bar'
    }
  }
}

export default {
  components: {
    ComponentTree,
    ComponentInspector,
    SplitPane
  },

  extends: superDef,

  mixins: [
    Defer()
  ],

  computed: mapState('components', [
    'instances',
    'inspectedInstance',
    'loading'
  ])
}
</script>
