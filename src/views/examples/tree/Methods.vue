<script lang="tsx">
  import { defineComponent, ref, unref } from 'compatible-vue';

  import { BasicTree, TreeActionType } from '@/components/tree/index';

  import { useMessage } from '@/hooks/core/useMessage';
  import { treeData } from './data';

  export default defineComponent({
    name: 'TreeMethodsDemo',
    setup() {
      const treeElRef1 = ref<TreeActionType | null>(null);
      const { createMessage } = useMessage();
      return () => {
        function filterLevel() {
          const treeEl = unref(treeElRef1);
          if (!treeEl) {
            return;
          }
          treeEl.filterByLevel(1);
        }

        function getCheckKeys() {
          const treeEl = unref(treeElRef1);
          if (!treeEl) {
            return;
          }
          const keys = treeEl.getCheckedKeys();
          createMessage.success(JSON.stringify(keys));
        }

        function setCheckKeys() {
          const treeEl = unref(treeElRef1);
          if (!treeEl) {
            return;
          }
          treeEl.setCheckedKeys(['0-0']);
        }
        function getExpandKeys() {
          const treeEl = unref(treeElRef1);
          if (!treeEl) {
            return;
          }
          const keys = treeEl.getExpandedKeys();
          createMessage.success(JSON.stringify(keys));
        }

        function setExpandKeys() {
          const treeEl = unref(treeElRef1);
          if (!treeEl) {
            return;
          }
          treeEl.setExpandedKeys(['2-2']);
        }

        function getSelectKeys() {
          const treeEl = unref(treeElRef1);
          if (!treeEl) {
            return;
          }
          const keys = treeEl.getSelectedKeys();
          createMessage.success(JSON.stringify(keys));
        }

        function setSelectKeys() {
          const treeEl = unref(treeElRef1);
          if (!treeEl) {
            return;
          }
          treeEl.setSelectedKeys(['2-2']);
        }
        return (
          <div class="tree-demo">
            <div class="tree-demo-item">
              <div class="tree-demo-title">函数使用示例</div>
              <a-button onClick={filterLevel}>显示到第2级</a-button>
              <a-button onClick={getCheckKeys} class="ml-2">
                获取勾选数据
              </a-button>
              <a-button onClick={setCheckKeys} class="ml-2">
                设置勾选数据
              </a-button>

              <a-button onClick={getSelectKeys} class="ml-2">
                获取选中数据
              </a-button>
              <a-button onClick={setSelectKeys} class="ml-2">
                设置选中数据
              </a-button>
              <a-button onClick={getExpandKeys} class="ml-2">
                获取展开数据
              </a-button>
              <a-button onClick={setExpandKeys} class="ml-2">
                设置展开数据
              </a-button>

              <BasicTree treeData={treeData} ref={treeElRef1} checkable={true} />
            </div>
          </div>
        );
      };
    },
  });
</script>
<style scoped lang="less">
  .tree-demo {
    position: relative;
    display: flex;
    padding: 20px;

    &-item {
      width: 100%;
      min-height: 500px;
      padding-left: 20px;
      margin-right: 2%;
      background: #fff;
      border-radius: 10px;
    }

    &-title {
      width: 100%;
      padding-top: 20px;
      font-size: 20px;
      text-align: center;
    }
  }
</style>
