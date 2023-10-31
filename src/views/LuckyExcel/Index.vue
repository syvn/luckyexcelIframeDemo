<template>
    <div class="LuckyExcel">
        <input type="file" @change="changeFile" />
        <LuckyExcelExtend ref="fileRef"></LuckyExcelExtend>
    </div>
</template>

<script>
import LuckyExcelExtend from '../../components/luckyexcelExtend/Index.vue';

export default {
    name: 'LuckyExcel',
    props: {},
    components: {
        LuckyExcelExtend,
    },
    data() {
        return {
            file: null,
        };
    },
    watch: {},
    created() {},
    methods: {
        changeFile(event) {
            this.file = event.target.files[0];

            this.$refs.fileRef.selectFile(this.file);
        },
    },
};
</script>

<style lang="scss" scoped>
.LuckyExcel {
    display: flex;
    flex-direction: column;
    .tip {
        margin-bottom: 20px;
    }
    overflow: auto;
    height: 100vh;
    width: 100%;
}
</style>
