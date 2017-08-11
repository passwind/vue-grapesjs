<template>
  <div id="gjs">
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted () {
    var editor = grapesjs.init({
      container: '#gjs',
      panels: {
        defaults: [
          {
            id: 'left-control',
            buttons: [
              {
                id: 'open-blocks',
                className: 'fa fa-th-large',
                command: 'wh-open-blocks',
                active: true,
                attributes: { title: 'Open Blocks' }
              },
              {
                id: 'open-layers',
                className: 'fa fa-bars',
                command: 'wh-open-layers',
                attributes: { title: 'Open Layer Manager' }
              }
            ]
          },
          {
            id: 'left-panel'
          },
          {
            id: 'right-control',
            buttons: [{
              id: 'open-sm',
              className: 'fa fa-paint-brush',
              command: 'wh-open-sm',
              active: true,
              attributes: { title: 'Open Style Manager' }
            }, {
              id: 'open-tm',
              className: 'fa fa-cog',
              command: 'wh-open-tm',
              attributes: { title: 'Settings' }
            }]
          },
          {
            id: 'right-panel'
          }
        ]
      },
      commands: {
        defaults: [{
          id: 'wh-open-blocks',
          run (editor, sender) {
            // var config = editor.Config
            // var pfx = config.stylePrefix;
            var bm = editor.BlockManager
            var panelC
            if (!this.blocks) {
              this.blocks = $('<div/>').get(0)
              this.blocks.appendChild(bm.render())
              var panels = editor.Panels
              panelC = panels.getPanel('left-panel')
              panelC.set('appendContent', this.blocks).trigger('change:appendContent')
            }

            this.blocks.style.display = 'block'
          },
          stop () {
            if (this.blocks) this.blocks.style.display = 'none'
          }
        }]
      },
      storageManager: {
        autosave: false
      }
    })
    var blockManager = editor.BlockManager
    // 'my-first-block' is the ID of the block
    blockManager.add('my-first-block', {
      label: 'Simple block',
      content: '<div class="my-block">This is a simple block</div>'
    })
  }
}
</script>

<style>
@import '../../static/vendors/grapes/css/grapes.min.css';

#gjs .gjs-editor .gjs-cv-canvas {
  padding-left: 264px;
  padding-right: 200px;
  width: 100%;
}

#gjs .gjs-editor .gjs-pn-panel#gjs-pn-left-control {
  width: 64px;
  height: 900px;
  left: 0;
  top: 0;
}

#gjs .gjs-editor .gjs-pn-panel#gjs-pn-left-panel {
  width: 200px;
  height: 900px;
  left: 64px;
  top: 0;
}

#gjs .gjs-editor .gjs-pn-panel#gjs-pn-right-control {
  width: 200px;
  height: 64px;
  right: 0;
  top: 0;
}

#gjs .gjs-editor .gjs-pn-panel#gjs-pn-right-panel {
  width: 200px;
  height: 836px;
  top: 64px;
  right: 0;
}
</style>
