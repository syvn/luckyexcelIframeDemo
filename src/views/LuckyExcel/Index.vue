<template>
    <div class="LuckyExcel">
        <div class="input-control">
            <input type="file" @change="changeFile($event, 'fileRef')" />
            <input type="file" @change="changeFile($event, 'fileRef1')" />
        </div>
        <LuckyExcelExtend ref="fileRef"></LuckyExcelExtend>
        <LuckyExcelExtend ref="fileRef1"></LuckyExcelExtend>
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
        changeFile(event, type) {
            this.file = event.target.files[0];

            this.$refs[type].selectFile(this.file);
        },
    },
};
</script>

<style lang="scss" scoped>
.LuckyExcel {
    display: flex;
    flex-direction: column;
    .input-control {
        height: 40px;
        line-height: 40px;
    }
    overflow: auto;
    height: 100vh;
    width: 100%;
}
</style>
