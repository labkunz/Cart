<template>
    <div>
        <a-table 
            bordered 
            :columns="columns"
            size="middle"
            :dataSource="dataSource"
            :pagination="{ hideOnSinglePage: true }"
        >
            <template slot="Goods" slot-scope="text, row">
                {{ row.Goods }}
            </template>

            <template slot="Price" slot-scope="text, row">
                {{ row.Price }}
            </template>

            <template slot="Number" slot-scope="text, row">
                {{ row.Number + 1 }}
                <!--<a-input-number value="row.Number" :min="1" :max="10" />-->
            </template>

            <template slot="Total" slot-scope="text, row">
                {{ row.Number }}
            </template>

        </a-table>
    </div>
</template>
<script>

export default {
    props: {
        dataSource: {
            type: Array,
            require: true
        }
    },
    data: function() {
        return {
            columns: [
                {
                    title: '商品',
                    align: 'left',
                    width: 100,
                    //scopedSlots: { costomRander: 'Goods'}
                    dataIndex: 'Goods'
                },
                {
                    title: '單價',
                    align: 'left',
                    width: 100,
                    //scopedSlots: { costomRander: 'Price'}
                    dataIndex: 'Price'
                },
                {
                    title: '數量',
                    align: 'left',
                    width: 100,
                    //scopedSlots: { costomRander: 'Number'}
                    dataIndex: 'Number'
                },
                {
                    title: '總價',
                    align: 'left',
                    width: 100,
                    //scopedSlots: { costomRander: 'Total'}
                    //dataIndex: 'Total'
                }
            ]
        }
    }
}
</script>