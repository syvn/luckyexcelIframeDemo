<template>
    <div class="LuckyExcelExtend">
        <iframe ref="iframeContent" src="/table.html" frameborder="0" @load="load"></iframe>
    </div>
</template>

<script>
import LuckyExcel from 'luckyexcel';

export default {
    name: 'LuckyExcelExtend',
    components: {},
    data() {
        return {
            iframeLoading: false,
        };
    },
    computed: {},
    created() {},
    methods: {
        update() {},
        load() {
            this.iframeLoading = true;
        },
        selectFile(fileData) {
            this.loading = true;

            LuckyExcel.transformExcelToLucky(fileData, (exportJson) => {
                if (exportJson.sheets == null || exportJson.sheets.length == 0) {
                    alert('Failed to read the content of the excel file, currently does not support xls files!');
                    return;
                }

                this.options = {
                    container: 'luckysheet',
                    lang: 'zh', // 设定表格语言
                    showinfobar: false,
                    data: exportJson.sheets,
                    title: exportJson.info.name,
                    userInfo: exportJson.info.creator,
                    sheetFormulaBar: false,
                    showsheetbar: true, // sheet页显示控制, 和showsheetbarConfig一起
                    showsheetbarConfig: {
                        add: false,
                        menu: false,
                        sheet: true,
                    },
                    showstatisticBar: false, // 底部计数栏
                    enableAddRow: false,
                    showtoolbar: false,
                    cellRightClickConfig: {
                        copy: false, // 复制
                        copyAs: false, // 复制为
                        paste: false, // 粘贴
                        insertRow: false, // 插入行
                        insertColumn: false, // 插入列
                        deleteRow: false, // 删除选中行
                        deleteColumn: false, // 删除选中列
                        deleteCell: false, // 删除单元格
                        hideRow: false, // 隐藏选中行和显示选中行
                        hideColumn: false, // 隐藏选中列和显示选中列
                        rowHeight: false, // 行高
                        columnWidth: false, // 列宽
                        clear: false, // 清除内容
                        matrix: false, // 矩阵操作选区
                        sort: false, // 排序选区
                        filter: false, // 筛选选区
                        chart: false, // 图表生成
                        image: false, // 插入图片
                        link: false, // 插入链接
                        data: false, // 数据验证
                        cellFormat: false, // 设置单元格格式
                        sheetFormulaBar: false,
                    },
                    allowEdit: false, //是否允许前台编辑
                    editMode: false,
                };

                this.loading = false;
                this.sendMessageTo();
            });
        },
        sendMessageTo() {
            if (this.timer) {
                window.clearTimeout(this.timer);
            }
            if (this.iframeLoading) {
                this.$refs.iframeContent.contentWindow.postMessage(JSON.stringify(this.options));
            } else {
                this.timer = window.setTimeout(() => {
                    this.sendMessageTo();
                }, 500);
            }
        },
    },
};
</script>

<style lang="scss" scoped>
.LuckyExcelExtend {
    height: 100%;
    width: 100%;

    iframe {
        display: block;
        width: 100%;
        height: 100%;
    }
}
</style>
