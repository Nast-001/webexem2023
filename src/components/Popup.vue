<template>
  <div class="popup_wrapper" ref="popup_wrapper">
    <div class='popup'>
      <div class="popup__header">
        <span>{{popupTitle}}</span>
        <span>
        <i class='bx bx-x' @click="closePopup"></i>
      </span>
      </div>
      <div class="popup__content">
        <slot></slot>
      </div>
      <div class="popup__footer">
        <button class="close_modal" @click="closePopup">Close</button>
        <button
            class="submit_btn"
            @click="rightBtnAction"
        >
          {{rightBtnTitle}}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "Popup",
    props: {
      popupTitle: {
        type: String,
        default: 'Popup name'
      },
      rightBtnTitle: {
        type: String,
        default: 'Ok'
      }
    },
    data() {
      return {}
    },
    methods: {
      rightBtnAction() {
        this.$emit('rightBtnAction')
      },
      closePopup() {
        this.$emit('closePopup')
      }
    },
    mounted() {
      let vm = this;
      document.addEventListener('click', function (item) {
        if (item.target === vm.$refs['popup_wrapper']) {
          vm.closePopup()
        }
      })
    },
  }
</script>

<style>
  .popup_wrapper {
    background: rgba(124, 123, 123, 0.4);
    min-height: 120vh;
    display: flex;
    justify-content: center;
    align-items: center;
    position: absolute;
    right: 0;
    left: 0;
    top: 0;
    bottom: 0;
  }
  .popup {
    padding: 50px;
    position: fixed;
    top: 50px;
    width: 320px;
    height: 400px;
    background: var(--popup-color);
    box-shadow: 0 0 17px 0 #e7e7e7;
    z-index: 10;
  }
  .popup__header, .popup__footer {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin: 0 auto;
  }
  .popup__content {
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .submit_btn {
    padding: 8px;
    color: #ffffff;
    background: #26ae68;
    border: none;
  }
  .close_modal {
    padding: 8px;
    color: #ffffff;
    border: none;
    background: red;
  }

</style>
