<template>
  <div class="vm-editor-menu">
    <VmEditorButton icon="paragraph" @click.native="execCommand('formatBlock', '<p>')"></VmEditorButton>
    <VmEditorButton icon="heading">
      <VmEditorDropdown>
        <ul class="vm-editor-ul">
          <li @click="execCommand('formatBlock', '<h1>')">
            <button>
              <h1>H1</h1>
            </button>
          </li>
          <li @click="execCommand('formatBlock', '<h2>')">
            <button>
              <h2>H2</h2>
            </button>
          </li>
          <li @click="execCommand('formatBlock', '<h3>')">
            <button>
              <h3>H3</h3>
            </button>
          </li>
          <li @click="execCommand('formatBlock', '<h4>')">
            <button>
              <h4>H4</h4>
            </button>
          </li>
          <li @click="execCommand('formatBlock', '<h5>')">
            <button>
              <h5>H5</h5>
            </button>
          </li>
        </ul>
      </VmEditorDropdown>
    </VmEditorButton>
    <VmEditorButton icon="font-size">
      <VmEditorDropdown>
        <ul class="vm-editor-ul">
          <li @click="execCommand('fontSize', 7)">
            <button style="font-size: 24px">7</button>
          </li>
          <li @click="execCommand('fontSize', 6)">
            <button style="font-size: 22px">6</button>
          </li>
          <li @click="execCommand('fontSize', 5)">
            <button style="font-size: 20px">5</button>
          </li>
          <li @click="execCommand('fontSize', 4)">
            <button style="font-size: 18px">4</button>
          </li>
          <li @click="execCommand('fontSize', 3)">
            <button style="font-size: 16px">3</button>
          </li>
          <li @click="execCommand('fontSize', 2)">
            <button style="font-size: 14px">2</button>
          </li>
          <li @click="execCommand('fontSize', 1)">
            <button style="font-size: 12px">1</button>
          </li>
        </ul>
      </VmEditorDropdown>
    </VmEditorButton>
    <VmEditorButton icon="bold" @click.native="execCommand('bold')"></VmEditorButton>
    <VmEditorButton icon="italic" @click.native="execCommand('italic')"></VmEditorButton>
    <VmEditorButton icon="underline" @click.native="execCommand('underline')"></VmEditorButton>
    <VmEditorButton icon="strikethrough" @click.native="execCommand('strikeThrough')"></VmEditorButton>
    <VmEditorButton icon="font-color">
      <VmEditorDropdown>
        <VmEditorFontcolor></VmEditorFontcolor>
      </VmEditorDropdown>
    </VmEditorButton>

    <span class="line"></span>

    <VmEditorButton icon="ol" @click.native="execCommand('insertOrderedList')"></VmEditorButton>
    <VmEditorButton icon="ul" @click.native="execCommand('insertUnorderedList')"></VmEditorButton>
    <VmEditorButton icon="quote"  @click.native="execCommand('formatBlock', '<blockquote>')"></VmEditorButton>
    <VmEditorButton icon="code" @click.native="execCommand('formatBlock', '<pre>')"></VmEditorButton>
    <!-- <VmEditorButton icon="fa fa-table"></VmEditorButton> -->

    <span class="line"></span>

    <VmEditorButton icon="image">
      <VmEditorDropdown>
        <VmEditorAddimage></VmEditorAddimage>
      </VmEditorDropdown>
    </VmEditorButton>
    
    <VmEditorButton icon="link">
      <VmEditorDropdown>
        <VmEditorAddlink></VmEditorAddlink>
      </VmEditorDropdown>
    </VmEditorButton>
    <VmEditorButton icon="line" @click.native="execCommand('insertHorizontalRule')"></VmEditorButton>

    <span class="line"></span>
    
    <VmEditorButton icon="align-center" @click.native="execCommand('justifyCenter')"></VmEditorButton>
    <VmEditorButton icon="align-left" @click.native="execCommand('justifyLeft')"></VmEditorButton>
    <VmEditorButton icon="align-right" @click.native="execCommand('justifyRight')"></VmEditorButton>
    <VmEditorButton icon="justify" @click.native="execCommand('justifyFull')"></VmEditorButton>

    <span class="line"></span>
    
    <VmEditorButton icon="eraser" @click.native="execCommand('removeFormat')"></VmEditorButton>
    <VmEditorButton icon="trash" @click.native="execCommand('delete')"></VmEditorButton>
    <slot></slot>
  </div>
</template>
<style lang="scss">
  .vm-editor-menu{
    width: 100%;
    box-sizing: border-box;
    display: flex;
    height: 40px;
    align-items: center;
    padding: 0 15px;
    background-color: #fafbfc;
    border-bottom: 1px solid #eeeff1;
    position: relative;
    .line{
      display: inline-block;
      width: 1px;
      height: 40px;
      margin: 0 10px;
      background-color: #eeeff1;
    }
  }
  ul.vm-editor-ul{
    padding: 0;
    margin: 0;
    li{
      margin: 0;
      padding: 6px 30px;
      display: flex;
      justify-content: center;
      &:hover{
        background: #f8f8f8;
      }
      h1{
        text-align: center;
      }
      button{
        color: inherit;
        width: 100%;
        height: 100%;
        background: transparent;
        border: none;
        cursor: pointer;
      }
    }  
  }
</style>
<script>
import VmEditorButton from './vm-editor-button.vue'
import VmEditorDropdown from './vm-editor-dropdown.vue'
import VmEditorAddlink from './vm-editor-addlink.vue'
import VmEditorAddimage from './vm-editor-addimage.vue'
import VmEditorFontcolor from './vm-editor-fontcolor.vue'
export default {
  name: 'VmEditorMenu',
  components: {
    VmEditorButton,
    VmEditorDropdown,
    VmEditorAddlink,
    VmEditorAddimage,
    VmEditorFontcolor
  },
  methods: {
    execCommand: function (commandName, valueArgument) {
      if (!valueArgument) {
        valueArgument = null
      }
      document.execCommand(commandName, false, valueArgument)
    },
    setImage: function (evt) {
      let reader = new FileReader()
      let file = evt.target.files[0]
      reader.readAsDataURL(file)
      reader.onload = function (evt) {
        let base64Image = evt.target.result
        document.execCommand('insertImage', false, base64Image)
      }
    }
  }
}
</script>
