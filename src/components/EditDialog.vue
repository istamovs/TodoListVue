<template>
  <div class="edit-dialog-overlay" v-if="show">
    <div class="edit-dialog container">
      <div class="input-container">
        <label>Enter the new value...</label>
        <input class="edit-input outlined" ref="dialogInput"/>
      </div>
      <div class="buttons-container">
        <div class="btn" @click="closeDialog">Close</div>
        <div class="btn" @click="acceptDialog">Accept</div>
      </div>
      <div class="close-btn" @click="closeDialog"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "EditDialog",
  props: {
    show: Boolean
  },
  methods: {
    acceptDialog() {
      this.$emit('accept', this.$refs.dialogInput.value)
      this.closeDialog()
    },
    closeDialog() {
      this.$emit('close')
    }
  }
}
</script>

<style scoped>
.edit-dialog-overlay {
  position: fixed;
  top: 0;
  left: 0;
  height: 100%;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.55);
}

.edit-dialog {
  height: 150px;
  width: 400px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #ffffa6;
}

.input-container {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 70%;
}

.edit-input {
  border: 2px solid black;
  border-radius: 5px;
  height: 30px;
  width: 100%;
}

.buttons-container {
  position: absolute;
  bottom: 10px;
  right: 10px;
  display: flex;
  gap: 10px;
}

.buttons-container .btn {
  height: 25px;
  width: 65px;
}

.close-btn{
  width: 25px;
  height: 25px;
  border-radius: 50%;
  margin: 3px;
  cursor: pointer;
  border: 2px solid #2d2b2b;
  position: absolute;
  margin-left: 365px;
}
.close-btn:before,
.close-btn:after {
  content: "";
  position: absolute;
  float: left;
  top: 11px;
  left: 2.5px;
  width: 20px;
  height: 4px;
  background: #2d2b2b;

}

.close-btn:before {
  webkit-transform: rotate(45deg);
  transform: rotate(45deg);
}

.close-btn:after {
  webkit-transform: rotate(-45deg);
  transform: rotate(-45deg);
}
</style>