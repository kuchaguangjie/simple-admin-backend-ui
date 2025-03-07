<template>
  <div :class="prefixCls">
    <span> {{ title }}</span>
    <Switch
      v-bind="getBindValue"
      @change="handleChange"
      :disabled="disabled"
      :checkedChildren="t('layout.setting.on')"
      :unCheckedChildren="t('layout.setting.off')"
    />
  </div>
</template>
<script lang="ts">
  import { defineComponent, PropType, computed } from 'vue';

  import { Switch } from 'ant-design-vue';
  import { useDesign } from '/@/hooks/web/useDesign';
  import { useI18n } from '/@/hooks/web/useI18n';
  import { baseHandler } from '../handler';
  import { HandlerEnum } from '../enum';

  export default defineComponent({
    name: 'SwitchItem',
    components: { Switch },
    props: {
      event: {
        type: Number as PropType<HandlerEnum>,
      },
      disabled: {
        type: Boolean,
      },
      title: {
        type: String,
      },
      def: {
        type: Boolean,
      },
    },
    setup(props) {
      const { prefixCls } = useDesign('setting-switch-item');
      const { t } = useI18n();

      const getBindValue = computed(() => {
        return props.def ? { checked: props.def } : {};
      });
      function handleChange(checked: boolean | number | string, _e: Event) {
        props.event && baseHandler(props.event, checked);
      }
      return {
        prefixCls,
        t,
        handleChange,
        getBindValue,
      };
    },
  });
</script>

<style lang="less" scoped>
  @prefix-cls: ~'@{namespace}-setting-switch-item';

  [data-theme='dark'] {
    .@{prefix-cls} {
      display: flex;
      justify-content: space-between;
      margin: 16px 0;
      color: rgb(233 233 233);
    }
  }

  .@{prefix-cls} {
    display: flex;
    justify-content: space-between;
    margin: 16px 0;
    color: #262626;
  }
</style>
