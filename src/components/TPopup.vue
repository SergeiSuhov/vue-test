<template>
  <transition name="fade">
    <div v-if="isOpen" class="t-popup_backdrop" @click.self="closeModal">
      <div class="t-popup">
        <slot></slot>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 't-popup',
  props: {
    isOpen: {
      type: Boolean,
      required: true
    }
  },
  mounted () {
    if (typeof document !== 'undefined') {
      document.addEventListener('keydown', this.keyListener)
    }
  },
  destroyed () {
    if (typeof document !== 'undefined') {
      document.removeEventListener('keydown', this.keyListener)
    }
  },
  methods: {
    closeModal () {
      this.$emit('onClose')
    },
    keyListener (evt) {
      if (this.isOpen && evt.key === 'Escape') {
        this.closeModal()
      }
    }
  }
}
</script>

<style>
.t-popup_backdrop {
  position: fixed;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  overflow: auto;
  display: flex;
  flex-flow: nowrap;
  justify-content: center;
  align-items: center;
  padding: 20px;
  background-color: rgba(0, 0, 0, 0.609);
  z-index: 100;
}

.t-popup {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.fade-enter-active,
.modal-leave-active {
  transition: opacity .6s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
