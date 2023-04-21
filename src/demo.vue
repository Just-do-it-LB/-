<template>
  <t-cascader
    v-model="value1"
    value-type="full"
    :options="options"
    :load="load"
    multiple
    @change="handleChange1"
  />
</template>
<script>
export default {
  data() {
    return {
      options: [
        {
          label: '选项1',
          value: '1',
          children: true,
        },
        {
          label: '选项2',
          value: '2',
          children: true,
        },
      ],
      value1: [
        ['1', '1-1.0', '1-1.0-2.1', '1-1.0-2.1-2.2'],
        ['1', '1-1.0', '1-1.0-1.1', '1-1.0-1.1-1.2'],
        ['1', '1-1.0', '1-1.0-1.1', '1-1.0-1.1-2.2'],
      ],
    };
  },
  methods: {
    load(node) {
      console.log('22--');
      return new Promise((resolve) => {
        setTimeout(() => {
          let nodes = [];
          console.log('-bb-', node, node.label, node.level);
          // children: true 表示 是否自动去加载 下一集合的菜单项。
          nodes = [
            {
              label: `${node.label}.1`,
              value: `${node.value}-1.${node.level}`,
              children: node.level < 2,
            },
            {
              label: `${node.label}.2`,
              value: `${node.value}-2.${node.level}`,
              children: node.level < 2,
            },
          ];
          resolve(nodes);
        }, 1000);
      });
    },
    handleChange(value) {
      console.log('value', value);
    },
    handleChange1(value, context) {
      // const { node } = context;
      // const path = node.getPath();
      // const labelPath = path.map((item) => item.label).join(' / ');
      // this.inputProps.value = labelPath;
      console.log('value1', value);
    },
  },
};
</script>
