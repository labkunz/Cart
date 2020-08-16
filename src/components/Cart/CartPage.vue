<template>
    <div>
        <a-card title="購物車">
            <h1>{{ test }}</h1>
            <a-button>test</a-button>
            <a-input-number defaultValue="1" :min="1" :max="10" />
            <CartList :dataSource="data"></CartList>
        </a-card>
    </div>
</template>
<script>
import CartList from './CartList'

export default {
    name: 'Cart',
    components : {
        CartList
    },
    props: {
        test: String
    },
    data: function() {
        return {
            data: [
                {
                    Goods: "Switch 二手主機",
                    Price: "$9970",
                    Number: 2,
                },
                {

                }
            ]
        }
    }
}
</script>