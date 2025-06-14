<script lang="ts">
import { defineComponent, ref } from 'vue';

import { checkImgType } from './helper';
import { PreviewModal } from './previewModal';
import { previewProps } from './props';

import { UploadApiResult } from '/@/api/sys/model/uploadModel';
import { uploadApi } from '/@/api/sys/upload';
import { BasicUpload } from '/@/components/Upload';
import { useMessage } from '/@/hooks/web/useMessage';

export default defineComponent({
  components: { BasicUpload, PreviewModal },
  setup() {
    const { createMessage } = useMessage();
    const fileList = ref<UploadApiResult[]>([]);
    const preview = ref<previewProps>({
      previewOpen: false,
      previewImage: '',
      previewTitle: '',
    });

    function handleChange(changeFileList: UploadApiResult[]) {
      fileList.value = changeFileList;
    }

    function handleDelete(record: UploadApiResult) {
      console.error('Delete', record);
      const index = fileList.value.findIndex((item) => item.uid === record.uid);
      index !== -1 && fileList.value.splice(index, 1);
    }

    async function handlePreview(record: UploadApiResult) {
      if (!record) return;
      if (!checkImgType(record)) {
        createMessage.warning('Please upload image files!');
        return;
      }
      if (!record.url) {
        createMessage.warning('File url does not exist!');
        return;
      }
      preview.value = {
        previewOpen: true,
        previewImage: record.url,
        previewTitle:
          record.name ||
          record.url.slice(Math.max(0, record.url.lastIndexOf('/') + 1)),
      };
    }

    function handleDownload(record: UploadApiResult) {
      console.error('Download', record);
      const { response } = record;
      const url: string = response?.data?.url || '';
      if (!url) {
        createMessage.warning('File url does not exist!');
        return;
      }
      window.open(url);
    }

    function handlePreviewCancel() {
      preview.value.previewOpen = false;
    }

    function handleUpload() {
      console.error('Upload', fileList.value);
    }

    function handleReset() {
      fileList.value = [];
    }

    return {
      fileList,
      preview,
      uploadApi,
      handleChange,
      handleDelete,
      handlePreview,
      handleDownload,
      handlePreviewCancel,
      handleUpload,
      handleReset,
    };
  },
});
</script>
<template>
  <div class="mb-4">
    <a-button type="primary" @click="handleUpload">Start Upload</a-button>
    <a-button class="ml-2" @click="handleReset">Reset</a-button>
  </div>
  <BasicUpload
    :max-size="20"
    :max-number="10"
    :api="uploadApi"
    :value="fileList"
    help-text="Only jpg/png files with a size less than 2MB can be uploaded"
    @change="handleChange"
    @delete="handleDelete"
    @preview="handlePreview"
    @download="handleDownload"
  />
  <PreviewModal
    :preview="preview"
    :preview-open="previewOpen"
    @preview-cancel="handlePreviewCancel"
  />
</template>
