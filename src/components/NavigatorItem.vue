<script setup lang="ts">
const props = withDefaults(defineProps<{
  mini?: boolean
  closeable?: boolean,
  label: string
  icon: string
  id: number | string
  active?: boolean,
  tab?: boolean
}>(), {
  mini: false,
  closeable: true,
  active: false,
  tab: false
})
const emit = defineEmits<{ ok: [number | string], close: [number | string] }>()

const click = (key: number | string) => {
  emit('ok', key)
}

const close = (key: number | string) => {
  emit('close', key)
}
</script>

<template>
  <div>
    <div
        class="_c_m_item cursor-default select-none rounded-lg px-1 py-1 hover:bg-[#32364A] text-white flex justify-between items-center"
        @click="click(props.id)" v-if="!props.mini" :class="{
          'tab-active': tab && active,
          'active': !tab && active
        }">
      <div class="flex items-center start w-full">
        <div class="w-30 h-30 flex justify-center  items-center">
          <div :class="props.icon" class="text-[18px]"></div>
        </div>
        <div class="text-12px w-90px text-ellipsis select-none cursor-default" style="overflow:hidden; white-space: nowrap">{{ props.label }}</div>
      </div>
      <div @click.stop="close(props.id)" v-if="props.closeable"
           class="_m_cos rounded-md hover:text-red bg-[#0001] p-4 cursor-pointer">
        <span class="i-ic-round-close"></span>
      </div>


      <div class="r1 hidden">
        <div class="r1-1"></div>
      </div>
      <div class="r2 hidden">
        <div class="r2-1"></div>
      </div>
    </div>
    <a-popover position="right" v-else :content-style="{
      'padding': '1px 10px'
    }">
      <div
          class="_c_m_item select-none rounded-lg px-1 py-1 hover:bg-[#32364A]  text-white flex  justify-between items-center"
          @click="click(props.id)" :class="{
          'tab-active': tab && active,
          'active': !tab && active
        }">
        <div class="flex items-center justify-center w-full ">
          <div class="w-30 h-30 flex justify-center  items-center">
            <div :class="props.icon" class="text-[18px]"></div>
          </div>
        </div>
        <div class="r1 hidden">
          <div class="r1-1"></div>
        </div>
        <div class="r2 hidden">
          <div class="r2-1"></div>
        </div>
      </div>
      <template #content>
        <div class="flex justify-center items-center pb-8px pt-4px px-3px">
          <span class="text-12px">{{ props.label }}</span>
          <div @click="close(props.id)" v-if="props.closeable"
               class="ml-[8px] rounded-md shrink-0 w-20 h-20 flex justify-center items-center hover:text-red bg-[#0001] cursor-pointer">
            <div class="_m_cos">
              <span class="i-ic-round-close "></span>
            </div>
          </div>
        </div>
      </template>
    </a-popover>
  </div>
</template>

<style lang="scss" scoped>
._c_m_item {
  position: relative;
  *{cursor: default;user-select: none}
  ._m_cos {
    display: none;
  }

  &:hover ._m_cos {
    display: flex;
  }
}

.active {
  background-color: rgb(62, 66, 87);
}
.r1,.r2 {
  width: 10px;
  height: 10px;
  background: #EDF1F2;
  position: absolute;
  right: -10px;
  overflow: hidden;
}
.r1 {
  top: -10px;
  .r1-1{
    border: 10px solid #282b3d;
    margin-top: -10px;
    margin-left: -10px;
    border-radius: 10px;
  }
}
.r2 {
  bottom: -10px;
  .r2-1{
    border: 10px solid #282b3d;
    margin-bottom: -10px;
    margin-left: -10px;
    border-radius: 10px;
  }
}
.tab-active {
  background: #EDF1F2 !important;
  color: black;
  border-top-right-radius: 0;
  border-bottom-right-radius: 0;
  position: relative;
  .r1,.r2{
    display: block;
  }
  &::after {
    content: '';
    position: absolute;
    right: -10px;
    top: 0;
    height: 100%;
    background: #EDF1F2;
    width: 10px;
  }
}
</style>