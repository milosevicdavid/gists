<template>
  <div
    @click="changeId(item.id)"
    :class="['item-wrapper', { 'item-click-text': click === item.id }]"
  >
    <div class="avatar-wrapper">
      <img
        :src="item.owner.avatar_url"
        alt="avatar"
        :class="['avatar', { 'item-click-avatar': click === item.id }]"
      />
    </div>
    <div class="file-name">
      {{ Object.keys(item.files)[0] }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
      required: true
    }
  },

  data() {
    return {
      click: -1
    };
  },

  methods: {
    changeId(id) {
      this.click = id;
    }
  }
};
</script>

<style scoped>
.avatar {
  width: 150px;
  height: 150px;
}

.item-click-text {
  color: #177ef2;
}

.item-click-avatar {
  -webkit-filter: grayscale(50%) brightness(51%);
  animation: linear;
  animation-name: movefade;
  animation-duration: 2s;
  animation-fill-mode: forwards;
}

.item-wrapper {
  border-bottom: 1px solid lightgray;
  padding: 30px 0px;
  display: flex;
  justify-content: flex-start;
  width: 900px;
  cursor: pointer;
}

.item-wrapper:nth-child(2) {
  border-top: 1px solid lightgray;
}

.file-name {
  margin-left: 20px;
  display: flex;
  align-items: center;
}

@keyframes movefade {
  0% {
    transform: translateX(0%);
    opacity: 1;
  }
  50% {
    transform: translateX(250%);
    opacity: 1;
  }
  80% {
    transform: translateX(250%);
    opacity: 0.5;
  }
  100% {
    transform: translateX(250%);
    opacity: 0;
  }
}
</style>
